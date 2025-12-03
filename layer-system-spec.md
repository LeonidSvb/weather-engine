# Layer System Technical Specification

## Overview
The layer system is the core architecture that allows users to build custom weather graphics by toggling different visual elements on and off.

---

## Layer Types

### 1. Map Layer (Base)
**Type:** `map`
**Always Visible:** Yes (cannot be disabled)
**Properties:**
```javascript
{
  type: 'map',
  zoom: 4,
  center: [lat, lng],
  style: 'satellite' | 'terrain' | 'street',
  projection: '2d' | '3d'
}
```

**What it does:**
- Interactive Leaflet/Mapbox map
- Pan and zoom
- Choose map style
- Optional 3D tilt

---

### 2. Weather Layers
**Type:** `weather`
**Toggleable:** Yes
**Sub-types:**
- Radar (precipitation)
- Satellite (cloud cover)
- Temperature overlay
- Wind patterns

**Properties:**
```javascript
{
  type: 'weather',
  source: 'radar' | 'satellite' | 'temperature',
  opacity: 0.7,
  animated: true,
  timeRange: { start: Date, end: Date }
}
```

**What it does:**
- Overlay weather data from APIs
- Can be animated (radar loops)
- Adjustable transparency
- Multiple weather layers can be active

---

### 3. Graphic Overlay Layers
**Type:** `graphic`
**Toggleable:** Yes
**Sub-types:**
- Upper third (title area)
- Lower third (name/branding area)
- Full-screen templates

**Properties:**
```javascript
{
  type: 'graphic',
  position: 'upper-third' | 'lower-third' | 'full',
  template: 'theme-1-upper',
  content: {
    title: 'WEATHER FORECAST',
    subtitle: 'Saturday Evening',
    logo: 'url-to-logo.png'
  },
  theme: 'professional-blue'
}
```

**What it does:**
- SVG-based graphics that overlay the map
- Editable text fields
- Theme-styled (colors, fonts)
- Can include logos

**Visual Example:**
```
┌─────────────────────────────────────────┐
│ [LOGO] SATURDAY FORECAST      8:00 PM   │ ← Upper Third Layer
├─────────────────────────────────────────┤
│                                         │
│         (Weather Map Here)              │ ← Map + Weather Layers
│                                         │
├─────────────────────────────────────────┤
│ JOHN SMITH | Meteorologist | WXYZ 10   │ ← Lower Third Layer
└─────────────────────────────────────────┘
```

---

### 4. Drawing Layers
**Type:** `drawing`
**Toggleable:** Yes
**Sub-types:**
- Cold fronts
- Warm fronts
- Pressure systems (H/L)
- Weather symbols
- Custom text annotations

**Properties:**
```javascript
{
  type: 'drawing',
  elements: [
    {
      kind: 'cold-front',
      points: [[lat1, lng1], [lat2, lng2], ...],
      style: { color: '#0066FF', width: 3 }
    },
    {
      kind: 'pressure-high',
      position: [lat, lng],
      label: 'H',
      style: { color: '#FF0000', size: 'large' }
    }
  ]
}
```

**What it does:**
- User-drawn weather features
- Curved bezier lines for fronts
- Draggable symbols
- Each drawing can be edited/deleted

---

### 5. Text Layers
**Type:** `text`
**Toggleable:** Yes

**Properties:**
```javascript
{
  type: 'text',
  position: [x, y],
  content: 'Severe Weather Warning',
  style: {
    font: 'Impact',
    size: 48,
    color: '#FFFFFF',
    stroke: '#000000',
    shadow: true
  }
}
```

**What it does:**
- Free-form text anywhere on map
- Customizable styling
- Draggable position

---

## Layer Management UI

### Sidebar Panel Design

```
┌─────────────────────────────┐
│ LAYERS                      │
├─────────────────────────────┤
│ ☑ Base Map                  │ (locked)
│   └─ Style: Satellite ▾     │
│                             │
│ ☑ Weather                   │
│   ├─ ☑ Radar       [70%] ━━━│ (opacity slider)
│   ├─ ☐ Satellite   [80%] ━━━│
│   └─ ☐ Temperature [60%] ━━━│
│                             │
│ ☑ Graphics                  │
│   ├─ ☑ Upper Third    [✎]  │ (edit button)
│   └─ ☑ Lower Third    [✎]  │
│                             │
│ ☑ Drawings                  │
│   ├─ ☑ Cold Front 1   [🗑]  │ (delete button)
│   ├─ ☑ Warm Front 1   [🗑]  │
│   └─ ☑ High Pressure  [🗑]  │
│                             │
│ ☑ Text Annotations          │
│   └─ ☑ Title Text     [✎]  │
│                             │
└─────────────────────────────┘
```

