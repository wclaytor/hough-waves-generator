# 🎛️ Hough Waves - Settings Template

This template provides all available settings with example values. Use this as a reference when configuring Hough Waves or creating your own presets.

## 📋 Basic Settings

### Pattern Type
**Setting**: `pattern`  
**Type**: Selection  
**Options**: `wave`, `spiral`, `circle`, `grid`, `random`  
**Example**: `wave`  
**Description**: Determines the spatial distribution of initial points

#### Wave Pattern Parameters
**Setting**: `waveFrequency`  
**Type**: Range (1-10)  
**Example**: `4`  
**Description**: Number of wave cycles across the canvas  
**Note**: Only applies when pattern is `wave`

**Setting**: `waveAmplitude`  
**Type**: Range (50-250)  
**Unit**: Pixels (px)  
**Example**: `150`  
**Description**: Height of the wave peaks  
**Note**: Only applies when pattern is `wave`

#### Spiral Pattern Parameters
**Setting**: `spiralRotations`  
**Type**: Range (1-10)  
**Example**: `6`  
**Description**: Number of complete rotations in the spiral  
**Note**: Only applies when pattern is `spiral`

**Setting**: `spiralRadius`  
**Type**: Range (0.2-0.5)  
**Example**: `0.4`  
**Percentage**: `40%`  
**Description**: Size of the spiral relative to canvas  
**Note**: Only applies when pattern is `spiral`

#### Circle Pattern Parameters
**Setting**: `circleRadius`  
**Type**: Range (0.1-0.5)  
**Example**: `0.3`  
**Percentage**: `30%`  
**Description**: Size of the circle relative to canvas  
**Note**: Only applies when pattern is `circle`

### Number of Points
**Setting**: `numPoints`  
**Type**: Range (10-150)  
**Example**: `50`  
**Description**: Controls how many points are generated in the pattern

### Threshold
**Setting**: `threshold`  
**Type**: Range (5-50)  
**Example**: `15`  
**Description**: Minimum votes required for a line to be drawn

### Resolution (Theta Step)
**Setting**: `thetaStep`  
**Type**: Range (0.5-5.0)  
**Unit**: Degrees (°)  
**Example**: `1`  
**Description**: Angular step size when sampling θ values

### Opacity
**Setting**: `opacity`  
**Type**: Range (0.01-1.0)  
**Example**: `0.05`  
**Percentage**: `5%`  
**Description**: Transparency of each drawn line (0.01 = 1%, 1.0 = 100%)

### Color Mode
**Setting**: `colorMode`  
**Type**: Selection  
**Options**: `mono`, `rainbow`, `gradient`, `ocean`, `fire`, `sunset`, `forest`, `neon`, `pastel`, `midnight`, `autumn`, `spring`, `galaxy`, `lava`, `arctic`  
**Example**: `mono`  
**Description**: Determines line coloring strategy

## 🔧 Advanced Optimization Settings

### Coarse Binning
**Setting**: `useCoarseBinning`  
**Type**: Boolean (checkbox)  
**Example**: `false`  
**Description**: Enable grouping of similar lines in parameter space

#### Theta Bin Size
**Setting**: `thetaBinSize`  
**Type**: Range (1-10)  
**Unit**: Degrees (°)  
**Example**: `1`  
**Description**: Angle grouping tolerance (only active when Coarse Binning is enabled)  
**Note**: Larger bins = more votes accumulate per line

#### Rho Bin Size
**Setting**: `rhoBinSize`  
**Type**: Range (2-20)  
**Unit**: Pixels (px)  
**Example**: `2`  
**Description**: Distance grouping tolerance (only active when Coarse Binning is enabled)  
**Note**: Larger bins = more forgiving line detection

### Dynamic Threshold
**Setting**: `useDynamicThreshold`  
**Type**: Boolean (checkbox)  
**Example**: `false`  
**Description**: Automatically scales threshold based on number of points

#### Threshold Multiplier
**Setting**: `thresholdMultiplier`  
**Type**: Range (0.05-0.5)  
**Example**: `0.2`  
**Percentage**: `20%`  
**Description**: Percentage of points used to calculate threshold (only active when Dynamic Threshold is enabled)  
**Formula**: `effective_threshold = numPoints × thresholdMultiplier`

