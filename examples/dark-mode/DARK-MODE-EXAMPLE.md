# 🌙 Dark Mode Example - Alpine.js Template

This example demonstrates how to implement a comprehensive, accessibility-focused dark mode feature using Alpine.js and Tailwind CSS.

## 🎯 What You'll Learn

- **System Preference Detection**: Automatically detect and respect user's system theme preference
- **Manual Toggle**: Provide users with manual control over theme switching
- **LocalStorage Persistence**: Save user preferences across browser sessions
- **Smooth Transitions**: Implement professional-grade theme transitions
- **Accessibility**: Follow WCAG guidelines for accessible theme switching
- **Component Examples**: See how different UI components adapt to themes

## 🚀 Quick Start

1. Open `dark-mode-example.html` in your browser
2. Click the moon/sun icon to toggle between light and dark themes
3. Try the "Detect System Preference" button to sync with your OS theme
4. Explore the interactive examples and code documentation

## 📋 Features Demonstrated

### 1. Basic Dark Mode Toggle
- Simple boolean state management
- CSS class conditional binding
- Icon state switching

### 2. System Preference Detection
- `window.matchMedia('(prefers-color-scheme: dark)')` API usage
- Event listeners for system theme changes
- Automatic theme synchronization

### 3. LocalStorage Persistence
- Save user theme preference
- Load saved preferences on page initialization
- Handle cases where no preference is saved

### 4. Smooth Transitions
- CSS transitions for theme switching
- Configurable transition speeds
- Professional visual feedback

### 5. UI Component Examples
- Form elements (inputs, selects, textareas)
- Buttons in different styles
- Cards and containers
- Proper color contrast in both themes

### 6. Accessibility Best Practices
- Proper ARIA labels on toggle buttons
- Keyboard navigation support
- Screen reader compatibility
- Color contrast compliance

## 🔧 Implementation Details

### Core JavaScript Function

```javascript
function darkModeApp() {
    return {
        darkMode: false,
        systemPreference: 'unknown',
        supportsDarkMode: false,
        
        init() {
            this.detectSystemPreference();
            this.loadSavedPreference();
            this.updateDarkMode();
        },
        
        toggleDarkMode() {
            this.darkMode = !this.darkMode;
            this.updateDarkMode();
            this.savePreference();
        },
        
        updateDarkMode() {
            if (this.darkMode) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        },
        
        detectSystemPreference() {
            if (window.matchMedia) {
                const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
                this.systemPreference = mediaQuery.matches ? 'dark' : 'light';
                this.darkMode = mediaQuery.matches;
            }
        },
        
        savePreference() {
            localStorage.setItem('darkMode', this.darkMode.toString());
        },
        
        loadSavedPreference() {
            const saved = localStorage.getItem('darkMode');
            if (saved !== null) {
                this.darkMode = saved === 'true';
            }
        }
    }
}
```

### HTML Structure

```html
<div x-data="darkModeApp()" 
     x-cloak 
     :class="darkMode ? 'dark' : ''" 
     class="min-h-screen bg-gray-50 dark:bg-gray-900">
     
  <button @click="toggleDarkMode()"
          :aria-label="darkMode ? 'Switch to light mode' : 'Switch to dark mode'"
          class="p-3 rounded-lg bg-gray-100 dark:bg-gray-700">
    <i x-show="!darkMode" class="bi bi-moon"></i>
    <i x-show="darkMode" class="bi bi-sun"></i>
  </button>
  
  <!-- Your themed content -->
  <div class="bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100">
    Content that adapts to theme
  </div>
</div>
```

### CSS Configuration

```css
/* Tailwind Configuration */
tailwind.config = {
    darkMode: 'class'
}

/* Smooth transitions */
* {
    transition: background-color 0.3s ease, 
                border-color 0.3s ease, 
                color 0.3s ease;
}

/* Prevent flash of unstyled content */
[x-cloak] { 
    display: none !important; 
}
```

## 🎨 Styling Patterns

### Common Dark Mode Classes

| Element | Light Theme | Dark Theme |
|---------|-------------|------------|
| Background | `bg-white` | `dark:bg-gray-800` |
| Text | `text-gray-900` | `dark:text-gray-100` |
| Secondary Text | `text-gray-600` | `dark:text-gray-400` |
| Borders | `border-gray-300` | `dark:border-gray-600` |
| Inputs | `bg-white border-gray-300` | `dark:bg-gray-700 dark:border-gray-600` |

### Transition Classes

```css
.theme-transition {
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
```

## ✅ Accessibility Checklist

- [x] Respects system color scheme preference
- [x] Provides manual override option
- [x] Uses proper ARIA labels
- [x] Maintains color contrast ratios (4.5:1 minimum)
- [x] Persists user preference
- [x] Smooth transitions (not too fast for users with vestibular disorders)
- [x] Keyboard navigation support
- [x] Screen reader compatibility

## 🔗 Integration with Your Project

To add dark mode to your Alpine.js project:

1. **Copy the JavaScript function** and customize the state variables
2. **Add the HTML structure** with proper Alpine.js directives
3. **Include the CSS transitions** for smooth theme switching
4. **Configure Tailwind** with `darkMode: 'class'`
5. **Add dark mode classes** to your existing components
6. **Test accessibility** with screen readers and keyboard navigation

## 🚀 Advanced Features

The example also demonstrates:
- Dynamic transition speed adjustment
- Real-time system preference monitoring
- Modal with scrollable content and proper dark mode styling
- Code syntax highlighting in both themes
- Interactive live demos
- Comprehensive implementation documentation

## 🔍 Browser Support

- **Modern Browsers**: Full support including system preference detection
- **Older Browsers**: Graceful degradation with manual toggle only
- **Mobile**: Responsive design that works on all screen sizes

---

**💡 Pro Tip**: This example follows the same patterns used in the main `index.html` file, making it easy to understand and integrate into your existing Alpine.js applications.