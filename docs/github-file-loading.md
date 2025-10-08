# Manifest-Based File Loading Feature

## Overview

The Alpine.js template now includes a powerful feature to dynamically load and display markdown files using a simple JSON manifest. This allows you to manage content as files in your repository and have them automatically appear in your application. This pattern is inspired by the successful [vegan-campsite-cookbook](https://github.com/wclaytor/vegan-campsite-cookbook) implementation.

## How It Works

### 1. File Discovery via Manifest
The application loads a list of files from `files.json` in the root directory:
```json
[
    "example-01.md",
    "example-02.md",
    "example-03.md"
]
```

### 2. Markdown Processing
When a user clicks on a file:
1. The markdown content is fetched from the `files/` directory
2. The content is parsed using [Marked.js](https://marked.js.org/)
3. The HTML is rendered in a modal with proper styling

### 3. Search and Filter
Users can search through files in real-time with case-insensitive matching.

## File Structure

Place your markdown files in the `files/` directory and list them in `files.json`:
```
alpine-pwa-template/
├── files/
│   ├── example-01.md
│   ├── example-02.md
│   ├── example-03.md
│   └── your-content.md
├── files.json          ← Manifest file
├── index.html
└── README.md
```

### Manifest File (files.json)
```json
[
    "example-01.md",
    "example-02.md",
    "example-03.md",
    "your-content.md"
]
```

## Features

### ✅ Automatic Loading
- Files are loaded automatically when the page initializes
- No manual configuration needed

### ✅ Real-time Search
- Filter files as you type
- Case-insensitive matching
- Instant results

### ✅ Professional UI
- Loading indicators during fetch
- Error handling with retry option
- Responsive design
- Dark mode support

### ✅ Markdown Rendering
- Full markdown support (headers, lists, code blocks, links)
- Syntax highlighting for code
- Responsive content layout
- Styled for both light and dark modes

## Usage

### Adding New Files

1. Create a new markdown file in the `files/` directory
2. Commit and push to GitHub
3. Wait a few minutes for GitHub's CDN to update
4. Refresh your application
5. The new file appears automatically!

### Example Markdown File

```markdown
# My Example Document

## Introduction
This is a simple example document.

## Features
- Feature 1
- Feature 2
- Feature 3

### Code Example
\`\`\`javascript
function hello() {
  console.log("Hello, World!");
}
\`\`\`

## Conclusion
This content is loaded dynamically from GitHub!
```

### Viewing Files

1. Navigate to Section 7: "Project Files from GitHub"
2. Browse the list of available files
3. Click on any file to view its content
4. The file opens in a modal with rendered markdown
5. Click outside the modal or the X button to close

## Technical Details

### State Variables
```javascript
files: [],              // Array of loaded files
loadingFiles: false,    // Loading state indicator
filesError: null,       // Error message if loading fails
selectedFile: null,     // Currently viewed file
showFileModal: false,   // Modal visibility state
fileSearchTerm: ''      // Search filter text
```

### Methods

#### `loadFilesFromGitHub()`
Fetches the list of markdown files from the manifest:
- Loads `files.json` manifest
- Filters for `.md` files only
- Maps to file objects with path and id
- Handles errors gracefully with fallback list

#### `viewFile(file)`
Downloads and renders a specific file:
- Fetches markdown content from `files/` directory
- Converts to HTML using Marked.js
- Opens in a modal viewer

#### `filteredFiles` (computed)
Returns filtered file list based on search term.

## Customization

### Adding New Files
To add new content files:

1. Create your markdown file in the `files/` directory
2. Add the filename to `files.json`:
```json
[
    "example-01.md",
    "example-02.md",
    "example-03.md",
    "my-new-file.md"
]
```
3. That's it! The file will appear automatically

### Change Directory
To load from a different directory, update the path mapping:
```javascript
this.files = fileList.map(filename => ({
    name: filename,
    path: `docs/${filename}`,  // Changed from files/ to docs/
    id: filename.replace('.md', '')
}));
```

### Add File Type Filters
Currently filters for `.md` files. To add more types:
```javascript
this.files = data
  .filter(file => 
    file.name.endsWith('.md') || 
    file.name.endsWith('.txt')
  )
  .map(file => ({...}));
```

### Custom Styling
The markdown is rendered with Tailwind's prose classes. Customize in the modal:
```html
<div class="prose prose-sm max-w-none 
            prose-headings:text-gray-800
            prose-p:text-gray-700
            ...">
```

## Use Cases

### 📚 Documentation Site
- Manage docs as markdown files
- Easy updates via GitHub
- No build process needed

### 📖 Blog or Articles
- Write posts in markdown
- Publish by committing
- Automatic listing and viewing

### 🍳 Recipe Collection
- Each recipe as a markdown file
- Searchable and filterable
- Easy to share and version

### 📝 Knowledge Base
- Internal documentation
- Team resources
- FAQ and guides

### 🎓 Educational Content
- Lessons and tutorials
- Reference materials
- Student resources

## Benefits

### For Users
- ✅ No need to edit HTML
- ✅ Version control for content
- ✅ Easy collaboration via GitHub
- ✅ Works offline (after initial load)

### For Developers
- ✅ Clean separation of content and code
- ✅ Standard markdown format
- ✅ No database required
- ✅ No server needed
- ✅ Free hosting with GitHub Pages

## Performance Considerations

The manifest-based approach is highly efficient:
- **No API rate limits**: Files loaded directly from your repository
- **Simple caching**: Browser caches files automatically
- **Fast loading**: No external API calls required
- **Offline-capable**: Works via file:// protocol after initial load

For production use:
1. Files are cached by the browser automatically
2. Use localStorage to cache the manifest if desired
3. Consider lazy loading for very large file collections

## Browser Compatibility

Works in all modern browsers:
- ✅ Chrome/Edge (90+)
- ✅ Firefox (88+)
- ✅ Safari (14+)
- ✅ Mobile browsers

## Troubleshooting

### Files Not Loading
- Check GitHub API rate limits
- Verify repository is public
- Ensure files are in correct directory
- Check browser console for errors

### Markdown Not Rendering
- Verify Marked.js CDN is loaded
- Check for JavaScript errors
- Ensure modal is displaying

### Search Not Working
- Verify `x-model` is on search input
- Check `filteredFiles` computed property
- Confirm Alpine.js is loaded

## Examples

See the example files in the `files/` directory:
- `example-01.md` - Basic markdown structure
- `example-02.md` - Alpine.js guide
- `example-03.md` - To-do app tutorial

## Credits

This feature was inspired by the [Vegan Campsite Cookbook](https://github.com/wclaytor/vegan-campsite-cookbook) project, which successfully uses this pattern for recipe management.

---

*This feature demonstrates the power of Alpine.js for creating dynamic, data-driven applications without complex build tools or backends.*
