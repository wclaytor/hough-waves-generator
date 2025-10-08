# GitHub File Loading Feature - Architecture Diagram

## Data Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                     Alpine.js Application                        │
│                                                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  init() Lifecycle                                        │   │
│  │  └─> loadFilesFromGitHub()                              │   │
│  └──────────────────────┬──────────────────────────────────┘   │
│                          │                                       │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Manifest Request                                         │  │
│  │  GET files.json                                           │  │
│  │  Returns: ["example-01.md", "example-02.md", ...]        │  │
│  └──────────────────────┬───────────────────────────────────┘  │
│                          │                                       │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Response Processing                                      │  │
│  │  • Filter for .md files                                   │  │
│  │  • Map to simplified structure                            │  │
│  │  • Store in files[] array                                 │  │
│  └──────────────────────┬───────────────────────────────────┘  │
│                          │                                       │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  UI Rendering                                             │  │
│  │  • Display file list                                      │  │
│  │  • Enable search/filter                                   │  │
│  │  • Show loading states                                    │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘

                              USER CLICKS FILE
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────┐
│                     viewFile(file)                               │
│                                                                   │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Fetch File Content                                       │  │
│  │  GET files/{filename}                                     │  │
│  └──────────────────────┬───────────────────────────────────┘  │
│                          │                                       │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Markdown Processing                                      │  │
│  │  • Parse with marked.js                                   │  │
│  │  • Convert to HTML                                        │  │
│  │  • Store in selectedFile                                  │  │
│  └──────────────────────┬───────────────────────────────────┘  │
│                          │                                       │
│                          ▼                                       │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Modal Display                                            │  │
│  │  • Show file name                                         │  │
│  │  • Render HTML content                                    │  │
│  │  • Apply prose styling                                    │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

## Component Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    starterApp() Component                        │
├─────────────────────────────────────────────────────────────────┤
│  STATE                                                           │
│  ├─ files: []           ← List of markdown files                │
│  ├─ loadingFiles: false ← Loading indicator                     │
│  ├─ filesError: null    ← Error messages                        │
│  ├─ selectedFile: null  ← Currently viewed file                 │
│  ├─ showFileModal: false ← Modal visibility                     │
│  └─ fileSearchTerm: ''  ← Search filter                         │
├─────────────────────────────────────────────────────────────────┤
│  COMPUTED PROPERTIES                                             │
│  └─ get filteredFiles() ← Search-filtered file list             │
├─────────────────────────────────────────────────────────────────┤
│  METHODS                                                         │
│  ├─ loadFilesFromGitHub() ← Fetch file list from API           │
│  └─ viewFile(file)         ← Load and display file content     │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    UI Components                                 │
├─────────────────────────────────────────────────────────────────┤
│  Section 7: Project Files                                       │
│  ├─ Search Input (x-model="fileSearchTerm")                    │
│  ├─ Loading State (x-show="loadingFiles")                      │
│  ├─ Error State (x-show="filesError")                          │
│  ├─ File List (x-for="file in filteredFiles")                  │
│  └─ Refresh Button (@click="loadFilesFromGitHub()")            │
├─────────────────────────────────────────────────────────────────┤
│  File Viewer Modal                                              │
│  ├─ Header (File name + close button)                          │
│  ├─ Content (x-html="selectedFile?.html")                      │
│  └─ Styling (Tailwind prose classes)                           │
└─────────────────────────────────────────────────────────────────┘
```

## State Lifecycle

```
┌──────────┐
│  INIT    │  Page loads
└────┬─────┘
     │
     ▼
┌─────────────────┐
│  LOADING FILES  │  loadingFiles = true
└────┬────────────┘
     │
     ▼
┌─────────────────┐
│  API REQUEST    │  Fetch from GitHub
└────┬────────────┘
     │
     ├──SUCCESS──┐
     │           ▼
     │      ┌─────────────────┐
     │      │  FILES LOADED   │  files = [...], loadingFiles = false
     │      └─────────────────┘
     │
     └──ERROR────┐
                 ▼
            ┌─────────────────┐
            │  ERROR STATE    │  filesError = message, loadingFiles = false
            └─────────────────┘


USER INTERACTION
─────────────────

┌──────────────┐
│  CLICK FILE  │
└──────┬───────┘
       │
       ▼
┌──────────────────┐
│  LOADING CONTENT │  loadingFiles = true
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  FETCH MARKDOWN  │
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  PARSE TO HTML   │  marked.parse()
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  SHOW MODAL      │  showFileModal = true, selectedFile = {...}
└──────────────────┘
```

## Integration Points

```
┌────────────────────────────────────────────────────────────────┐
│  External Dependencies                                          │
├────────────────────────────────────────────────────────────────┤
│  • Alpine.js 3.x    → Reactivity and component logic           │
│  • Marked.js 11.x   → Markdown to HTML conversion              │
│  • Tailwind CSS     → Styling and responsive design            │
│  • Bootstrap Icons  → UI icons                                 │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│  Repository Structure                                           │
├────────────────────────────────────────────────────────────────┤
│  /files/              ← Markdown files stored here             │
│  │  ├─ example-01.md                                           │
│  │  ├─ example-02.md                                           │
│  │  └─ example-03.md                                           │
│  /files.json          ← Manifest file listing all files        │
│  /index.html          ← Main application file                  │
│  /docs/               ← Documentation                           │
│  │  └─ github-file-loading.md                                  │
└────────────────────────────────────────────────────────────────┘
```

## Error Handling Flow

```
                    ┌─────────────────┐
                    │  API REQUEST    │
                    └────┬────────────┘
                         │
          ┌──────────────┴──────────────┐
          │                             │
          ▼                             ▼
    ┌─────────┐                   ┌─────────┐
    │ SUCCESS │                   │  ERROR  │
    └────┬────┘                   └────┬────┘
         │                             │
         ▼                             ▼
    ┌──────────────┐            ┌───────────────┐
    │ Display Files│            │ Show Error UI │
    └──────────────┘            └───────┬───────┘
                                        │
                                        ▼
                                ┌───────────────┐
                                │ Retry Button  │
                                └───────┬───────┘
                                        │
                                        ▼
                                ┌───────────────┐
                                │ Try Again     │
                                └───────────────┘
```

## Performance Considerations

```
┌────────────────────────────────────────────────────────────────┐
│  Optimization Strategy                                          │
├────────────────────────────────────────────────────────────────┤
│  1. Lazy Loading         → Files loaded only when clicked      │
│  2. Computed Properties  → Search filtering is reactive        │
│  3. Browser Caching      → Files cached automatically          │
│  4. Client-side Parse    → No server processing needed         │
│  5. Modal Reuse          → Single modal for all files          │
│  6. Manifest Pattern     → Inspired by recipe site success     │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│  Performance Benefits                                            │
├────────────────────────────────────────────────────────────────┤
│  • No API Rate Limits:  Direct file loading from repository    │
│  • Fast Response:        No external API calls required         │
│  • Offline Capable:      Works via file:// protocol            │
│  • Simple Management:    Just update files.json manifest        │
└────────────────────────────────────────────────────────────────┘
```

---

*This diagram illustrates the complete architecture of the GitHub file loading feature, showing data flow, component structure, state management, and integration points.*
