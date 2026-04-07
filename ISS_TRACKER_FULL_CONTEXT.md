# ISS Live Tracker — Full Project Context
> **Last Updated:** April 2026  
> **Use this file as context in Antigravity (or any AI tool) to continue work on the project without losing history.**

---

## 1. Project Identity

| Field | Value |
|---|---|
| **Project Name** | ISS Live Tracker |
| **Live URL** | https://vaibhavnagare-gis.github.io/ISS_LIVE_TRACKER/ |
| **Developer** | Vaibhav Shivaji Nagare |
| **Degree** | M.Sc. Geoinformatics |
| **Institution** | Bharati Vidyapeeth's Institute of Environment Education and Research, Pune |
| **Contact (LinkedIn)** | https://www.linkedin.com/in/vaibhav-nagare-gis |
| **Contact (GitHub)** | https://github.com/VaibhavNagare-GIS |
| **Contact (Email)** | vaibhavnagare20@gmail.com |
| **Current Version** | v2.0 (in progress — UI/UX enhancement phase) |
| **File** | Single HTML file: `Newwww.html` (deployed as `index.html` on GitHub Pages) |

---

## 2. Tech Stack

- **Architecture:** Single self-contained HTML file (no build process, no framework)
- **Language:** Vanilla JavaScript (ES6+)
- **Mapping Library:** Leaflet.js v1.9.4
- **Icons:** Font Awesome 6.4.0
- **CSS:** Pure CSS3 (custom properties, Grid, Flexbox, animations)
- **Deployment:** GitHub Pages (static hosting)
- **No npm, no webpack, no React/Vue** — intentionally kept simple for portfolio/academic use

---

## 3. External Dependencies (CDN)

```html
<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

<!-- Font Awesome -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />

<!-- Leaflet JS (bottom of body) -->
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
```

---

## 4. APIs & Data Sources

| Purpose | Endpoint |
|---|---|
| **ISS Real-Time Position** | `https://api.wheretheiss.at/v1/satellites/25544` |
| **Current Crew Members** | `https://corquaid.github.io/international-space-station-APIs/JSON/people-in-space.json` |
| **Map Tiles (Satellite)** | Esri World Imagery: `https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}` |
| **Map Tiles (Labels overlay)** | CartoDB Light Labels: `https://{s}.basemaps.cartocdn.com/light_only_labels/{z}/{x}/{y}{r}.png` |

- **Poll Interval:** Every 5 seconds (`const INTERVAL = 5000`)
- **Orbit Period Constant:** `92 * 60 * 1000` ms (92 minutes)
- **NORAD ID for ISS:** 25544

---

## 5. Current Features (v1.x — Working & Deployed)

1. **Real-time ISS position** — updates every 5 seconds via WhereTheISS API
2. **Live data panel** — Latitude, Longitude, Altitude, Velocity, Visibility, Last Updated timestamp
3. **Interactive satellite map** — Leaflet with Esri World Imagery basemap + CartoDB label overlay
4. **Ground track** — cyan polyline showing up to 200 past positions
5. **Trajectory prediction** — yellow dashed line extrapolating next ~15 steps from current velocity delta
6. **Current crew list** — dynamically loaded from corquaid API, displayed as gradient cards in a grid
7. **Toggle controls** — Ground Track, Trajectory, Follow ISS (all tri-state buttons with ARIA)
8. **Orbit progress ring** — SVG circular progress showing % complete of current orbit
9. **Orbit stats** — orbits completed today + minutes remaining in current orbit
10. **ISS facts scrolling banner** — auto-scrolling marquee below header
11. **UN SDG section** — 4 full-detail cards for SDG 4, 9, 13, 17 with links
12. **SDG badges in header** — quick-link chips for all 4 SDGs
13. **Toast notifications** — bottom-right pop-ups for user feedback
14. **Error banner** — shown when API fails, hides on success
15. **Responsive design** — 2-column grid on desktop, stacked on mobile
16. **ISS popup on map click** — rich popup with all live data in styled layout
17. **Sticky header** with slide-down animation
18. **ARIA accessibility** — aria-live regions, role labels, aria-pressed on toggles

---

## 6. Complete CSS Design System

### 6.1 CSS Custom Properties (`:root`)

