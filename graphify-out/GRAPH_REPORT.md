# Graph Report - .  (2026-06-13)

## Corpus Check
- 288 files · ~169,120 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 643 nodes · 2214 edges · 31 communities (22 shown, 9 thin omitted)
- Extraction: 99% EXTRACTED · 1% INFERRED · 0% AMBIGUOUS · INFERRED: 12 edges (avg confidence: 0.78)
- Token cost: 0 input · 34,721 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Settings & Device Attributes|Settings & Device Attributes]]
- [[_COMMUNITY_Map Rendering & Controls|Map Rendering & Controls]]
- [[_COMMUNITY_Attribute Editing & Value Formatters|Attribute Editing & Value Formatters]]
- [[_COMMUNITY_Reporting & Exports|Reporting & Exports]]
- [[_COMMUNITY_Page Routing & Navigation|Page Routing & Navigation]]
- [[_COMMUNITY_Runtime Dependencies|Runtime Dependencies]]
- [[_COMMUNITY_Device Status & Main Panel|Device Status & Main Panel]]
- [[_COMMUNITY_Redux Store Slices|Redux Store Slices]]
- [[_COMMUNITY_Project Stack & Integrations|Project Stack & Integrations]]
- [[_COMMUNITY_Linting & Dev Dependencies|Linting & Dev Dependencies]]
- [[_COMMUNITY_Native Bridge & Login|Native Bridge & Login]]
- [[_COMMUNITY_Error Handling & Localization|Error Handling & Localization]]
- [[_COMMUNITY_Theming|Theming]]
- [[_COMMUNITY_App Shell & Controllers|App Shell & Controllers]]
- [[_COMMUNITY_Package Manifest|Package Manifest]]
- [[_COMMUNITY_Server Selection & Loading|Server Selection & Loading]]
- [[_COMMUNITY_Login Layout|Login Layout]]
- [[_COMMUNITY_NPM Scripts|NPM Scripts]]
- [[_COMMUNITY_Session & Device Store|Session & Device Store]]
- [[_COMMUNITY_Menu Item Component|Menu Item Component]]
- [[_COMMUNITY_QR Code Dialog|QR Code Dialog]]
- [[_COMMUNITY_Geofences List|Geofences List]]
- [[_COMMUNITY_Video Stream Page|Video Stream Page]]
- [[_COMMUNITY_Prettier Config|Prettier Config]]
- [[_COMMUNITY_Logs Page|Logs Page]]
- [[_COMMUNITY_Feature Flags|Feature Flags]]
- [[_COMMUNITY_Translation Workflow|Translation Workflow]]

## God Nodes (most connected - your core abstractions)
1. `useTranslation()` - 165 edges
2. `useAsyncTask()` - 61 edges
3. `useCatch()` - 59 edges
4. `useAttributePreference()` - 57 edges
5. `useCatchCallback()` - 41 edges
6. `formatTime()` - 31 edges
7. `toMapCoordinates()` - 27 edges
8. `map` - 26 edges
9. `useRestriction()` - 25 edges
10. `prefixString()` - 24 edges

## Surprising Connections (you probably didn't know these)
- `Simple Demo App (simple/index.html)` --semantically_similar_to--> `Main App index.html`  [INFERRED] [semantically similar]
  simple/index.html → index.html
- `Dependabot Config` --conceptually_related_to--> `Traccar GPS Tracking Platform`  [INFERRED]
  .github/dependabot.yml → README.md
- `Build Project Workflow` --conceptually_related_to--> `Traccar GPS Tracking Platform`  [INFERRED]
  .github/workflows/build.yml → README.md
- `Run Lint Workflow` --conceptually_related_to--> `Traccar GPS Tracking Platform`  [INFERRED]
  .github/workflows/lint.yml → README.md
- `GitHub Funding Config` --conceptually_related_to--> `Traccar Team (Anton Tananaev, Andrey Kunitsyn)`  [INFERRED]
  .github/FUNDING.yml → README.md

## Import Cycles
- 3-file cycle: `src/map/core/MapView.jsx -> src/map/core/preloadImages.js -> src/map/core/mapUtil.js -> src/map/core/MapView.jsx`

## Hyperedges (group relationships)
- **Traccar Web Frontend Tech Stack** — concept_react, concept_material_ui, concept_maplibre, concept_traccar_platform [EXTRACTED 1.00]
- **GitHub Actions CI Workflows** — workflows_build, workflows_lint, workflows_translation [INFERRED 0.85]
- **Simple App API/WebSocket Data Flow** — simple_index_html, concept_traccar_rest_api, concept_websocket_positions, concept_traccar_backend [INFERRED 0.85]

## Communities (31 total, 9 thin omitted)

### Community 0 - "Settings & Device Attributes"
Cohesion: 0.06
Nodes (81): BaseCommandView(), BottomMenu(), CollectionActions(), useStyles, CollectionFab(), useStyles, DeviceUsersValue(), EditItemView() (+73 more)

### Community 1 - "Map Rendering & Controls"
Cohesion: 0.06
Nodes (49): MapGeocoder(), useStyles, MapNotification(), useStyles, MapRuler(), useStyles, MapSwitcher(), useStyles (+41 more)

### Community 2 - "Attribute Editing & Value Formatters"
Cohesion: 0.08
Nodes (48): AddAttributeDialog(), useStyles, EditAttributesAccordion(), MotionBar(), useStyles, PositionValue(), gradientStops, MapSpeedLegend() (+40 more)

