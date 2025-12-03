# Updated Project Plan
## Based on Client Answers (Dec 3, 2025)

### Client's Decisions ✅

**Budget:** YES - Can hire designer for 3-5 days
**Themes:** 2-3 themes (good variety)
**Maps:** Primarily 2D, possibly one 3D option (2D is priority)
**Timeline:** Extra 1-2 weeks for polish (considering vacation schedule)

---

## New Requirements from Latest Discussion

### Core Concept: Layer-Based System
The client wants a **modular layer system** where users can toggle different elements on/off:

**Layout Structure:**
```
┌─────────────────────────────────┐
│  Upper 1/3: Title Text + Theme  │ ← Toggle on/off
├─────────────────────────────────┤
│                                 │
│   Main Viewing Window           │
│   (Map + Weather Graphics)      │
│                                 │
├─────────────────────────────────┤
│  Lower 1/3: Name + Graphics     │ ← Toggle on/off
└─────────────────────────────────┘
```

### Key Features Requested:

**1. Layered Elements (Toggle On/Off)**
- Upper 1/3 graphic overlay (title text area)
- Lower 1/3 graphic overlay (broadcaster name, sponsor logo)
- Weather map layers (satellite, radar, etc.)
- Text layers (editable)
- Weather symbols (H, L, fronts, etc.)

**2. Content Types**
- Interactive map graphics (like the demo)
- Current conditions template
- 7-day forecast template
- Custom text overlays

**3. Export Options**
- PNG export (single frame)
- Screen recording for social media
- Both 16:9 (broadcast) and 9:16 (vertical/social)

**4. Reference Style**
- Instagram Reel example: Vertical format, mostly map, minimal theme, overlay text
- Professional broadcast examples: Full themed layouts

---

## Revised Technical Architecture

### Layer System Implementation

**Layer Types:**
```javascript
{
  layers: [
    {
      id: 'map-base',
      type: 'map',
      enabled: true,
      locked: false
    },
    {
      id: 'weather-radar',
      type: 'weather',
      enabled: true,
      opacity: 0.7
    },
    {
      id: 'upper-third',
      type: 'graphic',
      template: 'theme-1-upper',
      enabled: true,
      content: {
        title: 'WEATHER FORECAST',
        subtitle: 'Saturday Morning'
      }
    },
    {
      id: 'lower-third',
      type: 'graphic',
      template: 'theme-1-lower',
      enabled: true,
      content: {
        name: 'John Smith',
        station: 'Weather Channel 10'
      }
    },
    {
      id: 'fronts',
      type: 'drawing',
      enabled: true,
      elements: [/* cold fronts, warm fronts */]
    }
  ]
}
```

**UI Controls:**
```
Sidebar Panel:
├─ Layers
│  ├─ ☑ Upper Third
│  ├─ ☑ Lower Third
│  ├─ ☑ Map
│  ├─ ☑ Radar
│  └─ ☑ Fronts/Symbols
│
├─ Edit Text
│  ├─ Title: [              ]
│  ├─ Name:  [              ]
│  └─ Custom: [             ]
│
└─ Export
   ├─ [PNG 16:9]
   ├─ [PNG 9:16]
   └─ [Record Video]
```

---

## Updated Milestone Breakdown

### Milestone 1: Core Map Engine (Week 1)
**Duration:** 5-7 days
**Deliverable:** Working 2D map with weather layer support

**Features:**
- Leaflet-based interactive map
- Map controls (zoom, pan)
- Weather API integration (RainViewer for radar)
- Basic layer system architecture
- Toggle layers on/off

**Technical Stack:**
- Leaflet.js for 2D maps
- RainViewer API (free radar)
- React/Vue for UI (or vanilla JS if preferred)

---

### Milestone 2: Drawing Tools + Layer System (Week 2)
**Duration:** 5-7 days
**Deliverable:** Full drawing toolkit with layer management

**Features:**
- Draw curved cold/warm fronts with bezier curves
- Add H/L pressure markers
- Add weather symbols (rain, snow, etc.)
- Text tool for custom annotations
- Each tool creates a layer
- Layer panel with toggle/delete/reorder

**Technical Stack:**
- Fabric.js or Konva.js for canvas drawing
- Custom bezier curve editor
- Layer state management

---

### Milestone 3: Theme System + Graphic Overlays (Week 2-3)
**Duration:** 5-7 days
**Deliverable:** 2-3 professional themes with upper/lower third graphics

**Design Phase (Overlapping):**
- **Designer creates (3 days):**
  - 2-3 theme designs
  - Upper third templates (title area)
  - Lower third templates (name/logo area)
  - Color schemes
  - Typography rules
  - Spacing guidelines

