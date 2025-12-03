# ДЕТАЛЬНЫЙ TIMELINE ПРОЕКТА

## Бюджет и сроки
- **Бюджет клиента**: $3,000 (fixed-price)
- **Ожидаемый timeline клиента**: 1-2 месяца
- **Мой realistic estimate**: 4-6 недель для MVP

---

# ПРЕДЛАГАЕМЫЙ TIMELINE (4-6 НЕДЕЛЬ)

## WEEK 1: Setup, Architecture & Map Engine Foundation
**Deliverable**: Базовый map engine с Xweather интеграцией

### Days 1-2: Project Setup & Architecture
- [ ] Изучить AI-generated код клиента (если предоставлен)
- [ ] Setup dev environment (React/TypeScript/MapLibre)
- [ ] Setup modular architecture:
  - Map engine module
  - Layer manager module
  - Drawing tools module
  - Animation engine module
  - Export module
  - Auth/user module (базовый)
- [ ] Setup GitHub repo, CI/CD basics
- [ ] Create project documentation structure

### Days 3-5: Core Map Engine + Xweather Integration
- [ ] Implement MapLibre base map (1920x1080 fixed)
- [ ] Integrate Xweather API:
  - Get API access working
  - Implement tile layer loading
  - Test with 2-3 basic layers (radar, temperature, satellite)
- [ ] Create layer toggle system
- [ ] Ensure OBS compatibility (no scrollbars, interact works)

### Days 6-7: Layer Manager (First Pass)
- [ ] Implement modular layer configuration
- [ ] Add support for ALL Xweather layers:
  - Radar (composite)
  - Future/forecast radar
  - IR/VIS satellite
  - Snowfall totals
  - Rainfall totals (QPF)
  - Temperature, wind, etc.
- [ ] Create layer control UI
- [ ] Test layer switching performance

**Week 1 Milestone Payment**: $500
**Deliverable**: Working map engine with Xweather layers, OBS-ready layout

---

## WEEK 2: Drawing Tools & Object System
**Deliverable**: Full набор drawing tools с drag/edit functionality

### Days 8-10: Basic Drawing Tools
- [ ] High (H) pressure symbols
- [ ] Low (L) pressure symbols
- [ ] Text annotations
- [ ] Basic shapes (circles, rectangles)
- [ ] Station labels
- [ ] Drag & drop для всех объектов
- [ ] Delete functionality

### Days 11-12: Advanced Drawing Tools (Fronts)
- [ ] Cold front (blue triangles)
- [ ] Warm front (red semicircles)
- [ ] Stationary front
- [ ] Occluded front (если нужен)
- [ ] Curved line support (важно для клиента!)
- [ ] Angle/rotation controls

### Days 13-14: Polygons & Advanced Features
- [ ] Polygon drawing tool
- [ ] Impact zones
- [ ] Warning areas
- [ ] Jet streaks
- [ ] Edit mode для всех объектов
- [ ] Layer ordering (bring to front/back)

**Week 2 Milestone Payment**: $600
**Deliverable**: Complete drawing toolset with edit capabilities

---

## WEEK 3: Animation Engine & Timeline
**Deliverable**: Working animation system synced with Xweather time series

### Days 15-17: Timeline System
- [ ] Timeline UI (play/pause/scrub)
- [ ] Sync timeline to Xweather futurecast timestamps
- [ ] Frame-by-frame navigation
- [ ] Time display (readable format)
- [ ] Speed controls (1x, 2x, etc.)

### Days 18-19: Object Animation (Interpolation)
- [ ] Start/end position system для objects
- [ ] Smooth interpolation (linear + easing options)
- [ ] Animate:
  - H/L pressure systems moving
  - Fronts advancing
  - Polygons shifting
  - Text labels moving
- [ ] Sync overlays with Xweather layer animation

### Days 20-21: Animation Polish
- [ ] Animation preview/scrubbing smoothness
- [ ] Loop functionality
- [ ] Animation settings per object
- [ ] Testing complex scenarios (multiple moving objects)

**Week 3 Milestone Payment**: $700
**Deliverable**: Full animation engine with time-synced layers

---

## WEEK 4: Export, Scene Management & Static Templates (Phase 1)
**Deliverable**: PNG export, scene save/load, первые static templates

