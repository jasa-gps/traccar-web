# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).

## What this is

Web interface (SPA) for the [Traccar](https://www.traccar.org) GPS tracking platform. This repo is **frontend only** — it talks to a separate Traccar backend server over a REST API (`/api`) and a WebSocket (`/api/socket`). There is no backend code here. The Java backend lives at [tananaev/traccar](https://github.com/tananaev/traccar).

Stack: React 19, Material UI 9 (`@mui/material`, styled via `tss-react`), Redux Toolkit, React Router 7, MapLibre GL, Vite 8 (SWC), built as a PWA.

## Commands

- `npm start` — dev server on port 3000 (`vite --host`). Proxies `/api` → `http://localhost:8082` and `/api/socket` → `ws://localhost:8082`, so a local Traccar backend on 8082 is expected.
- `npm run build` — production build to `build/`.
- `npm run lint` — ESLint with `--max-warnings 0` (CI fails on any warning). `npm run lint:fix` to autofix.

There is **no test suite or test runner** configured. Verification is lint + build + manual.

## Backend dependency

Nothing renders without a reachable backend. The app bootstraps in `src/App.jsx` by calling `GET /api/session`; on 401 it redirects to `/login` (or `/register` for a new server). All data flows through the backend's REST endpoints and the live WebSocket.

## Architecture

### Entry and providers
`src/index.jsx` mounts a fixed provider stack: `ErrorBoundary` → Redux `Provider` → `LocalizationProvider` (i18n) → MUI `StyledEngineProvider` → `AppThemeProvider` → `ServerProvider` (fetches `/api/server` config) → `BrowserRouter` → `Navigation`. `preloadImages()` warms map marker images before render.

### Routing
`src/Navigation.jsx` is the router. Public routes (`/login`, `/register`, `/reset-password`, `/change-server`) render directly; everything else is nested under the `App` layout (`src/App.jsx`), which gates on an authenticated session. **Nearly every page is `React.lazy()`-imported** — when adding a page, add both the `lazy(() => import(...))` declaration and its `<Route>`. Navigation also handles deep-link query params (`locale`, `token`, `uniqueId`, `openid`) on load.

### State (Redux Toolkit)
`src/store/index.js` combines slices: `errors`, `session`, `devices`, `events`, `motion`, `geofences`, `groups`, `drivers`, `maintenances`, `calendars`. A custom `throttleMiddleware` batches high-frequency position/device updates. `session` holds the current user, server config, live positions, and socket state — it is the most-read slice.

### Live data: SocketController
`src/SocketController.jsx` (rendered inside `App`) owns the `/api/socket` WebSocket. It dispatches incoming `devices`, `positions`, `events`, and `logs` into Redux; plays alarm sounds for configured event types; surfaces event snackbars; auto-reconnects (60s backoff, plus on `online`/`visibilitychange`); and on socket close falls back to refetching `/api/devices` and `/api/positions`. `CachingController`, `UpdateController`, and `MotionController` are sibling headless controllers under `App`.

### Async + error conventions (important — used everywhere)
From `src/reactHelper.js`:
- `useAsyncTask(effect, deps)` — for data-loading effects. `effect` receives `{ signal }` (an `AbortController` signal), may return a cleanup fn, and any non-abort rejection is auto-dispatched to the `errors` slice.
- `useCatch(fn)` / `useCatchCallback(fn, deps)` — wrap async handlers so rejections flow to the `errors` slice instead of being swallowed.
- `fetchOrThrow` (`src/common/util/fetchOrThrow.js`) — `fetch` wrapper that throws on non-`ok` responses (throwing the response body text). Prefer it over raw `fetch` for calls whose failures should surface as errors.

Together these mean: don't hand-write try/catch + manual error dispatch — use these helpers and let `ErrorHandler` render the result.

### Preferences resolution
`src/common/util/preferences.js` exposes `usePreference` / `useAttributePreference`. Settings resolve from user, then server, with order flipped when the server sets `forceSettings`. Use these rather than reading `state.session` directly for any user/server-configurable value.

### i18n
`LocalizationProvider` + `useTranslation()` (the single most-connected symbol in the codebase). UI strings come from per-language translation catalogs in `src/resources/l10n/` (e.g. `en.json`, `ar.json`); use the `t(...)` keys, never hardcoded user-facing text.

### Maps
`src/map/` wraps MapLibre GL imperatively. `map/core/MapView.jsx` is the shared map instance; subcomponents (`MapPositions`, `MapGeofence`, `MapMarkers`, routes, overlays, controls) attach sources/layers to it. Note the known import cycle `MapView.jsx ↔ preloadImages.js ↔ mapUtil.js` — be careful editing these three together.

## Directory map

- `src/main/` — main tracking screen: device list, map, toolbar, events drawer, status card.
- `src/settings/` — CRUD pages for devices, users, groups, drivers, geofences, calendars, commands, notifications, maintenances, computed attributes, server/user preferences. Mostly `*Page` (single item) + `*sPage` (collection) pairs over a shared `EditItemView`/`BaseCommandView` pattern in `settings/components/` and `settings/common/`.
- `src/reports/` — report pages (route, events, trips, stops, summary, chart, combined, statistics, logs, audit) with Excel export via `exceljs` (`common/util/exportExcel.js`).
- `src/other/` — replay, geofences editor, network/position detail, emulator, stream.
- `src/login/` — login, register, reset password, change server.
- `src/common/` — shared `components/`, `util/` (formatters, converters, permissions, features), `attributes/`, `theme/`.
- `src/store/` — Redux slices.
- `simple/` — a standalone minimal demo HTML app; not part of the main SPA build.

## Conventions

- **Styling:** `tss-react`'s `makeStyles()` (the `const useStyles = makeStyles()(theme => ({...}))` pattern), not CSS files or `styled`. Theme comes from `common/theme/`.
- **Files:** components `.jsx`, pure utilities `.js`. Match the existing pattern in the directory you're editing.
- **Lint is strict:** zero warnings allowed. `react-hooks/exhaustive-deps` is off, but `@eslint-react/exhaustive-deps` is on (warn) and additionally checks the custom `useCatchCallback`/`useAsyncTask` hooks — pass correct dep arrays to them.
- Prettier is enforced via `eslint-plugin-prettier`; `.prettierrc.json` controls format (single quotes).
- Git/commit conventions follow the user's global rules (lowercase, prefixed: `feat:`, `fix:`, etc.).