```css
:root {
  --bg-main: #f8f9fa;
  --card-bg: #ffffff;
  --primary-blue: #1a73e8;
  --text-dark: #1a1a2e;
  --text-muted: #6b7280;
  --border: #e5e7eb;
  --green: #059669;
  --orange: #ea580c;
  --live-green: #43a047;
  --shadow: 0 2px 8px rgba(0,0,0,0.06);
  --shadow-hover: 0 4px 16px rgba(0,0,0,0.1);
}
```

### 6.2 SDG Brand Colors

| SDG | Color |
|---|---|
| SDG 4 (Quality Education) | `#c5192d` (red) |
| SDG 9 (Industry & Innovation) | `#fd6925` (orange) |
| SDG 13 (Climate Action) | `#3f7e44` (green) |
| SDG 17 (Partnerships) | `#19486a` (dark blue) |

### 6.3 Key CSS Animations

```css
@keyframes fadeInUp    /* card entrance — opacity 0→1, translateY 20px→0 */
@keyframes pulse       /* live badge — scale 1→1.05 every 2s */
@keyframes blink       /* live dot — opacity + glow on/off every 1.4s */
@keyframes slideDown   /* header entrance — translateY -100%→0 */
@keyframes scroll      /* facts banner marquee — translateX 0→-50% in 45s */
@keyframes countUp     /* data value update — opacity + translateY flash */
@keyframes slideInRight /* toast notification entrance */
```

### 6.4 Layout

- **Main grid:** `grid-template-columns: 340px 1fr` (sidebar + map area)
- **Sidebar gap:** 18px between cards
- **Card border-radius:** 14px
- **Card padding:** 22px
- **Mobile breakpoint 900px:** sidebar becomes 2-column grid
- **Mobile breakpoint 580px:** fully single column, map height 450px

### 6.5 Typography

- **Body font:** `'Segoe UI', Arial, sans-serif`
- **Data values font:** `'Courier New', monospace`
- **Card headings:** 0.85rem, uppercase, letter-spacing 1.2px
- **SDG number:** 2.2rem, font-weight 800

---

## 7. Complete HTML Structure

```
<header>                    — sticky, slideDown animation
  .header-left              — satellite emoji + h1 "ISS Live Tracker" + LIVE badge
  nav.sdg-badges            — SDG chip links (4, 9, 13, 17)

<div.facts-banner>          — scrolling marquee with ISS facts

<main.main-wrap>
  <aside.side-panel>
    <section.card>          — 📡 Live Position (lat, lon, alt, vel, vis, updated)
    <section.card>          — 🔄 Orbit Progress (SVG ring + orbit count + time left)

  <div.map-wrap>
    <div#error-banner>      — yellow warning when API fails
    <div.map-card>
      .map-toolbar          — title + toggle buttons (Ground Track, Trajectory, Follow ISS)
      <div#map>             — Leaflet map (600px height desktop, 450px mobile)
    <section.card>          — 👨‍🚀 Current Crew (crew-grid of crew-cards)
    <section.sdg-section>   — UN SDG alignment (4 SDG cards in grid)

<div.toast#toast>           — floating toast notification

<footer>
  .footer-left              — data sources + developer credit
  .footer-right             — LinkedIn / GitHub / Email icon links
```

---

## 8. Complete JavaScript Logic

### 8.1 Key Constants & Variables

```javascript
const API_URL = "https://api.wheretheiss.at/v1/satellites/25544";
const CREW_URL = "https://corquaid.github.io/international-space-station-APIs/JSON/people-in-space.json";
const INTERVAL = 5000;            // ms between ISS position fetches
const ORBIT_PERIOD = 92 * 60 * 1000;  // 92 minutes in ms

let followISS = true;             // whether map auto-centers on ISS
let showTrack = true;             // ground track polyline visibility
let showPredict = true;           // trajectory polyline visibility
let trackCoords = [];             // array of [lat, lon] pairs (max 200)
let lastLat = null, lastLon = null;  // previous position for delta prediction
```

### 8.2 Map Initialization

