# AGENTS.md - Hough Waves Project

## Project Overview

**Hough Waves** is an algorithmic art generator that transforms mathematical algorithms into stunning visual art using the Hough Transform from computer vision. This single-page Alpine.js application creates beautiful, wave-like patterns through the elegant interplay of geometry, voting systems, and emergent complexity.

### Project Type
- **Application**: Generative art tool / Educational visualization
- **Architecture**: Alpine.js standalone HTML (single file, 24KB)
- **Primary Use**: Creating and exploring algorithmic art based on the Hough Transform
- **Target Users**: Artists, educators, students, algorithm enthusiasts

### Core Features
- 🎨 Five pattern types (Wave, Spiral, Circle, Grid, Random)
- 🌈 Five color modes (Monochrome, Rainbow, Gradient, Ocean, Fire)
- 🎛️ Interactive controls with real-time visualization
- 🔧 Advanced optimization options for algorithm exploration
- 🌓 Dark mode with LocalStorage persistence
- 📥 PNG export functionality
- 📱 PWA-ready with offline support

## The Hough Transform Algorithm

### Mathematical Foundation
The Hough Transform is a feature extraction technique from computer vision that detects geometric shapes. In Hough Waves, we use it artistically:

**Core Principle**: A line in (x, y) space is represented in polar coordinates as:
```
r = x·cos(θ) + y·sin(θ)
```
Where:
- `θ` (theta) is the angle from the x-axis (-90° to +90°)
- `r` (rho) is the perpendicular distance from the origin

**Key Insight**: Each point in image space generates a **sinusoidal curve** in parameter space (θ, r). When multiple points lie on the same line, their sinusoids intersect at a common (θ, r) point.

### Algorithm Steps (Implemented in `computeHoughTransform`)
1. **Generate Points**: Create point distributions based on pattern type
2. **Vote in Parameter Space**: For each point, vary θ from -90° to +90°:
   - Calculate r = x·cos(θ) + y·sin(θ)
   - Quantize (θ, r) into bins
   - Cast a vote in the accumulator
3. **Accumulate Votes**: Build a vote map in parameter space
4. **Detect Lines**: Find (θ, r) pairs that exceed the threshold
5. **Render**: Draw detected lines on canvas

### Optimization Strategies (Critical Understanding)

**Problem**: Fine-grained binning (1° theta, 2px rho) causes vote fragmentation. With 50 points generating ~180 votes each (9,050 total), votes scatter across thousands of bins, making it hard for any single bin to exceed threshold >12.

**Three Solutions**:

1. **Coarse Binning** 🔵
   - Groups similar lines together
   - Larger bins (5° theta, 10px rho) = more votes per bin
   - Implementation: `Math.round(thetaDeg / thetaBinSize) * thetaBinSize`

2. **Dynamic Threshold** 🟣
   - Auto-scales threshold with point count
   - Formula: `threshold = points × multiplier`
   - Ensures consistent results across different point counts

3. **Vote Blurring** 🟢
   - Spreads each vote to neighboring bins
   - Uses Gaussian weighting: `weight = exp(-distance² / (2·radius²)) · 0.5`
   - Helps similar lines accumulate votes

### Pattern Generation (`createPoints` method)
Each pattern creates specific point distributions:
- **Wave**: `y = height/2 + sin(x·4π)·150` with noise
- **Spiral**: `r = progress·400, angle = progress·6π`
- **Circle**: Points on circle with `angle = i·2π/n`
- **Grid**: Regular grid `cols = ceil(sqrt(n))`
- **Random**: Uniform random distribution

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

## Hough Waves Control Documentation

### Basic Controls (User-Facing)

#### Pattern Type
Determines spatial distribution of initial points:
- **Wave**: Sinusoidal curve → flowing organic patterns
- **Spiral**: Expanding vortex → radial symmetry
- **Circle**: Ring arrangement → mandala designs
- **Grid**: Regular grid → geometric networks
- **Random**: Scattered → constellation patterns

#### Points (10-150)
- Controls point density
- More points = more potential lines + more vote fragmentation
- Typical: 40-80 for balanced complexity