### Community 3 - "Reporting & Exports"
Cohesion: 0.11
Nodes (39): AddressValue(), ColumnSelect(), ReportFilter(), updateReportParams(), ResizeHandle(), useStyles, AuditPage(), columnsArray (+31 more)

### Community 4 - "Page Routing & Navigation"
Cohesion: 0.04
Nodes (52): AccumulatorsPage, AnnouncementPage, AuditPage, CalendarPage, CalendarsPage, ChangeServerPage, ChartReportPage, CombinedReportPage (+44 more)

### Community 5 - "Runtime Dependencies"
Cohesion: 0.06
Nodes (34): dependencies, dayjs, @emotion/cache, @emotion/react, @emotion/styled, exceljs, file-saver, gcoord (+26 more)

### Community 6 - "Device Status & Main Panel"
Cohesion: 0.13
Nodes (16): StatusCard(), StatusRow(), useStyles, DeviceList(), useStyles, EventsDrawer(), useStyles, MainMap (+8 more)

### Community 7 - "Redux Store Slices"
Cohesion: 0.11
Nodes (9): { reducer, actions }, { reducer, actions }, { reducer, actions }, { reducer, actions }, { reducer, actions }, { reducer, actions }, reducer, { reducer, actions } (+1 more)

### Community 8 - "Project Stack & Integrations"
Cohesion: 0.17
Nodes (17): MapLibre GL, Material UI, React, Traccar Team (Anton Tananaev, Andrey Kunitsyn), Traccar Backend Server (tananaev/traccar), Traccar GPS Tracking Platform, Traccar REST API, Vite HTML Entry with Template Placeholders (+9 more)

### Community 9 - "Linting & Dev Dependencies"
Cohesion: 0.12
Nodes (17): devDependencies, eslint, eslint-config-prettier, @eslint/js, eslint-plugin-import-x, eslint-plugin-prettier, eslint-plugin-react-hooks, @eslint-react/eslint-plugin (+9 more)

### Community 10 - "Native Bridge & Login"
Cohesion: 0.28
Nodes (9): generateLoginToken(), handleLoginTokenListeners, handleNativeNotificationListeners, NativeInterface(), nativePostMessage(), updateNotificationTokenListeners, LoginPage(), useStyles (+1 more)

### Community 11 - "Error Handling & Localization"
Cohesion: 0.18
Nodes (6): ErrorHandler(), getDefaultLanguage(), LocalizationProvider(), ErrorBoundary, root, usePrevious()

### Community 12 - "Theming"
Cohesion: 0.20
Nodes (5): useLocalization(), theme, AppThemeProvider(), cache, Navigation()

### Community 13 - "App Shell & Controllers"
Cohesion: 0.22
Nodes (5): TermsDialog(), MotionController(), App(), useStyles, UpdateController()

### Community 14 - "Package Manifest"
Cohesion: 0.20
Nodes (9): browserslist, development, production, name, overrides, immer, private, type (+1 more)

### Community 15 - "Server Selection & Loading"
Cohesion: 0.29
Nodes (4): ChangeServerPage(), officialServers, useStyles, ServerProvider()

### Community 16 - "Login Layout"
Cohesion: 0.47
Nodes (4): LoginLayout(), useStyles, LogoImage(), useStyles

### Community 17 - "NPM Scripts"
Cohesion: 0.33
Nodes (6): scripts, build, generate-pwa-assets, lint, lint:fix, start

## Knowledge Gaps
- **165 isolated node(s):** `singleQuote`, `printWidth`, `name`, `version`, `type` (+160 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **9 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `useTranslation()` connect `Settings & Device Attributes` to `Map Rendering & Controls`, `Attribute Editing & Value Formatters`, `Reporting & Exports`, `Device Status & Main Panel`, `Native Bridge & Login`, `Error Handling & Localization`, `App Shell & Controllers`, `Server Selection & Loading`, `QR Code Dialog`, `Video Stream Page`, `Logs Page`?**
  _High betweenness centrality (0.172) - this node is a cross-community bridge._
- **Why does `useAsyncTask()` connect `Settings & Device Attributes` to `Map Rendering & Controls`, `Reporting & Exports`, `Page Routing & Navigation`, `Device Status & Main Panel`, `Native Bridge & Login`, `Theming`, `App Shell & Controllers`, `Server Selection & Loading`?**
  _High betweenness centrality (0.046) - this node is a cross-community bridge._
- **Why does `useAttributePreference()` connect `Map Rendering & Controls` to `Settings & Device Attributes`, `Attribute Editing & Value Formatters`, `Reporting & Exports`, `Device Status & Main Panel`, `Native Bridge & Login`, `App Shell & Controllers`?**
  _High betweenness centrality (0.036) - this node is a cross-community bridge._
- **What connects `singleQuote`, `printWidth`, `name` to the rest of the system?**
  _166 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Settings & Device Attributes` be split into smaller, more focused modules?**
  _Cohesion score 0.05589262732119875 - nodes in this community are weakly interconnected._
- **Should `Map Rendering & Controls` be split into smaller, more focused modules?**
  _Cohesion score 0.06404862085086489 - nodes in this community are weakly interconnected._
- **Should `Attribute Editing & Value Formatters` be split into smaller, more focused modules?**
  _Cohesion score 0.08391608391608392 - nodes in this community are weakly interconnected._