**Development:**
- SVG-based graphic overlays (upper/lower thirds)
- Editable text fields
- Theme switching system
- Logo upload functionality
- Sponsor logo support

**Themes Structure:**
```
Theme 1: "Professional Blue"
├─ upper-third.svg (title + branding)
├─ lower-third.svg (name + station)
└─ styles.json (colors, fonts)

Theme 2: "Storm Alert"
├─ upper-third.svg
├─ lower-third.svg
└─ styles.json

Theme 3: "Clean Minimal"
├─ upper-third.svg
├─ lower-third.svg
└─ styles.json
```

---

### Milestone 4: Timeline Animation Engine (Week 3-4)
**Duration:** 10-14 days
**Deliverable:** Animated weather sequences

**Features:**
- Timeline scrubber
- Keyframe system
- Animate radar loops
- Animate fronts moving
- Playback controls
- Export as frame sequence

**Technical Stack:**
- GSAP for smooth animations
- Frame-by-frame rendering
- Timeline state management

---

### Milestone 5: Export Engine (Week 4-5)
**Duration:** 5-7 days
**Deliverable:** Export to PNG and video formats

**Features:**
- **16:9 Export** (1920x1080 broadcast)
- **9:16 Export** (1080x1920 social/vertical)
- Single frame PNG
- Frame sequence for video
- Screen recording integration (if browser supports)

**Technical Stack:**
- html2canvas for PNG export
- Canvas rendering at specific resolutions
- MediaRecorder API for video capture
- FFmpeg integration (optional, for high-quality video)

---

### Milestone 6: Template System (Week 5)
**Duration:** 3-5 days
**Deliverable:** Pre-built templates for common use cases

**Templates:**
1. **Current Conditions**
   - Map with radar
   - Temperature overlays
   - Current conditions text

2. **7-Day Forecast**
   - Map background
   - 7-day layout overlay
   - Editable daily data

3. **Satellite/Radar Loop**
   - Clean map
   - Animated radar
   - Minimal text

4. **Custom Blank**
   - Just map + tools
   - User builds from scratch

---

### Milestone 7: Polish + OBS Mode (Week 5-6)
**Duration:** 5-7 days
**Deliverable:** Production-ready app with OBS integration

**Features:**
- Login system (simple auth)
- Save/load projects
- OBS Browser Source mode (fixed 1920x1080)
- Performance optimization
- Bug fixes and polish
- User testing feedback implementation

---

## Designer Collaboration Timeline

### Designer Tasks (3-5 days, can overlap with dev)

**Days 1-2: Design Phase**
- Create 2-3 theme concepts
- Design upper third graphics
- Design lower third graphics
- Create style guide

**Day 3: Review & Iteration**
- Client review
- Adjustments based on feedback

**Days 4-5: Asset Preparation**
- Export SVG files
- Provide color codes
- Font files
- Handoff to developer

**Best Timing:**
- Start designer during Week 2 (while I build core engine)
- Designer delivers by end of Week 2
- I implement themes in Week 3

---

## Realistic Timeline

### 5-Week Plan (Recommended)

**Week 1 (Dec 9-13):**
- Core map engine
- Basic weather layers
- Layer toggle system

**Week 2 (Dec 16-20):**
- Drawing tools (fronts, symbols, text)
- **Designer starts** (3 days)
- Layer management UI

**Week 3 (Dec 23-27):**
- Theme system implementation
- Upper/lower third graphics
- Designer assets integration
- *(Some holidays, adjusted schedule)*

**Week 4 (Dec 30 - Jan 3):**
- Timeline animation
- Template system
- Export PNG (both formats)

**Week 5 (Jan 6-10):**
- Video export/recording
- OBS mode
- Polish & testing
- **LAUNCH READY**

**Buffer (Jan 13-17):**
- Bug fixes
- User feedback
- Final polish

---

## 6-Week Plan (Safer, includes buffer)

Same as above, but:
- Week 5-6: More testing, edge cases, polish
- Week 6: Launch with confidence
- Vacation after Week 6 ✈️

---

## What We Need from You

### Immediate (This Week):
1. **Approve this plan** - Any changes needed?
2. **Designer contact** - Do you have one, or should I recommend?
3. **Branding assets:**
   - Your logo (PNG/SVG)
   - Preferred color scheme (if any)
   - Any specific fonts?

### Week 2:
4. **Design review** - Approve designer's theme concepts
5. **Template priorities** - Which templates are most important?

### Week 4:
6. **Testing feedback** - Try the app, report bugs
7. **Content samples** - Sample weather data for testing

---

## Technical Decisions Based on Your Answers

### Maps: 2D Priority ✅
**Implementation:**
- Use **Leaflet.js** as primary engine (free, fast, simple)
- Add **Mapbox GL** as optional "3D mode" toggle (for one fancy theme)
- 2D will be faster, clearer, easier to export