#### Threshold (5-50 votes)
- Minimum votes required for line to be drawn
- **Critical parameter**: "confidence level" for line detection
- Low (5-15): Many lines, artistic chaos
- High (25-50): Only strongest alignments, geometric precision

#### Resolution (0.5°-5° theta step)
- Angular sampling frequency
- Fine (0.5-1°): Smooth curves, more computation
- Coarse (3-5°): Faster, more artistic variation
- **Trade-off**: Precision vs. performance vs. vote density

#### Opacity (1%-100%)
- Line transparency
- Low (1-5%): Ethereal layered effects
- High (60-100%): Bold graphic art
- **Pro tip**: Lower opacity with lower threshold (more lines)

#### Color Mode
- Monochrome: White/black based on theme
- Rainbow: HSL spectrum (0-360°)
- Gradient: Purple-to-pink transition
- Ocean: Blue-teal (180-240° hue)
- Fire: Red-orange-yellow (0-60° hue)

### Advanced Options (Algorithm Tuning)

#### Coarse Binning (🔵)
- **Theta Bin Size** (1-10°): Angle grouping tolerance
- **Rho Bin Size** (2-20px): Distance grouping tolerance
- **When to use**: High threshold producing no lines
- **Effect**: Accumulates more votes per bin

#### Dynamic Threshold (🟣)
- **Multiplier** (5-50%): Percentage of points
- **Formula**: `threshold = floor(points × multiplier)`
- **When to use**: Want consistent results across point counts
- **Effect**: Auto-adjusts as point count changes

#### Vote Blurring (🟢)
- **Blur Radius** (1-5 bins): Gaussian spread distance
- **When to use**: Lines appear fragmented
- **Effect**: Votes spread to neighbors, smoother detection

### Control Interactions
- **Dense patterns**: High points + Low threshold + Low opacity
- **Geometric art**: Medium points + High threshold + High opacity
- **Performance**: Lower resolution + Coarse binning = faster
- **Algorithm exploration**: Enable all optimizations + vary parameters

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

## Hough Waves Codebase Structure

### Key Functions (All in `houghWaves()` Alpine component)

**State Management**:
```javascript
// Basic parameters
numPoints: 50          // Point count
threshold: 15          // Vote threshold
pattern: 'wave'        // Pattern type
opacity: 0.05          // Line opacity
colorMode: 'mono'      // Color scheme
thetaStep: 1          // Angular resolution

// Optimization options
useCoarseBinning: false
thetaBinSize: 1       // Coarse binning theta size
rhoBinSize: 2         // Coarse binning rho size
useDynamicThreshold: false
thresholdMultiplier: 0.2
useBlurring: false
blurRadius: 0.1
```

**Core Methods**:
- `init()`: Initialize canvas, load preferences, generate first pattern
- `generate()`: Main flow - clear → createPoints → computeHoughTransform → render
- `createPoints()`: Generate point patterns (wave/spiral/circle/grid/random)
- `computeHoughTransform(points)`: **CRITICAL** - Implements voting algorithm
- `render()`: Draw all detected lines with current opacity/color
- `drawLine(theta, rho, color, strength)`: Draw single line in polar coords
- `getColor(index, total)`: Color mode logic
- `randomize()`: Random parameter exploration

### Critical Implementation Details

**computeHoughTransform - The Heart of the Algorithm**:
```javascript
// For each point
points.forEach(point => {
    // Vary theta from -90° to +90° in steps of thetaStep
    for (let thetaDeg = -90; thetaDeg <= 90; thetaDeg += this.thetaStep) {
        const theta = thetaDeg * Math.PI / 180;
        
        // Calculate rho using polar line equation
        const rho = point.x * Math.cos(theta) + point.y * Math.sin(theta);
        
        // Quantize for binning (with optimization support)
        const thetaKey = Math.round(thetaDeg / thetaBinSize) * thetaBinSize;
        const rhoKey = Math.round(rho / rhoBinSize) * rhoBinSize;
        
        // Vote in accumulator
        castVote(thetaKey, rhoKey, 1.0);
        
        // Optional: Blur votes to neighbors
        if (useBlurring) { /* spread votes */ }
    }
});
```

