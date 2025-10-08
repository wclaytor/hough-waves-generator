# 🌊 Hough Waves - Quick Start Guide

## Try It Now! (30 Seconds)

### Step 1: Open the App
```bash
# Just open index.html in your browser
# - Double-click the file, OR
# - Drag it to your browser, OR
# - Right-click → Open With → Browser
```

### Step 2: Watch It Work
The app automatically generates a beautiful Hough wave pattern when it loads!

### Step 3: Experiment
Try these quick experiments:

#### 🎨 Try These Examples

Copy these settings exactly to create stunning art:

### 🌌 Aurora Borealis
```
Pattern: Wave | Points: 85 | Threshold: 12
Resolution: 1° | Opacity: 4% | Color: Gradient
Optimizations: None
```
*Flowing, layered waves resembling northern lights*

### � Crystal Mandala
```
Pattern: Circle | Points: 120 | Threshold: 25
Resolution: 0.5° | Opacity: 12% | Color: Rainbow
Optimizations: Coarse Binning (Theta: 2°, Rho: 5px)
```
*Intricate mandala with perfect radial symmetry*

### ⭐ Star Constellation
```
Pattern: Random | Points: 60 | Threshold: 8
Resolution: 2° | Opacity: 20% | Color: Ocean
Optimizations: Vote Blurring (Radius: 2)
```
*Matrix-like patterns with organic flow*

### 🏛️ Minimalist Architecture
```
Pattern: Grid | Points: 40 | Threshold: 35
Resolution: 1° | Opacity: 90% | Color: Monochrome
Optimizations: Dynamic Threshold (25%)
```
*Bold, clean geometric lines*

### 🔥 Fire Vortex
```
Pattern: Spiral | Points: 75 | Threshold: 15
Resolution: 1.5° | Opacity: 8% | Color: Fire
Optimizations: Coarse Binning (Theta: 3°, Rho: 8px)
```
*Swirling flame-like patterns*

### ⚛️ Quantum Field
```
Pattern: Random | Points: 150 | Threshold: 5
Resolution: 1° | Opacity: 2% | Color: Gradient
Optimizations: All enabled (Coarse, Dynamic, Blur)
```
*Extremely dense, field-like patterns*

## Tips & Tricks

### 🎯 Getting Started
1. Start with **Wave + Monochrome** to understand the basics
2. Try **Randomize All** a few times to see what's possible
3. Find a pattern you like, then fine-tune with sliders
4. Download your favorites before changing settings

### 🎨 Creating Art
- **Ethereal**: Low opacity (2-5%) with 80+ points, threshold 10-15
- **Bold**: High opacity (70-100%) with 30-50 points, threshold 30+
- **Minimal**: Low points (20-40) with high threshold (25-40)
- **Complex**: High points (120+) with low threshold (5-10), low opacity (2-4%)

### 💡 Pro Tips
- Change just one parameter at a time to understand its effect
- Dark mode is great for viewing light-colored patterns
- The "Generate New Pattern" button uses your current settings
- Download multiple variations before randomizing again
- Refresh the page to reset to default settings

### � Advanced Options (Click to expand in the app)

#### 🔵 Coarse Binning
**When to use**: Threshold above 20 produces no visible lines
- Groups similar line angles and distances together
- Try: Theta Bin 3-5°, Rho Bin 8-10px
- Makes high thresholds work effectively

#### 🟣 Dynamic Threshold
**When to use**: Want consistent results across point counts
- Auto-scales threshold based on number of points
- Try: Multiplier 20-25%
- Great for "Randomize!" experiments

#### 🟢 Vote Blurring
**When to use**: Lines look fragmented or broken
- Smooths vote distribution across nearby bins
- Try: Blur Radius 2-3
- Creates smoother, more connected patterns

### 🐛 Troubleshooting
- **Blank canvas?** Lower threshold to 5-10, or enable Coarse Binning
- **Too dense?** Increase threshold (25-40) or reduce points (30-50)
- **Too sparse?** Decrease threshold (5-10) or increase points (80-120)
- **Lines too faint?** Increase opacity (20-50%)
- **Performance slow?** Increase Resolution to 2-3°, or reduce points
- **Need a fresh start?** Refresh the page (F5)

---

## What's Happening Behind the Scenes?

### The Hough Transform Algorithm

When you click "Generate New Pattern", the app:

1. **Generates Points** - Places points based on your pattern choice (wave, spiral, circle, etc.)
2. **Computes Lines** - Each point votes for ALL possible lines passing through it
3. **Accumulates Votes** - Builds a vote map in polar coordinate space (angle θ, distance r)
4. **Detects Strong Lines** - Finds angles/distances that exceed your vote threshold
5. **Renders Art** - Draws detected lines with your chosen colors and opacity

**The Math**: For each point, the algorithm varies the angle θ from -90° to +90° and calculates r = x·cos(θ) + y·sin(θ). When multiple points lie on the same line, their votes converge at the same (θ, r) location—that's how lines are detected!

It's the same algorithm used in computer vision for detecting shapes in images!

---

## Next Steps

### Share Your Art
- Download PNG images to share on social media
- Email the entire `index.html` file to friends
- Host it on GitHub Pages for online access

### Learn More
- Read [IMPLEMENTATION.md](IMPLEMENTATION.md) for technical details
- Check [docs/hough-waves.md](docs/hough-waves.md) for algorithm deep-dive
- Explore the code in `index.html` (it's commented!)

### Customize It
The code is easy to modify! Try:
- Adding new pattern types
- Creating new color schemes
- Adjusting the canvas size
- Adding animation effects

---

## Need Help?

### Common Questions

**Q: Does it work offline?**  
A: Yes! Once the page loads initially, it works without internet.

**Q: Can I install it as an app?**  
A: Yes! It's a PWA - look for the install prompt in your browser.

**Q: What browsers work?**  
A: All modern browsers (Chrome, Firefox, Safari, Edge).

**Q: Can I use this commercially?**  
A: Check the license file, but generally the template is free to use.

**Q: How do I host it online?**  
A: Upload `index.html` to any web host or use GitHub Pages.

---

## Have Fun! 🎉

The beauty of Hough Waves is that every generation is unique. Experiment, explore, and create stunning algorithmic art!

**Remember**: There are no wrong settings - just different artistic expressions! ✨