**Cost:** Leaflet = Free, Mapbox = $0-25/month (free tier covers MVP)

---

### Layer System ✅
**This is the RIGHT approach** - Here's why:
- Users can customize exactly what they want
- Easy to add new layers later
- Simple UI (checkboxes)
- Export what you see
- Perfect for both simple (Instagram) and complex (broadcast) use

---

### Two Format Support (16:9 + 9:16) ✅
**Implementation:**
- Single canvas/workspace
- Export button offers:
  - "Export Horizontal (1920x1080)"
  - "Export Vertical (1080x1920)"
- Themes automatically adjust to aspect ratio
- Designer creates both orientations for upper/lower thirds

---

### Screen Recording ✅
**Implementation Options:**

**Option A: Browser MediaRecorder (Easy)**
```javascript
// Built-in browser recording
const stream = canvas.captureStream(30); // 30fps
const recorder = new MediaRecorder(stream);
```
- Pros: No setup, works in browser
- Cons: Quality depends on browser, limited formats

**Option B: Frame Sequence + FFmpeg (Better)**
```javascript
// Export PNG sequence
// User combines in video editor or we use FFmpeg
```
- Pros: Perfect quality, full control
- Cons: Slightly more complex workflow

**Recommendation:** Start with Option A, add Option B if needed.

---

## Cost Breakdown

### Development Time: 5-6 weeks
*(Your existing agreement with Leonid)*

### Designer: 3-5 days
**Estimated:** $500-1500 depending on designer
- 3 days @ $150-300/day = $450-900
- OR
- Flat rate for 2-3 themes = $800-1200

**Deliverables:**
- 2-3 complete theme designs
- Upper/lower third graphics (SVG)
- Style guide
- Font/color specifications

### Tools/Services (Monthly):
- **Mapbox** (optional 3D): $0-25/month
- **Xweather API** (premium weather): $0-50/month (can start free)
- **Hosting**: $5-10/month
- **Domain**: $12/year

**Total Monthly After Launch:** ~$20-50/month
*(Can start with free tiers)*

---

## Risk Mitigation

### Risk 1: Holiday Schedule
**Mitigation:**
- Front-load critical work (Weeks 1-3)
- Designer works during your availability
- Week 4 can be lighter (animation polish)
- Buffer week if needed

### Risk 2: Designer Availability
**Mitigation:**
- Need designer commitment by next week
- I can recommend freelancers if needed
- Alternative: Use AI-generated designs + Canva (cheaper but less custom)

### Risk 3: Scope Creep
**Mitigation:**
- This plan is LOCKED ✅
- Any new features → Phase 2 (after launch)
- Focus: MVP that works beautifully

---

## Success Criteria

### MVP Must Have:
✅ 2D interactive map with weather layers
✅ Drawing tools (fronts, symbols, text)
✅ 2-3 professional themes
✅ Upper/lower third graphics (toggle on/off)
✅ Editable text fields
✅ PNG export (16:9 and 9:16)
✅ Basic animation/timeline
✅ Layer management system
✅ Current conditions + 7-day forecast templates

### Nice to Have (Phase 2):
- Advanced animation keyframes
- More themes
- 3D map option
- Video export with FFmpeg
- User accounts with cloud save
- Template marketplace

---

## Next Steps

### This Week:
1. **You:** Review and approve this plan
2. **You:** Find designer OR let me know if you want recommendations
3. **You:** Send branding assets (logo, colors)
4. **Me:** Set up project repository
5. **Me:** Start Week 1 tasks (map engine)

### By End of Week 1:
6. **Demo:** Working map with weather layers you can test
7. **Designer:** Kickoff meeting with designer
8. **Milestone:** First demo you can show to potential customers

### By End of Week 2:
9. **Demo:** Drawing tools working
10. **Designer:** Initial theme concepts ready for review
11. **Milestone:** Core functionality complete

---

## Questions for You

1. **Designer:** Do you have someone in mind, or want me to recommend a few freelancers I've worked with?

2. **Branding:** Do you have existing brand colors/logo, or is this a fresh start?

3. **Priority:** If we had to pick ONE template to perfect first, would it be:
   - Current conditions?
   - 7-day forecast?
   - Free-form map graphics?

4. **Instagram Reel:** Can you share that reel link again? I want to study the vertical layout style.

5. **Launch Date:** Is there a hard deadline, or flexible "early January"?

---

## My Commitment

I'm committed to:
- 5-6 week timeline
- 2-3 professional themes
- Layer-based system that's intuitive
- Export quality that's broadcast-ready
- Weekly demos so you see progress
- Before New Year vacation: Core functionality done ✅

Let's build something weather broadcasters will love!

Ready to start as soon as you approve this plan.

— Leonid