**Drawing Lines from Polar Coordinates**:
```javascript
// Convert polar (theta, rho) to Cartesian endpoints
const cos = Math.cos(theta);
const sin = Math.sin(theta);
let x0 = cos * rho;
let y0 = sin * rho;

// Extend line across canvas (±1000 units perpendicular to normal)
let x1 = x0 - sin * 1000;
let y1 = y0 + cos * 1000;
let x2 = x0 + sin * 1000;
let y2 = y0 - cos * 1000;
```

## Development History & Lessons Learned

### Phase 1: Initial Implementation (PR #2)
- Created from Alpine.js template
- Implemented 5 patterns, 5 color modes
- **Issue**: Used pair-wise point voting (wrong algorithm)
- Result: Interesting but not wave-like patterns

### Phase 2: Algorithm Correction
- **Discovery**: Wasn't producing smooth waves like reference image
- **Root Cause**: Should vote for all lines through EACH point, not pairs
- **Fix**: Implemented true sinusoidal voting in parameter space
- Result: Beautiful wave patterns emerged ✨

### Phase 3: Threshold Problem
- **Issue**: Threshold >12 produced no visible lines
- **Analysis**: Vote fragmentation due to fine binning
- **Solution**: Three-pronged optimization framework
- Result: Full parameter space exploration enabled 🎛️

### Key Lessons for Agents

1. **Algorithm Accuracy Matters**: Small implementation differences dramatically affect output
2. **Vote Accumulation**: Fine binning spreads votes thin - consider accumulation strategies
3. **User Control**: Advanced options should be optional but available
4. **Visual Feedback**: Real-time updates essential for parameter exploration
5. **Documentation**: Complex algorithms need thorough explanation

## Common Application Patterns

### Algorithmic Art Generator Pattern (This Project)
Generate → Transform → Accumulate → Detect → Render
```javascript
// Product-Owner: Artistic exploration and educational value
// Architect: Algorithm correctness and optimization strategies
// Designer: Control layout and real-time feedback UX
// Developer: Canvas rendering and Alpine.js reactivity
// QA-Engineer: Parameter validation and visual quality
```

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

## Example Art Recipes (For Testing & Documentation)

When demonstrating features or testing changes, use these proven configurations:

### 🌌 Aurora Borealis
```
Pattern: Wave | Points: 85 | Threshold: 12
Resolution: 1° | Opacity: 4% | Color: Gradient
Optimizations: None
Effect: Flowing, layered waves resembling northern lights
```

### 🔮 Crystal Mandala
```
Pattern: Circle | Points: 120 | Threshold: 25
Resolution: 0.5° | Opacity: 12% | Color: Rainbow
Optimizations: Coarse Binning (Theta: 2°, Rho: 5px)
Effect: Intricate mandala with perfect radial symmetry
```

### ⭐ Star Constellation
```
Pattern: Random | Points: 60 | Threshold: 8
Resolution: 2° | Opacity: 20% | Color: Ocean
Optimizations: Vote Blurring (Radius: 2)
Effect: Matrix-like patterns with organic flow
```

### 🏛️ Minimalist Architecture
```
Pattern: Grid | Points: 40 | Threshold: 35
Resolution: 1° | Opacity: 90% | Color: Monochrome
Optimizations: Dynamic Threshold (25%)
Effect: Bold, clean geometric lines
```

### 🔥 Fire Vortex
```
Pattern: Spiral | Points: 75 | Threshold: 15
Resolution: 1.5° | Opacity: 8% | Color: Fire
Optimizations: Coarse Binning (Theta: 3°, Rho: 8px)
Effect: Swirling flame-like patterns
```

### ⚛️ Quantum Field
```
Pattern: Random | Points: 150 | Threshold: 5
Resolution: 1° | Opacity: 2% | Color: Gradient
Optimizations: All enabled (Coarse, Dynamic, Blur)
Effect: Extremely dense, field-like patterns
```

## Troubleshooting Guide for Agents

### Issue: No lines appearing
**Symptoms**: Canvas is blank except background
**Causes**:
1. Threshold too high for current binning
2. Not enough points generating votes
3. Resolution too coarse with fine binning