### Controls:
- **Checkbox:** Toggle layer on/off
- **Opacity Slider:** For weather layers
- **Edit Button [✎]:** Open text editor
- **Delete Button [🗑]:** Remove drawing/text
- **Drag Handle:** Reorder layers (changes z-index)

---

## Export Behavior

### Single Frame Export (PNG)

**User clicks "Export PNG"**

**Dialog appears:**
```
┌─────────────────────────────────┐
│ Export Settings                 │
├─────────────────────────────────┤
│ Format:                         │
│ ○ Horizontal (1920x1080)        │
│ ● Vertical (1080x1920)          │
│                                 │
│ Quality:                        │
│ ● High (PNG)                    │
│ ○ Medium (JPG 90%)              │
│                                 │
│ Include:                        │
│ ☑ All visible layers            │
│                                 │
│ [Cancel]  [Export]              │
└─────────────────────────────────┘
```

**Process:**
1. Create canvas at target resolution
2. Render layers in order (bottom to top):
   - Map
   - Weather layers
   - Drawings
   - Graphics (upper/lower thirds)
   - Text
3. Export to PNG
4. Download file

---

### Video/Animation Export

**User clicks "Export Animation"**

**Options:**
```
┌─────────────────────────────────┐
│ Export Animation                │
├─────────────────────────────────┤
│ Type:                           │
│ ● Screen Recording (WebM)       │
│ ○ Frame Sequence (PNG series)   │
│                                 │
│ Duration: [___5___] seconds     │
│                                 │
│ Format:                         │
│ ○ Horizontal (1920x1080)        │
│ ● Vertical (1080x1920)          │
│                                 │
│ [Cancel]  [Start Recording]     │
└─────────────────────────────────┘
```

**Process (Screen Recording):**
1. Start MediaRecorder on canvas
2. User clicks "Play" on timeline
3. Records 5 seconds of animation
4. Stops, downloads WebM file

**Process (Frame Sequence):**
1. Render each frame of timeline
2. Export as numbered PNGs (frame_001.png, frame_002.png, ...)
3. User can combine in video editor or FFmpeg

---

## Theme System Integration

### How Themes Work with Layers

**Theme Definition:**
```javascript
const theme = {
  id: 'professional-blue',
  name: 'Professional Blue',

  assets: {
    upperThird: 'themes/prof-blue/upper.svg',
    lowerThird: 'themes/prof-blue/lower.svg'
  },

  styles: {
    colors: {
      primary: '#0066FF',
      secondary: '#003366',
      accent: '#00CCFF',
      text: '#FFFFFF'
    },
    fonts: {
      heading: 'Impact',
      body: 'Arial',
      accent: 'Roboto Condensed'
    },
    effects: {
      textShadow: '2px 2px 4px rgba(0,0,0,0.8)',
      glow: true
    }
  }
}
```

**When user selects a theme:**
1. Load SVG graphics for upper/lower thirds
2. Apply color scheme to text layers
3. Apply font choices
4. Update drawing styles (cold front color, etc.)

**User can still customize:**
- Edit text in graphics
- Toggle graphics on/off
- Mix theme elements

---

## Template System

### Pre-built Templates

Templates are **preset layer configurations** that users can load.

**Template Definition:**
```javascript
const template = {
  id: 'current-conditions',
  name: 'Current Conditions',
  aspectRatio: '16:9',

  layers: [
    {
      type: 'map',
      zoom: 5,
      center: [40.7128, -74.0060],
      style: 'satellite'
    },
    {
      type: 'weather',
      source: 'radar',
      opacity: 0.7,
      enabled: true
    },
    {
      type: 'graphic',
      position: 'upper-third',
      template: 'theme-1-upper',
      content: {
        title: 'CURRENT CONDITIONS',
        subtitle: 'As of 8:00 PM'
      }
    },
    {
      type: 'graphic',
      position: 'lower-third',
      template: 'theme-1-lower',
      content: {
        name: 'Your Name',
        station: 'Your Station'
      }
    }
  ]
}
```

**Templates to Build:**

**1. Current Conditions**
- Map + radar
- Upper third: "Current Conditions" + time
- Lower third: Broadcaster name
- Users can add temperature labels

**2. 7-Day Forecast**
- Map background (zoomed out to show region)
- Upper third: "7-Day Forecast"
- Custom graphic: 7-day layout overlay
- Lower third: Name

