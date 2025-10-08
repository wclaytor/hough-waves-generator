// ...existing code...
# Alpine.js Standalone HTML Application Template

🚀 **Create powerful, reactive web applications in a single HTML file** - perfect for tools, utilities, and applications that need to be easily distributed without servers or build processes.

## 🆕 Latest Update: Dark Mode Standardization

**Version 1.1** - The dark mode toggle has been updated to match our Pine Crop app standard:
- ✨ **New Position**: Moved to top-right corner next to stats for better UX
- 🎨 **Refined Design**: Icon-only button with subtle styling and smooth transitions
- 🌙 **Better Icons**: Separate sun/moon icons with clean Alpine.js `x-show` directives
- 🔧 **Simplified Code**: Streamlined implementation following project standards

This creates a consistent dark mode experience across all our Alpine.js applications!

## ✨ What is this?

This template helps you build modern, reactive web applications using [Alpine.js](https://alpinejs.dev/) and [Tailwind CSS](https://tailwindcss.com/) that work completely offline and can be shared as a single HTML file.

### Perfect for:
- ✅ Internal tools and utilities
- ✅ Data analyzers and converters
- ✅ Offline calculators and forms
- ✅ Prototypes and demos
- ✅ Educational tools
- ✅ Apps you share via email or USB drive

### Not ideal for:
- ❌ Large-scale applications
- ❌ SEO-critical websites
- ❌ Apps needing backend APIs
- ❌ Real-time collaboration apps

## 🚀 Quick Start

### 1. Basic Template with Dark Mode
Copy this starter template and save as an `.html` file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Alpine App</title>
    
    <!-- Alpine.js for reactivity -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        if (typeof tailwind !== 'undefined') {
            tailwind.config = { darkMode: 'class' }
        }
    </script>
    
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    
    <style>
        [x-cloak] { display: none !important; }
        * { transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease; }
    </style>
</head>
<body>
    <div x-data="app()" x-cloak :class="darkMode ? 'dark' : ''" class="min-h-screen bg-gray-50 dark:bg-gray-900 p-6">
        <div class="max-w-4xl mx-auto">
            <!-- Header with Dark Mode Toggle -->
            <header class="bg-white dark:bg-gray-800 rounded-lg shadow p-6 mb-6">
                <div class="flex items-center justify-between">
                    <h1 class="text-3xl font-bold text-gray-900 dark:text-gray-100">My Alpine App</h1>
                    
                    <!-- Dark Mode Toggle (Pine Crop Style) -->
                    <button 
                        @click="toggleDarkMode()"
                        class="p-3 rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-600 dark:text-gray-300 transition-all duration-200 border border-gray-300 dark:border-gray-600"
                        title="Toggle dark mode">
                        <i x-show="!darkMode" class="bi bi-moon text-xl"></i>
                        <i x-show="darkMode" class="bi bi-sun text-xl"></i>
                    </button>
                </div>
            </header>
            
            <!-- Your app content here -->
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
                <p x-text="message" class="text-lg text-gray-900 dark:text-gray-100"></p>
                <button @click="updateMessage()" 
                        class="mt-4 bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition-colors">
                    Click me!
                </button>
            </div>
        </div>
    </div>
    
    <script>
        function app() {
            return {
                message: 'Hello, Alpine.js!',
                darkMode: false,
                
                init() {
                    // Load dark mode preference
                    const saved = localStorage.getItem('app-darkMode');
                    this.darkMode = saved === 'true';
                    this.updateDarkMode();
                },
                
                toggleDarkMode() {
                    this.darkMode = !this.darkMode;
                    this.updateDarkMode();
                    localStorage.setItem('app-darkMode', this.darkMode.toString());
                },
                
                updateDarkMode() {
                    if (this.darkMode) {
                        document.documentElement.classList.add('dark');
                    } else {
                        document.documentElement.classList.remove('dark');
                    }
                },
                
                updateMessage() {
                    this.message = 'You clicked the button! 🎉';
                }
            }
        }
    </script>
</body>
</html>
```

### 2. Save and Test
1. Save the code above as `my-app.html`
2. Double-click the file to open in your browser
3. Click the moon/sun icon to test dark mode!
4. Click the button to see Alpine.js reactivity in action!

## 🌙 Dark Mode Implementation

### Standard Dark Mode Pattern
Following our Pine Crop app standard, all Alpine.js apps should use this dark mode pattern:

```javascript
// State
darkMode: false,

// Initialization
init() {
    const saved = localStorage.getItem('app-darkMode');
    this.darkMode = saved === 'true';
    this.updateDarkMode();
},

// Toggle method
toggleDarkMode() {
    this.darkMode = !this.darkMode;
    this.updateDarkMode();
    localStorage.setItem('app-darkMode', this.darkMode.toString());
},

// Update DOM
updateDarkMode() {
    if (this.darkMode) {
        document.documentElement.classList.add('dark');
    } else {
        document.documentElement.classList.remove('dark');
    }
}
```

### Dark Mode Button HTML
```html
<button 
    @click="toggleDarkMode()"
    class="p-3 rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-600 dark:text-gray-300 transition-all duration-200 border border-gray-300 dark:border-gray-600"
    title="Toggle dark mode">
    <i x-show="!darkMode" class="bi bi-moon text-xl"></i>
    <i x-show="darkMode" class="bi bi-sun text-xl"></i>
</button>
```

## 📚 Documentation

- **[Complete Alpine.js Guide](docs/alpine-guide.md)** - Comprehensive guide with patterns and examples
- **[Copilot Instructions](.github/copilot-instructions.md)** - How GitHub Copilot can help you build Alpine.js apps

## 🎯 Common Use Cases

### Data Analyzer with Dark Mode
Perfect for CSV/JSON analysis tools:
```javascript
function dataAnalyzer() {
    return {
        data: [],
        darkMode: false,
        
        init() {
            this.loadDarkMode();
        },
        
        loadDarkMode() {
            const saved = localStorage.getItem('analyzer-darkMode');
            this.darkMode = saved === 'true';
            this.updateDarkMode();
        },
        
        async handleFileUpload(event) {
            const file = event.target.files[0];
            const text = await file.text();
            this.data = this.parseCSV(text);
        },
        
        get statistics() {
            return {
                total: this.data.length,
                average: this.data.reduce((sum, item) => sum + item.value, 0) / this.data.length
            };
        }
    }
}
```

### Form Builder with Accessibility
Create interactive forms with dark mode support:
```javascript
function formApp() {
    return {
        form: { name: '', email: '' },
        errors: {},
        darkMode: false,
        
        init() {
            this.loadDarkMode();
        },
        
        validate() {
            this.errors = {};
            if (!this.form.name) this.errors.name = 'Name required';
            if (!this.form.email.includes('@')) this.errors.email = 'Valid email required';
            return Object.keys(this.errors).length === 0;
        },
        
        submit() {
            if (this.validate()) {
                alert('Form submitted!');
            }
        }
    }
}
```

## 🎨 Key Features

### Reactive Data Binding
```html
<input x-model="searchTerm" placeholder="Search..." 
       class="bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100">
<p x-text="'You searched for: ' + searchTerm" 
   class="text-gray-700 dark:text-gray-300"></p>
```

### Conditional Display with Dark Mode
```html
<div x-show="isVisible" class="bg-white dark:bg-gray-800">
    This appears conditionally with dark mode support
</div>
<template x-if="user.isAdmin">
    <button class="bg-blue-500 dark:bg-blue-600">Admin Panel</button>
</template>
```

### Lists and Loops
```html
<template x-for="item in filteredItems" :key="item.id">
    <div x-text="item.name" 
         class="p-2 border-b border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-800"></div>
</template>
```

### Event Handling
```html
<button @click="handleClick()" 
        class="bg-blue-500 dark:bg-blue-600 text-white">Click me</button>
<input @keyup.enter="search()" 
       class="bg-white dark:bg-gray-800">
<form @submit.prevent="save()">
```

## 💾 Data Persistence

### Local Storage with Dark Mode
```javascript
function persistentApp() {
    return {
        data: [],
        darkMode: false,
        
        init() {
            const savedData = localStorage.getItem('appData');
            const savedDarkMode = localStorage.getItem('app-darkMode');
            
            if (savedData) this.data = JSON.parse(savedData);
            if (savedDarkMode) {
                this.darkMode = savedDarkMode === 'true';
                this.updateDarkMode();
            }
        },
        
        save() {
            localStorage.setItem('appData', JSON.stringify(this.data));
            localStorage.setItem('app-darkMode', this.darkMode.toString());
        }
    }
}
```

### File Export
```javascript
exportData() {
    const blob = new Blob([JSON.stringify(this.data, null, 2)], 
                         { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'data.json';
    a.click();
}
```

## 🎯 Best Practices

### ✅ Do This
- **Always include dark mode** using our standardized pattern
- Use computed properties for derived data: `get filteredItems() { }`
- Include `x-cloak` to prevent flash of unstyled content
- Use `x-show` for frequently toggled elements
- Always provide `:key` for `x-for` loops
- Add dark mode classes to all UI elements
- Position dark mode toggle in top-right corner

### ❌ Avoid This
- Don't filter/sort data in templates - use computed properties
- Don't use `x-if` for frequently shown/hidden content
- Don't forget error handling for file operations
- Don't use Tailwind classes for modal heights - use inline styles
- Don't forget to add dark mode variants to your styling
- Don't place dark mode toggle in left-side actions (use top-right)

## 📏 File Size Guidelines

- **Target**: Keep HTML + JS under 2000 lines
- **Performance**: Test with 1000+ data items
- **Distribution**: Single file should be under 100KB
- **Compatibility**: Test with `file://` protocol
- **Dark Mode**: Ensure smooth transitions don't impact performance

## 🚀 Distribution

### Share Your App
1. **Email**: Attach the HTML file
2. **USB Drive**: Copy and share
3. **GitHub**: Upload to repository
4. **Company Drive**: Share via internal systems

### Users Just Need To:
1. Save the HTML file
2. Double-click to open in browser
3. Toggle dark mode for accessibility
4. Start using immediately!

## 🔧 Advanced Features

### File Upload Handling with Dark Mode
```html
<label class="flex flex-col items-center justify-center w-full h-32 border-2 border-dashed border-gray-300 dark:border-gray-600 rounded-lg cursor-pointer bg-gray-50 dark:bg-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 transition-colors">
    <input type="file" @change="handleFileUpload($event)" accept=".csv,.json" class="hidden">
    <div class="text-center">
        <i class="bi bi-cloud-upload text-4xl text-gray-400 dark:text-gray-500 mb-3"></i>
        <p class="text-sm text-gray-700 dark:text-gray-300">Click to upload or drag and drop</p>
    </div>
</label>
```

### Modal with Proper Scrolling and Dark Mode
```html
<div x-show="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-8">
    <div class="bg-white dark:bg-gray-800 rounded-lg w-full max-w-4xl transition-colors" style="height: 80vh">
        <div class="p-6 border-b border-gray-200 dark:border-gray-700">
            <h3 class="text-xl font-bold text-gray-900 dark:text-gray-100">Modal Title</h3>
        </div>
        <div class="p-6 overflow-y-scroll" style="height: calc(80vh - 120px)">
            <p class="text-gray-700 dark:text-gray-300">Modal content with dark mode support</p>
        </div>
    </div>
</div>
```

### Copy to Clipboard
```javascript
async copyToClipboard(text) {
    try {
        await navigator.clipboard.writeText(text);
        alert('Copied!');
    } catch (err) {
        // Fallback for older browsers
        const textarea = document.createElement('textarea');
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        alert('Copied!');
    }
}
```

## 🎓 Learning Resources

- **[Alpine.js Documentation](https://alpinejs.dev/)** - Official Alpine.js docs
- **[Tailwind CSS Dark Mode](https://tailwindcss.com/docs/dark-mode)** - Dark mode implementation guide
- **[Bootstrap Icons](https://icons.getbootstrap.com/)** - Icon library
- **[MDN Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)** - Browser APIs reference

## 🤝 Contributing

Have examples or improvements? Contributions welcome!

1. Fork the repository
2. Create your feature branch
3. Add your example or improvement
4. Ensure dark mode compatibility
5. Submit a pull request

## 📄 License

This template is free to use for any purpose. No attribution required.

---

**Happy coding!** 🎉🌙 Start building amazing standalone applications with Alpine.js and accessible dark mode today.