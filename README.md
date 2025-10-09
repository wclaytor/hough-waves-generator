# 🌊 Hough Waves - Algorithmic Art Generator

Transform mathematical algorithms into stunning visual art using the Hough transform from computer vision. Create beautiful, wave-like patterns through the elegant interplay of geometry, voting systems, and emergent complexity.

[![Algorithm](https://img.shields.io/badge/Algorithm-Hough_Transform-7C3AED)](https://en.wikipedia.org/wiki/Hough_transform)
[![Alpine.js](https://img.shields.io/badge/Alpine.js-3.x-8BC0D0?logo=alpine.js)](https://alpinejs.dev/)
[![Art](https://img.shields.io/badge/Art-Generative-FF6B6B)](https://github.com)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.md)


## 🎨 What Are Hough Waves?

Hough Waves represent a fascinating intersection of **computer vision and generative art**. The application uses the **Hough Transform algorithm** (invented by Paul Hough in 1962) to detect lines in a creative, artistic way.

### The Algorithm

Instead of analyzing photographs to find edges, Hough Waves:
1. **Generates points** in artistic patterns (waves, spirals, circles, grids, random)
2. **Transforms each point** into a sinusoidal curve in parameter space (θ, r)
3. **Accumulates votes** - each point "votes" for all possible lines through it
4. **Detects consensus** - lines receiving enough votes are drawn
5. **Creates emergence** - complex patterns emerge from simple mathematical rules

### Artistic Inspiration

Inspired by the 2004 art project by **Andreas Schjønhaug & Kristoffer Stenersen** at NTNU, Norway, which explored the aesthetic potential of computer vision algorithms.

## 🚀 Quick Start

### Try It Now!

1. **Download** `index.html` from this repository
2. **Double-click** to open in your browser (works offline!)
3. **Experiment** with the controls to create unique art
4. **Download** your creations as PNG files

### Instant Examples

Copy these settings to try different artistic effects:

**🌌 Northern Lights**
- Pattern: Wave
- Points: 80
- Threshold: 15
- Resolution: 1°
- Opacity: 5%
- Color: Gradient

**🔮 Crystal Mandala**
- Pattern: Circle
- Points: 100
- Threshold: 20
- Resolution: 0.5°
- Opacity: 8%
- Color: Rainbow

**⭐ Star Constellation**
- Pattern: Random
- Points: 50
- Threshold: 10
- Resolution: 2°
- Opacity: 15%
- Color: Monochrome

## 📖 Background & Research

### The Hough Transform

The Hough Transform is a feature extraction technique in computer vision used to detect geometric shapes. It works by mapping points from image space to parameter space:

**Mathematical Foundation:**
- A line in (x, y) space is represented as: `r = x·cos(θ) + y·sin(θ)`
- Where `θ` is the angle from the x-axis, and `r` is the perpendicular distance from origin
- Each point generates a **sinusoidal curve** in (θ, r) parameter space
- Lines in image space appear as **intersection points** in parameter space

### From Computer Vision to Art

Traditional use: Detecting lines in photographs
**Our artistic use**: Creating emergent patterns through:
- Deliberate point arrangements (patterns)
- Vote accumulation (threshold)
- Semi-transparent overlays (opacity)
- Multiple color schemes

### Research & Development

This implementation was developed through collaborative AI-assisted development:

1. **Research Phase**: Studied original Hough Transform papers and artistic implementations
2. **Initial PR**: Created baseline implementation following Alpine.js template best practices
3. **Algorithm Refinement**: Corrected implementation to use true sinusoidal voting in parameter space
4. **Optimization Phase**: Added three advanced optimization strategies for better line detection

## 🎛️ Controls & Parameters

### Basic Controls

#### **Pattern Type**
Determines the spatial distribution of initial points:

- **Wave** - Sinusoidal curve with added noise. Creates flowing, organic patterns
  - *Frequency* (1-10): Number of wave cycles across canvas
  - *Amplitude* (50-250px): Height of wave peaks
- **Spiral** - Expanding vortex from center. Produces radial symmetry
  - *Rotations* (1-10): Number of complete rotations
  - *Radius* (20-50%): Size relative to canvas
- **Circle** - Points arranged in a circle. Creates mandala-like designs
  - *Radius* (10-50%): Size relative to canvas
- **Grid** - Regular grid layout. Generates geometric networks
- **Random** - Scattered points. Produces chaotic, constellation-like patterns

**Note**: Pattern-specific parameters appear dynamically when you select Wave, Spiral, or Circle patterns, allowing fine-tuned control over the pattern shape.

#### **Points** (10-150)
Controls how many points are generated:
- **Low (10-30)**: Sparse, minimal patterns with clear geometric structure
- **Medium (40-80)**: Balanced complexity with visible wave formations
- **High (90-150)**: Dense, intricate patterns with rich texture

**Impact**: More points = more potential lines, but also more vote fragmentation

#### **Threshold** (5-50 votes)
Minimum votes required for a line to be drawn:
- **Low (5-15)**: Shows many lines, including subtle connections. More chaotic
- **Medium (15-25)**: Balanced - shows major structural lines with some detail
- **High (25-50)**: Only strongest alignments. Very clean, geometric look

**Key Insight**: This is the "confidence level" for line detection. Lower threshold = more artistic freedom, higher = more mathematical precision

#### **Resolution** (0.5°-5°)
Angular step size when sampling θ values:
- **Fine (0.5°-1°)**: Smooth, precise curves. More computational work
- **Medium (1°-2°)**: Good balance of quality and performance
- **Coarse (3°-5°)**: Faster computation, more artistic variation

**Trade-off**: Finer resolution = smoother patterns but more vote fragmentation

#### **Opacity** (1%-100%)
Transparency of each drawn line:
- **Very Low (1-5%)**: Ethereal, layered effects. Best for dense patterns
- **Low (10-20%)**: Subtle wave formations with depth
- **Medium (30-50%)**: Clear lines with some overlay effects
- **High (60-100%)**: Bold, graphic line art

**Pro Tip**: Lower opacity works better with lower thresholds (more lines)

#### **Color Mode**
Determines line coloring strategy:
- **Monochrome**: White on black (light mode) or black on white (dark mode)
- **Rainbow**: Full HSL spectrum from red to violet
- **Gradient**: Purple-to-pink color transition
- **Ocean**: Blue-teal atmospheric tones
- **Fire**: Red-orange-yellow flame colors
- **Sunset**: Warm oranges, pinks, and purples
- **Forest**: Greens and earth tones
- **Neon**: Vibrant electric colors
- **Pastel**: Soft, muted colors
- **Midnight**: Deep blues and purples
- **Autumn**: Warm reds, oranges, and browns
- **Spring**: Fresh greens and yellows
- **Galaxy**: Purples, blues, and pinks
- **Lava**: Deep reds and oranges
- **Arctic**: Cool blues and whites

### Advanced Optimization Options

These controls fine-tune the Hough Transform algorithm for better line detection:

#### **🔵 Coarse Binning**
Groups similar lines together in parameter space:

**Theta Bin Size** (1°-10°): Angle grouping tolerance
- Larger bins = more votes accumulate per line
- Helps when points are slightly misaligned

**Rho Bin Size** (2-20px): Distance grouping tolerance
- Larger bins = more forgiving line detection
- Useful for noisy point patterns

**When to use**: Enable when threshold seems too high and you're not seeing enough lines

#### **🟣 Dynamic Threshold**
Automatically scales threshold based on number of points:

**Multiplier** (5%-50% of points): 
- Calculates threshold as: `points × multiplier`
- Example: 50 points × 20% = 10 vote threshold
- Automatically adjusts as you change point count

**When to use**: Enable for consistent results across different point counts

#### **🟢 Vote Blurring**
Spreads each vote to neighboring bins using Gaussian weighting:

**Blur Radius** (1-5 bins):
- Larger radius = more vote spreading
- Helps similar lines accumulate votes
- Uses exponential falloff for natural distribution

**When to use**: Enable when lines seem fragmented or you want smoother detection

### How Controls Interact

**Creating Dense Patterns:**
- High points (100+) + Low threshold (10) + Low opacity (3%) = Ethereal waves

**Creating Geometric Art:**
- Medium points (50) + High threshold (30) + High opacity (80%) = Bold structure

**Exploring the Algorithm:**
- Enable all optimizations + adjust parameters = See how vote accumulation works

**Performance Tuning:**
- Lower resolution (3°-5°) + Coarse binning = Faster generation with artistic variation

## 🎨 Example Gallery

### Recipe: "Aurora Borealis"
```
Pattern: Wave
Points: 85
Threshold: 12
Resolution: 1°
Opacity: 4%
Color: Gradient
Optimizations: None
```
Creates flowing, layered waves resembling northern lights.

### Recipe: "Sacred Geometry"
```
Pattern: Circle
Points: 120
Threshold: 25
Resolution: 0.5°
Opacity: 12%
Color: Rainbow
Optimizations: Coarse Binning (Theta: 2°, Rho: 5px)
```
Produces intricate mandala patterns with perfect radial symmetry.

### Recipe: "Digital Rain"
```
Pattern: Random
Points: 60
Threshold: 8
Resolution: 2°
Opacity: 20%
Color: Ocean
Optimizations: Vote Blurring (Radius: 2)
```
Creates matrix-like patterns with organic flow.

### Recipe: "Minimalist Architecture"
```
Pattern: Grid
Points: 40
Threshold: 35
Resolution: 1°
Opacity: 90%
Color: Monochrome
Optimizations: Dynamic Threshold (25%)
```
Bold, clean geometric lines with strong structural presence.

### Recipe: "Fire Vortex"
```
Pattern: Spiral
Points: 75
Threshold: 15
Resolution: 1.5°
Opacity: 8%
Color: Fire
Optimizations: Coarse Binning (Theta: 3°, Rho: 8px)
```
Swirling, flame-like patterns emanating from center.

### Recipe: "Quantum Field"
```
Pattern: Random
Points: 150
Threshold: 5
Resolution: 1°
Opacity: 2%
Color: Gradient
Optimizations: All enabled (Coarse, Dynamic, Blur)
```
Extremely dense, field-like patterns suggesting quantum probability clouds.

## 🏗️ Development History

### Initial Implementation (PR #2)

Created by GitHub Copilot coding agent based on:
- Alpine.js standalone HTML application template
- Claude Opus research documentation
- Original Hough Waves art project (2004)

**Key Features:**
- Single HTML file architecture (24KB)
- Alpine.js 3.x reactive patterns
- Tailwind CSS styling
- 5 pattern types, 5 color modes
- PWA capabilities
- Dark mode support

### Algorithm Enhancement

**Issue Discovered**: Original pair-wise point voting didn't produce smooth wave patterns

**Solution Implemented**: Corrected to true Hough Transform
- Each point generates sinusoidal curve in parameter space
- Proper (θ, r) accumulator voting
- Polar coordinate representation
- Results in authentic wave-like patterns

### Optimization Framework

**Challenge**: High threshold values (>12) produced no visible lines

**Analysis**: Vote fragmentation due to:
- Fine-grained binning (1° theta, 2px rho)
- Floating-point precision issues
- Noise in point generation
- Maximum votes per bin too low

**Solution**: Three-pronged optimization system
- Coarse Binning: Group similar lines
- Dynamic Threshold: Auto-scale with point count
- Vote Blurring: Spread votes to neighbors

**Result**: Users can now explore full parameter space with any combination of optimizations

## 🛠️ Technical Stack

- **Alpine.js 3.x** - Reactive component framework
- **Tailwind CSS** - Utility-first styling
- **Bootstrap Icons** - UI iconography
- **HTML5 Canvas** - High-performance rendering
- **LocalStorage** - Settings persistence
- **PWA** - Installable application support

## 📱 Features

✅ **Single HTML File** - Entire app in one 24KB file  
✅ **Works Offline** - No server or internet required  
✅ **Responsive Design** - Mobile, tablet, and desktop  
✅ **Dark Mode** - Full theme support with persistence  
✅ **PWA Ready** - Installable on any platform  
✅ **Export Art** - Download creations as PNG  
✅ **Real-time Updates** - Instant visual feedback  
✅ **Cross-browser** - Chrome, Firefox, Safari, Edge  

## 🎓 Educational Value

This project demonstrates:

### Computer Science Concepts
- **Algorithm Visualization**: See the Hough Transform in action
- **Parameter Space Mapping**: Points → Sinusoids transformation
- **Vote Accumulation**: Democratic line detection
- **Optimization Strategies**: Multiple approaches to solving vote fragmentation

### Software Engineering
- **Single File Architecture**: Complete app without build process
- **Reactive Patterns**: Alpine.js state management
- **Progressive Enhancement**: Works without optimizations, better with them
- **User Experience**: Immediate feedback and experimentation

### Mathematics & Art
- **Polar Coordinates**: r = x·cos(θ) + y·sin(θ)
- **Trigonometric Functions**: Sinusoidal curves in parameter space
- **Emergence**: Complex patterns from simple rules
- **Aesthetic Exploration**: Math as medium for artistic expression

## 📚 Further Reading

### Hough Transform
- [Wikipedia: Hough Transform](https://en.wikipedia.org/wiki/Hough_transform)
- [Original Paper: Paul Hough (1962)](https://en.wikipedia.org/wiki/Paul_Hough)

### Alpine.js Development
- [Alpine.js Documentation](https://alpinejs.dev/)
- [Alpine.js Template guide](docs/alpine/alpine-readme.md)
- [Alpine.js Standalone Guide](docs/alpine/alpine-standalone-guide.md)

### Project Documentation
- `IMPLEMENTATION.md` - Technical implementation details
- `QUICKSTART.md` - User getting started guide

## 🤝 Contributing

Contributions welcome! Areas for enhancement:

- Additional pattern types (hexagonal, fibonacci spiral, etc.)
- More color schemes (sunset, neon, pastel, etc.)
- Export options (SVG, different resolutions)
- Animation/time-based evolution
- Preset library system
- Social sharing features

## 📄 License

MIT License - Free for any use, personal or commercial.

## 🙏 Credits

- **Original Art Concept**: Andreas Schjønhaug & Kristoffer Stenersen (2004, NTNU Norway)
- **Hough Transform Algorithm**: Paul Hough (1962)
- **Implementation**: GitHub Copilot coding agent + Human collaboration
- **Research**: Claude Opus
- **Framework**: Alpine.js by Caleb Porzio
- **Styling**: Tailwind CSS by Adam Wathan

## 🌟 Gallery

Share your creations! Tag with #HoughWaves

---

**Transform mathematics into art. Explore the beauty of algorithms. Create something unique.** 🌊✨