### Days 22-23: Export System
- [ ] Export current frame as 1920x1080 PNG
- [ ] Export frame sequence (ZIP of PNGs)
- [ ] Test export качество (high-res, no artifacts)
- [ ] Optional: MP4 export research (ffmpeg-wasm)

### Days 24-25: Scene Save/Load System
- [ ] Save full project state to JSON
- [ ] Load previous scenes
- [ ] Scene library UI
- [ ] Auto-save functionality
- [ ] Import/export scenes

### Days 26-28: Static Template Graphics (First Pass)
⚠️ **КРИТИЧНЫЙ РАЗДЕЛ** - клиент упоминал это, но детали не ясны

- [ ] Clarify requirements with client (ВОПРОСЫ ОБЯЗАТЕЛЬНЫ)
- [ ] Create 2-3 template layouts:
  - 7-day forecast layout
  - Current conditions layout
  - Hourly forecast layout
- [ ] Auto-populate with weather data (city-based)
- [ ] Make templates editable (text, colors, positions)
- [ ] Export templates as PNG

**Week 4 Milestone Payment**: $700
**Deliverable**: Export system, scene management, basic static templates

---

## WEEK 5-6: Auth, Polish, Testing & Extended Features

### Week 5: User Auth & Dashboard (Days 29-33)
- [ ] Simple auth system (login/signup)
- [ ] User dashboard
- [ ] Scene library per user
- [ ] Basic subscription check (can be simple flag)
- [ ] Landing page:
  - Product description
  - Screenshots
  - Pricing table
  - Sign up/login

### Week 6: Polish, Testing & Deployment (Days 34-42)
- [ ] UI/UX polish (clean, broadcasting-ready look)
- [ ] Comprehensive testing:
  - All Xweather layers
  - All drawing tools
  - Animation scenarios
  - Export functionality
  - OBS integration
- [ ] Performance optimization
- [ ] Bug fixes
- [ ] Documentation (user guide)
- [ ] Deploy to production
- [ ] Client training session

**Final Milestone Payment**: $500
**Deliverable**: Fully functional MVP, deployed and ready for use

---

# TIMELINE SUMMARY

| Week | Focus | Milestone Payment | Running Total |
|------|-------|------------------|---------------|
| 1 | Map Engine + Xweather | $500 | $500 |
| 2 | Drawing Tools | $600 | $1,100 |
| 3 | Animation Engine | $700 | $1,800 |
| 4 | Export + Templates | $700 | $2,500 |
| 5-6 | Auth + Polish | $500 | $3,000 |

**Total**: $3,000 over 4-6 weeks

---

# RISK FACTORS & BUFFER TIME

## Potential Delays
1. **Xweather API complexity** (+3-5 days)
   - Если API documentation плохая
   - Если есть rate limits
   - Если нужны additional API endpoints

2. **Static template requirements unclear** (+5-7 days)
   - Клиент упомянул Ventusky Weather Graphics
   - Scope этой части может быть больше чем ожидается
   - **ТРЕБУЕТСЯ CLARIFICATION**

3. **Client revision rounds** (+3-5 days)
   - Нормально для iterative process
   - Клиент сам упомянул: "client changes can add to timeline"

4. **Front curve implementation** (+2-3 days)
   - Клиент специально упомянул: "usually they're more like curved"
   - Может потребовать custom drawing logic

5. **AI prototype integration** (+2-4 days)
   - Если клиент пришлет AI-generated код
   - Нужно будет оценить и интегрировать useful parts

## Buffer Strategy
- **Aggressive timeline**: 4 weeks (28 days) - если все идеально
- **Realistic timeline**: 5 weeks (35 days) - с учетом revisions
- **Safe timeline**: 6 weeks (42 days) - с учетом всех рисков

**Рекомендация для пропозала**: Commit to 5-6 weeks, highlight что может быть faster если scope stays clear.

---

# POST-MVP EXTENSIONS (НЕ ВКЛЮЧЕНО В $3K)

Клиент упомянул:
> "Additional budget available for extended phases (SaaS features, branding tools, user accounts)."

## Potential Phase 2 Features
- Advanced subscription/payment integration (Stripe)
- More static template varieties
- Branding customization (logos, colors, fonts)
- MP4 video export
- Collaboration features (team accounts)
- Weather data from multiple APIs
- Advanced animation curves (bezier)
- Mobile-responsive version
- API for third-party integrations

**Strategy**: Deliver solid MVP first, then discuss Phase 2 scope
