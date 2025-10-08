# AGENTS.md

## Project Overview

This repository provides a comprehensive template and methodology for creating modern Alpine.js standalone HTML applications using a professional role-based development approach. When working on issues, adopt the appropriate role perspective(s) based on the ticket type and requirements.

## Role-Based Development System

This project uses five specialized roles that collaborate to ensure comprehensive, high-quality Alpine.js applications:

### 🎯 Product-Owner Role (Strategy & Vision)
**When to adopt**: Requirements clarification, feature prioritization, user story definition
- Define user value and business impact
- Create acceptance criteria and success metrics
- Prioritize features based on user needs
- **Reference**: [Product-Owner Role Definition](./.github/roles/Product-Owner.md)

### 🏗️ Architect Role (Technical Blueprint)
**When to adopt**: System design, technology decisions, performance requirements
- Design technical architecture and patterns
- Make technology stack decisions with justification
- Define performance and scalability requirements
- **Reference**: [Architect Role Definition](./.github/roles/Architect.md)

### 🎨 Designer Role (User Experience)
**When to adopt**: UI/UX issues, accessibility requirements, responsive design
- Create UI/UX specifications and design system
- Ensure accessibility compliance (WCAG 2.1 AA)
- Define responsive design patterns
- **Reference**: [Designer Role Definition](./.github/roles/Designer.md)

### 💻 Developer Role (Implementation)
**When to adopt**: Code implementation, Alpine.js patterns, bug fixes
- Implement Alpine.js reactive patterns
- Follow established coding standards
- Optimize performance and handle errors
- **Reference**: [Developer Role Definition](./.github/roles/Developer.md)

### 🧪 QA-Engineer Role (Quality Assurance)
**When to adopt**: Testing requirements, quality validation, cross-browser compatibility
- Create comprehensive test strategies
- Validate accessibility and performance
- Ensure cross-browser compatibility
- **Reference**: [QA-Engineer Role Definition](./.github/roles/QA-Engineer.md)

## Role Selection Guidelines

### Single Role Issues:
- **Bug Reports** → Developer Role
- **UI/UX Issues** → Designer Role  
- **Performance Issues** → Architect Role
- **Feature Requests** → Product-Owner Role
- **Testing Issues** → QA-Engineer Role

### Multi-Role Issues (Use collaboration pattern):
- **New Features** → Product-Owner → Architect → Designer → Developer → QA-Engineer
- **Architecture Changes** → Architect → Developer → QA-Engineer
- **User Experience Improvements** → Product-Owner → Designer → QA-Engineer
- **Performance Optimization** → Architect → Developer → QA-Engineer

## Alpine.js Development Standards

### Core Template Structure
Always start standalone applications with this proven pattern:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[App Name]</title>
    
    <!-- Alpine.js for reactivity -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    
    <style>
        [x-cloak] { display: none !important; }
    </style>
</head>
<body>
    <div x-data="app()" x-cloak class="min-h-screen bg-gray-50 p-6">
        <!-- App content here -->
    </div>
    
    <script>
        function app() {
            return {
                // State and methods
            }
        }
    </script>
