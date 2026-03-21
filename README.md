# Jai Narula — Space Portfolio

> An immersive solar system portfolio built entirely in a single HTML file. Each planet in the solar system represents a section of my professional profile. Click a planet to explore.

**Live:** [Deploy the HTML file to any static host — GitHub Pages, Vercel, or Netlify]

---

## Preview

```
☀️  The Sun      →  About Me
☿   Mercury      →  Skills
♀   Venus        →  Projects
🌍  Earth        →  Experience
♂   Mars         →  Achievements
♃   Jupiter      →  Certifications
♄   Saturn       →  Education
♅   Uranus       →  AI Projects (NIKA)
♆   Neptune      →  Contact
```

---

## Features

### Visual
- **WebGL planets** — each planet is a live Three.js sphere with procedural noise textures (Perlin noise, 8-octave fBm), proper lighting, atmospheric glow and specular shine overlay
- **Saturn rings** — full ring geometry with Cassini Division gap and radial UV mapping
- **Earth** — spherical UV mapping for correct pole distribution, continent mask, ice caps, animated cloud layer
- **Live star field** — 320 stars with individual twinkle phases, brightness tiers, color tints (blue-white, warm amber), and diffraction spikes on bright stars
- **Colored meteor shower** — 10 mineral-based colors (magnesium blue-white, sodium yellow, iron orange, copper cyan, nickel green, lithium red, potassium violet, calcium blue) with gradient trails and head glow
- **Nebula glow blobs** — 4 slow-drifting radial gradient orbs creating depth in the background
- **Specular shine** — CSS pseudo-element shine layer on each planet simulating directional starlight

### Interaction
| Input | Action |
|-------|--------|
| Click menu item | Select planet |
| Click planet | Open full details |
| `↑` / `↓` arrows | Navigate planets |
| Mouse wheel | Scroll through planets |
| Touch swipe up/down | Navigate planets (mobile) |
| `Enter` | Open full details of current planet |
| `Escape` | Close overlay |
| Hover planet | Scale + brightness boost |
| Hover menu item | Slide + tooltip |
| Mouse move on overlay | 3D camera parallax |

### Overlay Panels
Each planet's "Full Details" opens a full-screen immersive panel with:
- Live Three.js 3D scene unique to each section (DNA helix, bar chart, globe, neural network, etc.)
- Mouse-parallax camera responding to cursor movement
- Staggered entrance animations on all content elements
- Animated skill bars, timeline, project cards, trophy cards, cert badges, roadmap nodes

---

## Stack

| Layer | Tech |
|-------|------|
| 3D Rendering | Three.js r128 (WebGL) |
| Textures | Procedural Perlin noise (CPU canvas) |
| Fonts | Orbitron, Exo 2, Share Tech Mono (Google Fonts) |
| Styling | Vanilla CSS with CSS custom properties |
| Logic | Vanilla JavaScript (ES6+) |
| Bundling | None — single HTML file, zero build step |

---

## Project Structure

```
portfolio.html          ← Everything. One file.
│
├── <style>             ← All CSS (loading screen, planets, menu, overlay)
├── <script src="...">  ← Three.js from cdnjs CDN
└── <script>
    ├── Planet data (P[])
    ├── Star / meteor animation
    ├── Menu builder
    ├── Planet texture generators (sunTex, earthTex, etc.)
    ├── Three.js planet renderer (buildPlanets)
    ├── 9× Scene builders (buildScene_*)
    ├── 9× Content builders (buildContent_*)
    ├── Overlay system (openOverlay, closeOverlay)
    ├── selectPlanet + all interaction handlers
    └── Loading screen (initLoadingScreen)
```

---

## Running Locally

No build step needed. Just open the file:

```bash
# Option 1 — direct
open portfolio.html

# Option 2 — local server (avoids any CORS issues with fonts)
npx serve .
# then open http://localhost:3000

# Option 3 — Python
python3 -m http.server 8080
# then open http://localhost:8080
```

---

## Deploying

### GitHub Pages
1. Push `portfolio.html` to a repo
2. Go to Settings → Pages → Source: main branch / root
3. Rename to `index.html` if you want it at the root URL

### Vercel
```bash
npx vercel --name jai-portfolio
# Vercel will detect the HTML file and deploy instantly
```

### Netlify
Drag and drop the HTML file onto [netlify.com/drop](https://netlify.com/drop)

---

## Customisation

### Change content
All portfolio data lives in the `P[]` array near the top of the script. Each planet object has:

```js
{
  id: 'mercury',
  name: 'Mercury',
  sec: 'Skills',
  col: '#E8927C',          // accent color
  blurb: '...',            // one-line shown before Full Details
  panel: {
    title: 'Skills',
    eye: '...',
    secs: [{ t: 'Section Title', li: ['item 1', 'item 2'] }],
    tags: ['SQL', 'Python'],
    acts: [{ l: 'Button Label', h: 'https://...', p: true }]
  }
}
```

### Change planet colors
Edit the `col` field in each planet object. The color propagates to glow, menu dot, overlay accent, and skill bar.

### Add a resume download
Add this to the Sun (About Me) content builder or the Neptune (Contact) panel:

```html
<a href="YOUR_RESUME_URL.pdf" download class="ov-btn-secondary">Download Resume</a>
```

---

## Projects Featured

| Project | Stack | Link |
|---------|-------|------|
| **NIKA AI Analytics Platform** | Gemini AI, Flask, React, Vercel | [Live](https://nika-ai-platform.vercel.app/) · [GitHub](https://github.com/jaijaijai353/NIKA--main) |
| **Blinkit Sales Dashboard** | Power BI, DAX, Star Schema | [GitHub](https://github.com/jaijaijai353/Blinkit-Sales-Dashboard) |
| **Netflix Content EDA Pipeline** | Python, Pandas, Seaborn | [GitHub](https://github.com/jaijaijai353/Netflix-EDA-Analysis) |

---

## Contact

**Jai Narula** — BBA Business Analytics, SRM University Delhi NCR  
Degree completion: June 2026

- Email: [jai.narula08@gmail.com](mailto:jai.narula08@gmail.com)
- Phone: +91 70424 26504
- LinkedIn: [jai-narula-aa3185242](https://www.linkedin.com/in/jai-narula-aa3185242/)
- GitHub: [jaijaijai353](https://github.com/jaijaijai353)

---

## Performance Notes

- File size: ~145 KB (all-in-one)
- Planet textures: 11× 512px procedural (generated on load, ~1–2s on first visit)
- Three.js loaded from CDN: ~580 KB (cached after first load)
- Only the active planet's scene is rendered each frame (idle scenes paused)
- GPU memory is released via `dispose()` when overlay panels are closed

---

## Browser Support

| Browser | Status |
|---------|--------|
| Chrome 90+ | ✅ Full support |
| Firefox 88+ | ✅ Full support |
| Safari 15+ | ✅ Full support |
| Edge 90+ | ✅ Full support |
| Mobile Chrome/Safari | ✅ Touch swipe supported |

Requires WebGL support. Falls back gracefully on unsupported browsers (planet canvas remains blank, rest of UI functional).

---

*Built with Three.js, Perlin noise, and no frameworks.*