```javascript
const map = L.map("map", { center: [20, 0], zoom: 3, minZoom: 2, maxZoom: 10 });

// Layer 1: Esri satellite imagery
L.tileLayer("https://server.arcgisonline.com/...MapServer/tile/{z}/{y}/{x}", {...}).addTo(map);

// Layer 2: CartoDB label overlay (opacity 0.7)
L.tileLayer("https://{s}.basemaps.cartocdn.com/light_only_labels/{z}/{x}/{y}{r}.png", {...}).addTo(map);
```

### 8.3 ISS Marker

- Custom `L.divIcon` — 58×58px circular div, blue gradient, satellite emoji 🛰️
- Has `bindPopup` with rich HTML content (lat/lon/alt/vel/vis in a 2-column grid)
- Popup wrapper styled with purple gradient via `.leaflet-popup-content-wrapper`

### 8.4 Polylines

```javascript
let trackLine    = L.polyline([], { color: "#00d4ff", weight: 3, opacity: 0.8 });   // cyan
let predictLine  = L.polyline([], { color: "#ffeb3b", weight: 2, opacity: 0.7, dashArray: "8,6" }); // yellow dashed
```

### 8.5 `fetchISS()` — Core Update Function

1. Fetches `API_URL`
2. Parses `latitude`, `longitude`, `altitude`, `velocity`, `visibility`
3. Updates `issMarker` position
4. Updates popup content
5. Applies `.updating` CSS class to data elements (triggers countUp animation), then sets values after 100ms
6. Appends to `trackCoords[]` (max 200), updates `trackLine`
7. Computes linear prediction: `dLat * i * 5` for 15 steps ahead, updates `predictLine`
8. If `followISS` is true, calls `map.setView([lat, lon])` *(note: code appears truncated at end of file — this line is incomplete in source)*
9. On error: shows `#error-banner`, calls `showToast` with error type

### 8.6 `updateOrbitProgress()` — Orbit Ring Logic

```javascript
// Calculates elapsed ms within current 92-min orbit window
const elapsed = (now - orbitStartTime) % ORBIT_PERIOD;
const percent = Math.floor((elapsed / ORBIT_PERIOD) * 100);
// SVG circle circumference = 2π × 56 = 351.86
// strokeDashoffset = circumference × (1 - percent/100)
```

- `orbitStartTime` calculated once on page load from midnight
- Updates: `#progressCircle` strokeDashoffset, `#orbitPercent`, `#orbitCount`, `#timeLeft`

### 8.7 `fetchCrew()` — Crew Loading

- Fetches CREW_URL
- Filters for ISS crew only (field likely `"craft": "ISS"`)
- Renders `.crew-card` elements inside `#crew-list .crew-grid`
- Each card: avatar circle with initials + astronaut name
- Cards link externally (likely to NASA bio pages)
- Card style: purple gradient, hover lift + scale

### 8.8 Toggle Functions

```javascript
toggleLayer('track')    // toggles showTrack, adds/removes trackLine from map
toggleLayer('predict')  // toggles showPredict, adds/removes predictLine
toggleCenter()          // toggles followISS, shows toast feedback
```

- Each toggle updates button `.active` class and `aria-pressed` attribute

### 8.9 `showToast(title, message, type)`

- `type`: `"success"` or `"error"`
- Adds `.show` class, sets content, auto-removes after 3000ms
- Uses `slideInRight` animation

### 8.10 Interval Setup

```javascript
fetchISS();                            // immediate first call
setInterval(fetchISS, INTERVAL);       // then every 5 seconds
setInterval(updateOrbitProgress, 1000); // orbit ring updates every 1 second
fetchCrew();                           // crew loaded once on startup
```

---

## 9. UN SDG Alignment Details

| SDG | Number | Color | Description in App |
|---|---|---|---|
| Quality Education | 04 | `#c5192d` | Interactive STEM tool for students & educators |
| Industry, Innovation & Infrastructure | 09 | `#fd6925` | Open-source geospatial tech + live API infrastructure |
| Climate Action | 13 | `#3f7e44` | ISS monitors CO₂, sea levels, ice sheets, weather |
| Partnerships for the Goals | 17 | `#19486a` | 15-nation collaboration: NASA, ESA, JAXA, CSA, Roscosmos |

All SDG cards link to `https://sdgs.un.org/goals/goalN` (opens in new tab).

---