</body>
</html>
```

### Critical Implementation Rules
1. **Modal Heights**: ALWAYS use inline styles for modal dimensions (`style="height: 80vh"`)
2. **x-cloak**: Always include to prevent flash of unstyled content
3. **Computed Properties**: Use getters for reactive derived data (`get filteredData() {}`)
4. **Event Handlers**: Use Alpine syntax (`@click`, not `onclick`)
5. **Scrollable Content**: Use `overflow-y-scroll` not `overflow-y-auto`
6. **Performance**: Use `x-show` for frequent toggles, `x-if` for rare conditions
7. **Keys in Loops**: Always use `:key` in `x-for` loops

### State Management Pattern
```javascript
function app() {
    return {
        // === STATE ===
        data: [],
        searchTerm: '',
        loading: false,
        
        // === COMPUTED PROPERTIES ===
        get filteredData() {
            return this.data.filter(item => 
                item.name.toLowerCase().includes(this.searchTerm.toLowerCase())
            );
        },
        
        // === LIFECYCLE ===
        init() {
            this.loadData();
        },
        
        // === METHODS ===
        async loadData() {
            this.loading = true;
            // Implementation
            this.loading = false;
        }
    }
}
```

## Quality Standards

### Technical Requirements
- ✅ Single HTML file under 100KB
- ✅ Works with `file://` protocol (offline)
- ✅ Responsive design for all screen sizes
- ✅ WCAG 2.1 AA accessibility compliance
- ✅ Fast performance with 1000+ data items
- ✅ Cross-browser compatibility (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

### Code Quality Requirements
- ✅ Clean, readable Alpine.js patterns
- ✅ Proper error handling and fallbacks
- ✅ Comprehensive inline documentation
- ✅ Performance optimization (debounced search, efficient filtering)
- ✅ Progressive enhancement principles

## Testing Instructions

### Manual Testing Checklist
- [ ] Save HTML file and test via `file://` protocol
- [ ] Test on mobile devices (iOS Safari, Android Chrome)
- [ ] Validate keyboard navigation and screen reader compatibility
- [ ] Test with large datasets (100+ items)
- [ ] Verify offline functionality after initial load
- [ ] Test in all supported browsers

### Performance Validation
- [ ] Initial load under 2 seconds on 3G
- [ ] Search/filter response under 100ms
- [ ] Modal open/close under 150ms
- [ ] Memory usage stable during extended use

### Accessibility Validation
- [ ] All interactive elements have proper ARIA labels
- [ ] Color contrast meets WCAG 2.1 AA standards (4.5:1 minimum)
- [ ] Full keyboard navigation support
- [ ] Screen reader compatibility verified

## Development Workflow

### Issue Analysis Process
1. **Read the issue carefully** - Understand user needs and technical requirements
2. **Identify role perspective(s)** - Determine which role(s) should lead the response
3. **Check existing patterns** - Reference role documentation and established patterns
4. **Plan the solution** - Consider impact on architecture, design, implementation, and quality
5. **Implement comprehensively** - Address all aspects from relevant role perspectives

### Implementation Standards
- **Single File Architecture**: All functionality in one HTML file
- **CDN Dependencies**: Use Alpine.js, Tailwind CSS, and Bootstrap Icons via CDN
- **Progressive Enhancement**: Core functionality works without JavaScript
- **Error Resilience**: Graceful handling of all failure scenarios
- **Mobile-First**: Optimize for mobile devices and touch interactions

### Documentation Requirements
- **Inline Comments**: Explain complex Alpine.js patterns and business logic
- **README Updates**: Update documentation for new features or patterns
- **Example Code**: Provide working examples for new functionality
- **Role Rationale**: Document which roles influenced the solution and why

## Common Application Patterns

### Data Analyzer Pattern
File upload → Process → Display table → Export
```javascript
// Product-Owner: User workflow requirements
// Architect: Data processing strategy  
// Designer: Table and filter UI
// Developer: Alpine.js reactive implementation
// QA-Engineer: Data validation and edge cases
```

### Converter Tool Pattern
Input → Transform → Preview → Download
```javascript
// Product-Owner: Conversion requirements and formats
// Architect: Processing pipeline design
// Designer: Input/output interface design
// Developer: Transformation logic implementation  
// QA-Engineer: Format validation and error handling
```

### Dashboard Pattern
Load data → Filter → Visualize → Interact
```javascript
// Product-Owner: Dashboard requirements and KPIs
// Architect: Data architecture and performance
// Designer: Chart layouts and responsive design
// Developer: Alpine.js reactive charts and filters
// QA-Engineer: Cross-browser compatibility and performance
```

## PR Instructions

### Title Format
- `[ROLE] Brief description` (e.g., `[Developer] Fix search filtering performance`)
- `[Multi-Role] Brief description` for complex features

### PR Description Template
```markdown
## Role Perspective(s)
- [ ] Product-Owner: [If applicable, describe user value and acceptance criteria]
- [ ] Architect: [If applicable, describe technical approach and performance implications]
- [ ] Designer: [If applicable, describe UI/UX changes and accessibility considerations] 
- [ ] Developer: [Describe implementation approach and Alpine.js patterns used]
- [ ] QA-Engineer: [Describe testing approach and quality validation]

## Changes Made
- [List specific changes]

## Testing Completed
- [ ] Manual testing on desktop and mobile
- [ ] Accessibility validation
- [ ] Performance testing with large datasets
- [ ] Cross-browser compatibility check
- [ ] Offline functionality verification

## Quality Checklist
- [ ] Follows Alpine.js best practices
- [ ] Maintains single-file architecture
- [ ] Includes proper error handling
- [ ] Performance optimized
- [ ] Accessibility compliant
```

### Pre-commit Checklist
- [ ] Code follows Alpine.js patterns and project standards
- [ ] All critical implementation rules followed (modal heights, x-cloak, etc.)
- [ ] Performance tested with realistic data volumes
- [ ] Accessibility requirements met
- [ ] Cross-browser compatibility verified
- [ ] Documentation updated as needed

## Additional Resources

- **[Role Collaboration Guide](./docs/guides/Roles.md)** - How roles work together effectively
- **[Copilot Role Usage Guide](./docs/guides/Roles-Copilot.md)** - AI-specific role implementation patterns
- **[Complete Alpine.js Guide](./docs/alpine-guide.md)** - Comprehensive patterns and examples
- **[Project README](./README.md)** - Quick start and basic usage

---

**Remember**: This role-based approach ensures comprehensive solutions that consider business value, technical excellence, user experience, implementation quality, and thorough validation. Always adopt the appropriate role perspective(s) for the issue at hand.