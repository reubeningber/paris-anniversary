# AI Coding Instructions for Paris Anniversary Itinerary

This is a **self-contained mobile-first travel website** for a specific Paris anniversary trip (Oct 9-14, 2025). It consists of static HTML files with embedded CSS/JS and interactive Leaflet maps.

## Project Architecture

### Core Structure
- **`index.html`** - Main itinerary with accordion-style daily plans and embedded maps
- **`photo-routes.html`** - Two curated walking photo routes from the hotel
- **`running-routes.html`** - Two scenic ~5km running routes from the hotel
- **`README.md`** - Minimal project description

### Key Design Patterns

#### **Self-Contained Philosophy**
- Each HTML file is completely standalone - no external CSS/JS files
- All styles embedded in `<style>` tags using CSS custom properties (`:root` variables)
- All JavaScript embedded inline with dependencies loaded from CDN
- **Critical**: When adding features, maintain this self-contained approach

#### **Mobile-First Responsive Design**
- Uses CSS custom properties for theming: `--bg`, `--card`, `--muted`, `--text`, `--accent`
- Responsive grid using `clamp()`, `grid-template-columns`, and media queries
- Sticky headers with backdrop blur effects
- **Pattern**: Always test layouts at mobile sizes first

#### **Interactive Maps with Leaflet**
```javascript
// Standard map initialization pattern used across all files
const map = L.map(elId, {scrollWheelZoom: false}).setView([hotel.lat, hotel.lon], 13);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {...}).addTo(map);
```
- **Hotel-centric**: All routes start/end at "Hotel Maison Hamelin" (48.8641, 2.2889)
- Maps are lazy-loaded and cached to avoid performance issues
- **Important**: Disable scroll wheel zoom for mobile usability

#### **Accordion UI Pattern**
```html
<details data-day="day1">
  <summary>Day Title <span class="tag">Category</span></summary>
  <div class="body">Content + Map + Buttons</div>
</details>
```
- Only one accordion open at a time (JavaScript enforced)
- Maps initialize when accordion opens to save resources

### Content Conventions

#### **Time Format**: Always use 12-hour format with AM/PM (e.g., "9:30 AM")
#### **Location Links**: 
- Google Maps routes: `https://www.google.com/maps/dir/?api=1&origin=...&destination=...&waypoints=...`
- External venues: Target `_blank` with full URLs
#### **Tags**: Use for categorization (e.g., `<span class="tag">Booked ✅</span>`)

### Development Workflow

#### **No Build Process**
- Direct file editing - no compilation, bundling, or preprocessing
- Test by opening files directly in browser
- Deploy by pushing to GitHub Pages (serves static files directly)

#### **Adding New Features**
1. **Maps**: Follow the coordinate pattern in existing files - define lat/lon objects, then pass to `buildMap()` function
2. **Styling**: Add to the embedded `<style>` tag using existing CSS custom properties
3. **Navigation**: Maintain the header nav pattern with `.btn` classes for consistency

#### **External Dependencies**
- **Leaflet**: `https://unpkg.com/leaflet@1.9.4/dist/leaflet.css` and `.js`
- **Fonts**: System font stack only (`system-ui, -apple-system, Segoe UI, Inter, Roboto, Arial`)
- **No frameworks**: Pure vanilla JavaScript and CSS

### Code Style

#### **CSS**: 
- Minified custom properties in `:root`
- Mobile-first media queries
- Use `clamp()` for responsive typography

#### **JavaScript**:
- Vanilla JS with `DOMContentLoaded` event listeners
- Arrow functions and modern ES6+ syntax
- Coordinate objects pattern: `{name: "Location", lat: 48.xxxx, lon: 2.xxxx}`

### Critical Implementation Notes

- **Maps Performance**: Use lazy initialization and `invalidateSize()` when showing/hiding
- **Mobile UX**: Disable map scroll zoom, use touch-friendly button sizes
- **Content Updates**: All trip details are hardcoded - update HTML directly for changes
- **GitHub Pages**: Repository is configured for static hosting - no server-side processing

When making changes, preserve the intimate, personal nature of this travel site while maintaining mobile usability and the self-contained architecture.