## 10. ISS Facts in Banner (Scrolling Marquee)

- First Module: Launched Nov 20, 1998
- Orbit Period: ~92 minutes
- Orbits per Day: ~15.5
- Size: 109m × 73m
- Solar Power: 120 kW
- Partners: NASA · ESA · JAXA · CSA · Roscosmos

---

## 11. Known Code Issues / Bugs

1. **Truncated `fetchISS()` function** — the source file `Newwww.html` appears to end mid-line at `if (followISS) map.setView` without closing parenthesis or the rest of the function, `setInterval` calls, or `fetchCrew()`. The live deployed version works, so the real source file likely has more content not captured in the provided snippet.
2. **SDG 13 card has a `</div>` closing tag** instead of `</a>` in the HTML source — minor bug that should be fixed.
3. **`trackCoords.push()` wraps across the anti-meridian** without correction — long east-west segments may appear on the map when ISS crosses 180°/-180° longitude.
4. **Crew card links** — the CREW_URL API may not provide individual astronaut bio URLs; clicking crew cards may not navigate anywhere meaningful.

---

## 12. What Needs Improvement (Enhancement Backlog)

### High Priority
- [ ] Night mode / dark theme toggle
- [ ] Speed/altitude mini chart (line graph over time using Canvas or SVG)
- [ ] Orbit counter animation (odometer-style number tick)
- [ ] ISS marker with CSS rotation animation (slowly spins)
- [ ] Fix anti-meridian crossing bug in ground track
- [ ] Fix SDG 13 closing tag bug (`</div>` → `</a>`)
- [ ] Close/complete truncated `fetchISS()` function safely

### Medium Priority
- [ ] "Next pass over my location" feature (requires geolocation + orbital math)
- [ ] Glassmorphism card variant for hero data card
- [ ] Share button — deep link with current lat/lon in URL hash
- [ ] Skeleton loading screens instead of "Loading…" text
- [ ] Educational tooltips on hover (e.g., "What is altitude?")
- [ ] Fun facts tooltip/carousel on the ISS marker

### Lower Priority / Nice-to-Have
- [ ] Historical path playback (scrubber to replay track)
- [ ] Day/night terminator overlay on map
- [ ] "ISS is as big as a football field" visual size comparison
- [ ] Screenshot/share image button
- [ ] Comparison card: ISS vs other satellites

---

## 13. Animation Enhancement Ideas (Detailed)

| Element | Current State | Proposed Enhancement |
|---|---|---|
| ISS Marker | Static emoji in circle | Slow CSS rotation + pulsing glow ring |
| Ground Track | Appears instantly | Animate path drawing via SVG `stroke-dasharray` |
| Data Values | Flash via countUp | Odometer/ticker roll animation |
| Card Entrance | `fadeInUp` with delay | Add slight horizontal translate for variety |
| Crew Cards | Hover lift | Flip animation revealing nationality/mission |
| Map Follow | `setView` snap | Smooth `flyTo` with 0.5s ease |
| Toggle Buttons | Color switch | Ripple + scale animation on state change |
| Error Banner | `fadeInUp` | Shake animation on API failure |

---

## 14. Design Goals & Target Audience

**Audience:** M.Sc. Geoinformatics students, space enthusiasts, educators, academic reviewers

**Goals:**
1. Engaging — keeps users curious and exploring
2. Educational — teaches orbital mechanics without overwhelming
3. Professional — academic portfolio quality
4. Modern — contemporary web design (glassmorphism, micro-interactions)
5. Performant — 60fps, fast first paint (<1s), interactive in <2s
6. Accessible — WCAG 2.1 AA compliant (ARIA labels, keyboard nav, contrast ratios)
7. Memorable — stands out from other ISS trackers

**Inspiration:** SpaceX website (clean/dramatic), NASA Eyes on Solar System (interactive/educational), isstracker.pl (colorful path), Google Satellite view (smooth animation)

---

## 15. Performance Targets

| Metric | Target |
|---|---|
| First Paint | < 1 second |
| Time to Interactive | < 2 seconds |
| Animation FPS | 60fps sustained |
| JS Bundle (excl. map tiles) | < 100KB |
| API Response Handling | < 500ms |

---

## 16. Constraints — What Must NOT Change