**3. Radar Loop**
- Clean map
- Animated radar layer
- Minimal text (just title)
- Good for social media

**4. Blank Canvas**
- Just map
- No overlays
- User builds from scratch

**5. Social Media Vertical**
- 9:16 aspect ratio
- Centered map
- Simple text overlays
- No heavy graphics (like Instagram example)

---

## Technical Implementation

### State Management

**Redux/Zustand Store:**
```javascript
{
  canvas: {
    width: 1920,
    height: 1080,
    aspectRatio: '16:9'
  },

  layers: [
    { id: 'layer-1', type: 'map', ... },
    { id: 'layer-2', type: 'weather', ... },
    { id: 'layer-3', type: 'graphic', ... }
  ],

  activeTheme: 'professional-blue',

  timeline: {
    currentTime: 0,
    duration: 300, // 5 minutes
    playing: false
  }
}
```

**Actions:**
- `addLayer(layer)`
- `removeLayer(id)`
- `toggleLayer(id)`
- `updateLayer(id, props)`
- `reorderLayers(fromIndex, toIndex)`

---

### Rendering Pipeline

**On every frame:**
1. Clear canvas
2. For each layer (ordered by z-index):
   ```javascript
   if (layer.enabled) {
     if (layer.type === 'map') renderMap()
     if (layer.type === 'weather') renderWeather(layer)
     if (layer.type === 'graphic') renderGraphic(layer)
     if (layer.type === 'drawing') renderDrawing(layer)
     if (layer.type === 'text') renderText(layer)
   }
   ```
3. Render UI controls on top

---

### Component Architecture (React Example)

```jsx
<App>
  <Sidebar>
    <LayerPanel layers={layers} />
    <ThemeSelector themes={themes} />
    <TemplateSelector templates={templates} />
    <ExportPanel />
  </Sidebar>

  <Canvas>
    <MapLayer />
    {layers.map(layer => (
      <Layer key={layer.id} {...layer} />
    ))}
    <DrawingTools />
  </Canvas>

  <Timeline>
    <Scrubber />
    <PlaybackControls />
  </Timeline>
</App>
```

---

## User Workflow Examples

### Example 1: Quick Social Media Post
1. Select "Social Media Vertical" template
2. Map auto-loads in 9:16
3. Toggle on radar layer
4. Add text: "Storm approaching tonight"
5. Click "Export PNG"
6. Post to Instagram story ✅

### Example 2: Broadcast Forecast
1. Select "7-Day Forecast" template
2. Map loads with forecast overlay
3. Edit text in lower third (add name)
4. Upload station logo
5. Draw cold front on map
6. Export 16:9 PNG
7. Import to broadcast software ✅

### Example 3: Custom Radar Loop
1. Start with "Blank Canvas"
2. Add radar layer
3. Set timeline to 2 hours
4. Add text "Evening Radar"
5. Click "Export Animation"
6. Download WebM video
7. Share on social media ✅

---

## Performance Considerations

### Optimization Strategies:

**1. Layer Caching**
- Cache rendered map tiles
- Only re-render layers that changed
- Use offscreen canvas for heavy layers

**2. Debouncing**
- Debounce slider changes (opacity)
- Throttle map pan/zoom events

**3. Lazy Loading**
- Load weather data only for visible timeframe
- Load theme assets on demand

**4. Export Optimization**
- Render at target resolution (don't scale down)
- Use Web Workers for heavy processing
- Show progress indicator for long exports

---

## Future Enhancements (Phase 2)

### Advanced Layer Features:
- Layer groups (organize related layers)
- Layer blending modes (multiply, screen, etc.)
- Layer effects (blur, glow, etc.)
- Layer animations (fade in/out, slide)

### Collaboration:
- Share layer configurations
- Template marketplace
- User-uploaded themes

### Advanced Export:
- MP4 video export (via FFmpeg)
- GIF export for social media
- Scheduled auto-export (for live updates)

---

## Questions & Decisions Needed

1. **Default Themes:** Should we create themes for specific broadcast styles (news, weather channel, local station)?

2. **Layer Limits:** Any limit on number of layers? (Recommend max 20 for performance)

3. **Weather Data Sources:** Preference for radar API? (RainViewer free, Xweather paid but better)

4. **Save/Load:** Should users be able to save layer configurations for reuse?

5. **Collaboration:** Need multi-user editing? Or single user for MVP?

---

This layer system gives users **maximum flexibility** while keeping the UI simple. Toggle what you need, export what you see.