**Solutions**:
- Enable Coarse Binning (Theta: 5°, Rho: 10px)
- Lower threshold to 5-10
- Enable Dynamic Threshold
- Increase point count

### Issue: Too many lines (visual noise)
**Symptoms**: Canvas completely filled, hard to see pattern
**Causes**:
1. Threshold too low
2. Too many points
3. Opacity too high

**Solutions**:
- Increase threshold to 20-30
- Reduce point count to 30-50
- Lower opacity to 2-5%

### Issue: Performance slow
**Symptoms**: UI freezes when adjusting controls
**Causes**:
1. Fine resolution (0.5°) with many points (150)
2. Vote blurring with large radius
3. Too many lines being drawn

**Solutions**:
- Increase resolution to 2-3°
- Disable vote blurring
- Increase threshold to reduce line count
- Use coarse binning to reduce accumulator size

### Issue: Pattern not visible/clear
**Symptoms**: Lines there but pattern unclear
**Causes**:
1. Wrong opacity for line density
2. Color mode doesn't show structure
3. Noise in point generation obscuring pattern

**Solutions**:
- Adjust opacity inversely to line count
- Try Monochrome or Gradient color mode
- Reduce noise in `createPoints` (currently ±10 pixels)

## Additional Resources

### Project Documentation
- **[Project README](./README.md)** - User guide, examples, comprehensive control documentation
- **[Implementation Guide](./IMPLEMENTATION.md)** - Technical implementation details
- **[Quick Start Guide](./QUICKSTART.md)** - User-friendly getting started
- **[PR Documentation](./docs/hough/hough-waves-pr-01.md)** - Original PR description

### Algorithm Understanding
- **[Hough Transform Explanation](./docs/hough/01/hough-01.md)** - Detailed algorithm walkthrough
- **[Hough Waves Research](./docs/hough/hough-waves.md)** - Claude Opus research documentation
- **[Wikipedia: Hough Transform](https://en.wikipedia.org/wiki/Hough_transform)** - Mathematical foundation

### Alpine.js Resources
- **[Role Collaboration Guide](./docs/guides/Roles.md)** - How roles work together effectively
- **[Copilot Role Usage Guide](./docs/guides/Roles-Copilot.md)** - AI-specific role implementation patterns
- **[Complete Alpine.js Guide](./docs/alpine-guide.md)** - Comprehensive patterns and examples
- **[Alpine.js Template README](./docs/alpine-readme.md)** - Original template documentation

## Agent Working Guidelines

### When Working on Hough Waves Issues

1. **Understand the Algorithm First**: Review the mathematical foundation and voting mechanism
2. **Test with Known Recipes**: Use the example configurations to validate changes
3. **Consider All Optimizations**: Changes may affect accumulator behavior differently with each optimization
4. **Preserve Performance**: Canvas rendering with hundreds of lines must stay responsive
5. **Document Parameter Interactions**: Complex interactions between controls need clear explanation

### Making Changes to Core Algorithm

**CRITICAL**: The `computeHoughTransform` function is the heart of the application.

**Before modifying**:
- Understand current binning strategy
- Consider impact on vote accumulation
- Test with all three optimization modes
- Validate with multiple patterns

**After modifying**:
- Test all pattern types
- Verify threshold range still works (5-50)
- Check performance with 150 points
- Validate with known recipes

### Adding New Features

**New Pattern Types**:
- Add to `createPoints` method
- Maintain noise addition pattern
- Test with various point counts
- Document mathematical formula

**New Color Modes**:
- Add to `getColor` method
- Consider dark mode compatibility
- Test with various opacities
- Ensure adequate contrast

**New Optimizations**:
- Add state variables
- Add UI controls in Advanced Options section
- Implement in `computeHoughTransform`
- Add to Stats display badges
- Document in README

---

**Remember**: Hough Waves combines mathematical rigor with artistic expression. Solutions should respect both the algorithmic correctness and the creative possibilities. Always adopt the appropriate role perspective(s) and leverage the documented patterns and lessons learned.