- Single HTML file architecture (GitHub Pages compatible)
- Current API endpoints (breaking them breaks the live site)
- Responsive design (must work on mobile)
- ARIA accessibility attributes
- Leaflet.js as the mapping library
- No heavy frameworks (no React, Vue, Angular)
- No build process or npm required

---

## 17. Version History

| Version | Status | Notes |
|---|---|---|
| v1.0 | Deployed | Initial tracking with basic map |
| v1.1 | Deployed | Fixed crew API → switched to corquaid endpoint |
| v1.2 | Deployed | Updated to satellite map (Esri World Imagery) |
| v2.0 | In Progress | Full UI/UX enhancement — animations, interactions, polish |

---

## 18. File Reference: Full CSS Key Classes

| Class | Purpose |
|---|---|
| `.header-left` | Logo + title + LIVE badge row |
| `.live-badge` | Green pulsing "LIVE" indicator |
| `.live-dot` | Blinking green circle inside badge |
| `.sdg-badges` | Header SDG chip row (hidden on mobile <580px) |
| `.sdg-chip` | Individual SDG numbered chip button |
| `.facts-banner` | Purple gradient scrolling facts strip |
| `.facts-scroll` | Inner container with `scroll` animation |
| `.main-wrap` | CSS Grid: `340px 1fr` |
| `.side-panel` | Left column flex container |
| `.map-wrap` | Right column flex container |
| `.card` | Standard white card with shadow + hover lift |
| `.data-row` | Label/value pair with hover highlight |
| `.val` | Monospace data value (`.green`, `.blue`, `.orange` modifiers) |
| `.val.updating` | Triggers `countUp` keyframe flash |
| `.orbit-ring` | 130×130px SVG container |
| `.progress-circle` | Blue stroke with `stroke-dashoffset` transition |
| `.crew-grid` | Auto-fill grid for crew cards |
| `.crew-card` | Purple gradient card with initials + name |
| `.map-card` | Map container card with toolbar |
| `.map-toolbar` | Toolbar with title + toggle buttons |
| `.toggle-btn` | Pill-shaped toggle button |
| `.toggle-btn.active` | Blue filled active state |
| `.toast` | Fixed bottom-right notification |
| `.toast.show` | Visible state with `slideInRight` animation |
| `.sdg-section` | Full-width SDG section below map |
| `.sdg-grid` | 4-column SDG card grid (2-col on mobile) |
| `.sdg-card` | Individual SDG card with `::before` icon |
| `#error-banner` | Yellow warning banner (display:none by default) |

---

## 19. Leaflet Map Configuration Summary

```javascript
// Map init
L.map("map", { center: [20, 0], zoom: 3, minZoom: 2, maxZoom: 10 })

// ISS icon: 58×58px, iconAnchor [29,29], popupAnchor [0,-35]
// Track line: cyan #00d4ff, weight 3, opacity 0.8
// Predict line: yellow #ffeb3b, weight 2, opacity 0.7, dashArray "8,6"
// Popup wrapper: purple gradient via .leaflet-popup-content-wrapper override
```

---

## 20. Quick Reference — DOM Element IDs

| ID | Content |
|---|---|
| `#lat` | Latitude value |
| `#lon` | Longitude value |
| `#alt` | Altitude value |
| `#vel` | Velocity value |
| `#vis` | Visibility value |
| `#updated` | Last updated time string |
| `#progressCircle` | SVG orbit ring progress arc |
| `#orbitPercent` | Orbit % text |
| `#orbitCount` | Orbits today count |
| `#timeLeft` | Minutes until orbit complete |
| `#crew-list` | Crew card grid container |
| `#map` | Leaflet map mount point |
| `#error-banner` | API error warning div |
| `#toast` | Toast notification container |
| `#toastIcon` | Toast icon span |
| `#toastTitle` | Toast title div |
| `#toastMessage` | Toast message div |
| `#btn-track` | Ground Track toggle button |
| `#btn-predict` | Trajectory toggle button |
| `#btn-center` | Follow ISS toggle button |

---

*End of context file. This document covers the full project state as of April 2026 and is intended for use as AI context in Antigravity or similar tools to continue development of the ISS Live Tracker v2.0.*