### Vote Blurring
**Setting**: `useBlurring`  
**Type**: Boolean (checkbox)  
**Example**: `false`  
**Description**: Spreads votes to neighboring bins using Gaussian weighting

#### Blur Radius
**Setting**: `blurRadius`  
**Type**: Range (0.1-5)  
**Unit**: Bins  
**Example**: `0.1`  
**Description**: Number of neighboring bins to blur into (only active when Vote Blurring is enabled)  
**Note**: Larger radius = more vote spreading

## 🌙 Display Settings

### Dark Mode
**Setting**: `darkMode`  
**Type**: Boolean (toggle)  
**Example**: `false`  
**Description**: Enables dark theme for the interface and inverts canvas background  
**Note**: Automatically saved to localStorage

## 📝 Complete Example Settings

### Example 1: Aurora Borealis
```
pattern: wave
waveFrequency: 4
waveAmplitude: 150
numPoints: 85
threshold: 12
thetaStep: 1
opacity: 0.04
colorMode: gradient
useCoarseBinning: false
useDynamicThreshold: false
useBlurring: false
darkMode: false
```

### Example 2: Crystal Mandala (with Coarse Binning)
```
pattern: circle
circleRadius: 0.3
numPoints: 120
threshold: 25
thetaStep: 0.5
opacity: 0.12
colorMode: rainbow
useCoarseBinning: true
thetaBinSize: 2
rhoBinSize: 5
useDynamicThreshold: false
useBlurring: false
darkMode: false
```

### Example 3: Digital Rain (with Vote Blurring)
```
pattern: random
numPoints: 60
threshold: 8
thetaStep: 2
opacity: 0.20
colorMode: ocean
useCoarseBinning: false
useDynamicThreshold: false
useBlurring: true
blurRadius: 2
darkMode: false
```

### Example 4: Minimalist Architecture (with Dynamic Threshold)
```
pattern: grid
numPoints: 40
threshold: 35
thetaStep: 1
opacity: 0.90
colorMode: mono
useCoarseBinning: false
useDynamicThreshold: true
thresholdMultiplier: 0.25
useBlurring: false
darkMode: false
```

### Example 5: Quantum Field (All Optimizations)
```
pattern: random
numPoints: 150
threshold: 5
thetaStep: 1
opacity: 0.02
colorMode: gradient
useCoarseBinning: true
thetaBinSize: 3
rhoBinSize: 8
useDynamicThreshold: true
thresholdMultiplier: 0.15
useBlurring: true
blurRadius: 2
darkMode: false
```

## 💡 Tips for Using This Template

### Creating Custom Presets
1. Copy any example settings block
2. Modify the values to suit your artistic vision
3. Test the settings in the application
4. Save successful combinations for future use

### Understanding Value Ranges
- **Low opacity (0.01-0.05)**: Best for dense patterns with many lines
- **Medium opacity (0.1-0.3)**: Balanced visibility with some overlay
- **High opacity (0.5-1.0)**: Bold, clear lines with minimal blending

### Optimization Combinations
- **Coarse Binning + High Threshold**: Effective for clean geometric patterns
- **Dynamic Threshold**: Useful when frequently changing point count
- **Vote Blurring**: Helps create smoother, more connected patterns
- **All Three**: Maximum line detection, very dense results

### Performance Considerations
- Higher `thetaStep` (3-5°) = faster generation
- Lower `numPoints` (20-60) = faster generation
- Optimizations add computation time but improve results

## 🔄 Default Values

When the application loads for the first time, these are the default values:

```
pattern: wave
numPoints: 50
threshold: 15
thetaStep: 1
opacity: 0.05
colorMode: mono
waveFrequency: 4
waveAmplitude: 150
spiralRotations: 6
spiralRadius: 0.4
circleRadius: 0.3
useCoarseBinning: false
thetaBinSize: 1
rhoBinSize: 2
useDynamicThreshold: false
thresholdMultiplier: 0.2
useBlurring: false
blurRadius: 0.1
darkMode: false (or loaded from localStorage)
```

## 📚 Related Documentation

- **[README.md](README.md)** - Main project overview and examples
- **[QUICKSTART.md](QUICKSTART.md)** - User getting started guide
- **[IMPLEMENTATION.md](IMPLEMENTATION.md)** - Technical implementation details

---

*Use this template to experiment with settings, create presets, or understand how each parameter affects the final artwork.* ✨
