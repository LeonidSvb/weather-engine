# РИСКИ И ПОДВОДНЫЕ КАМНИ

## 🔴 КРИТИЧЕСКИЕ РИСКИ

### 1. Static Template Graphics - Неясный Scope
**Уровень риска**: ВЫСОКИЙ ⚠️⚠️⚠️

**Проблема**:
- В оригинальном job posting **минимальные детали** про static templates
- В звонке клиент показал Ventusky Weather Graphics (сотни разных layouts)
- Неясно сколько templates нужно
- Неясно насколько кастомизируемые должны быть
- Это может быть 20% проекта или 50% проекта

**Что клиент сказал**:
> "This dude puts together these graphics, which are actually pretty impressive, but he does them in like Photoshop."

> "It would be cool to like do something like this, whether it's designing our own layout template or contacting him about some sort of license."

> "So it would be cool to like do something like this... some of these slides that people could like edit."

**Impact**:
- Может добавить 1-2 недели к timeline
- Может потребовать designer для layouts
- Может быть отдельный проект сам по себе

**Mitigation**:
- ✅ В пропозале четко ограничить scope: "2-3 basic templates for MVP"
- ✅ Спросить client КОНКРЕТНО сколько templates нужно для MVP
- ✅ Предложить templates как Phase 2 (после map engine работает)

---

### 2. Xweather API - Unknown Complexity
**Уровень риска**: СРЕДНЕ-ВЫСОКИЙ ⚠️⚠️

**Проблема**:
- Я не работал с Xweather API раньше
- API documentation может быть плохой
- Могут быть rate limits
- Не все layers могут быть доступны через один endpoint
- Некоторые advanced layers могут требовать premium subscription

**Что может пойти не так**:
- Future radar может быть доступен только через отдельный API
- Time-series данные могут иметь странный format
- Tile servers могут быть медленными
- API могут меняться (deprecated endpoints)

**Impact**:
- +3-5 дней на Milestone 1
- Возможна необходимость использовать fallback API

**Mitigation**:
- ✅ Попросить клиента предоставить Xweather API credentials ASAP
- ✅ Потратить первые 1-2 дня на API exploration
- ✅ Если API problematic - обсудить alternatives (OpenWeather, Weather.gov)
- ✅ В пропозале упомянуть: "pending Xweather API access and documentation review"

---

### 3. Animation Performance - Technical Challenge
**Уровень риска**: СРЕДНЕ-ВЫСОКИЙ ⚠️⚠️

**Проблема**:
- Animating tiled map layers + custom objects + timeline = тяжелая нагрузка
- Browser может лагать при большом количестве objects
- OBS Browser Source имеет performance limitations
- 1920x1080 high-res rendering может быть медленным

**Что может пойти не так**:
- Animation stutters (не плавная)
- High CPU usage в OBS
- Frame drops во время broadcast
- Export занимает слишком долго

**Impact**:
- +2-4 дня на optimization
- Может потребовать WebGL optimization
- Может потребовать ограничить количество animated objects

**Mitigation**:
- ✅ Use Canvas rendering где possible
- ✅ Implement layer caching
- ✅ Lazy load tiles
- ✅ Test performance early (Milestone 1)
- ✅ Set realistic limits (max 20 objects, max 50 timeline frames)

---

## 🟡 СРЕДНИЕ РИСКИ

### 4. Client's AI-Generated Code - Integration Unknown
**Уровень риска**: СРЕДНИЙ ⚠️

**Проблема**:
- Клиент упомянул: "ChatGPT says that it's provided 60% of the stuff"
- Неизвестно качество кода
- Может быть написан на другом stack
- Может иметь bugs или incomplete features
- Клиент сказал что загрузит в post, но пока не загрузил

**Impact**:
- Если код useful: может сэкономить 3-5 дней
- Если код problematic: может добавить 2-3 дня (refactoring)
- Если код unusable: игнорируем и строим с нуля (мой demo уже работает)

**Mitigation**:
- ✅ Попросить код immediately после hire
- ✅ Потратить 1 день на review
- ✅ Использовать только useful parts
- ✅ Не чувствовать obligation использовать плохой код

---

### 5. Curved Front Lines - Technical Implementation
**Уровень риска**: СРЕДНИЙ ⚠️

**Проблема**:
Клиент специально упомянул:
> "Now the cold fronts and the warm fronts, usually they're more like curved and you would need to angle them in such a manner. So that would need some adjustments."

- Мое demo имеет straight lines
- Curved lines с symbols (triangles/semicircles) вдоль curve = нетривиально
- Нужны bezier curves или spline interpolation
- Symbols нужно rotate по tangent линии

**Impact**:
- +2-3 дня на Milestone 2
- Может потребовать canvas manipulation вместо simple SVG

**Mitigation**:
- ✅ Research existing libraries (fabric.js, paper.js, konva.js)
- ✅ Показать клиенту prototype curved fronts рано (week 2)
- ✅ Если слишком сложно - предложить simplified version для MVP

---

### 6. Export Quality - PNG/MP4 Rendering
**Уровень риска**: СРЕДНИЙ ⚠️

**Проблема**:
- Exporting canvas/WebGL to PNG может иметь artifacts
- 1920x1080 high-res export может быть медленным
- MP4 export в browser = challenging (ffmpeg-wasm)
- OBS может render по-другому чем browser export

**Impact**:
- Export может выглядеть не так качественно как on-screen
- MP4 export может не уместиться в Milestone 4 timeline

**Mitigation**:
- ✅ Use html2canvas или dom-to-image для PNG
- ✅ Test export quality early
- ✅ MP4 export как "optional" (не critical для MVP)
- ✅ Клиент может использовать external tools (OBS record) если export проблематичен

---

## 🟢 НИЗКИЕ РИСКИ

### 7. Client Burned Before - Trust Issues
**Уровень риска**: НИЗКИЙ 🟢

**Проблема**:
Клиент сказал:
> "I've had a lot of burned projects on this platform... a lot of people that say they're capable, then they're not."

> "I just want somebody that's confident in it and knows what they're doing."

**Impact**:
- Клиент может быть skeptical
- Может требовать много check-ins
- Может быть осторожным с milestone approvals

**Mitigation**:
- ✅ Я уже показал working demo - это ОГРОМНЫЙ trust builder
- ✅ Over-communicate (weekly updates)
- ✅ Under-promise, over-deliver
- ✅ Deliver milestones on time
- ✅ Video walkthroughs для каждого milestone

---

### 8. Timezone Difference
**Уровень риска**: ОЧЕНЬ НИЗКИЙ 🟢

**Проблема**:
- Клиент: Minneapolis (CST - UTC-6)
- Я: Bali (UTC+8)
- 14 hours difference

**Impact**:
- Real-time collaboration limited
- Calls только утро для него (ночь для меня)

**Mitigation**:
- ✅ Async communication (works fine)
- ✅ Scheduled calls 1x/week (я сказал 3am ok)
- ✅ Detailed updates via Upwork messaging
- ✅ Video demos для async review

---

### 9. Authentication Implementation
**Уровень риска**: НИЗКИЙ 🟢

**Проблема**:
- Auth может быть tedious
- Security considerations

**Impact**:
- Может добавить 1-2 дня к Milestone 5

**Mitigation**:
- ✅ Use Firebase Auth или Supabase (fast setup)
- ✅ Minimal MVP auth (не overengineer)
- ✅ Defer advanced features (OAuth, SSO) to Phase 2

---

# УТОЧНЯЮЩИЕ ВОПРОСЫ ДЛ� КЛИЕНТА

## 🎯 КРИТИЧНЫЕ ВОПРОСЫ (Must Answer Before Starting)

### Q1: Static Template Graphics - Scope Definition
**Контекст**: Вы показали мне Ventusky Weather Graphics во время звонка и упомянули что хотите similar templates.

**Вопросы**:
1. Сколько различных template layouts нужно для **MVP**?
   - 3-5 basic templates?
   - 10-15 templates?
   - 20+ templates?

2. Какие конкретно types templates наиболее important?
   - [ ] 7-day forecast
   - [ ] Current conditions
   - [ ] Hourly forecast (24hr)
   - [ ] Radar overview
   - [ ] Temperature map
   - [ ] Severe weather alerts
   - [ ] Other: _________

3. Уровень customization для templates:
   - **Option A**: Pre-designed, только data auto-populates (faster)
   - **Option B**: Fully customizable (colors, fonts, layout positions) (slower)
   - **Option C**: Hybrid - некоторые elements editable

4. Вы хотите чтобы я design templates с нуля, или:
   - Вы предоставите design references/mockups?
   - Можно адаптировать existing styles (Ventusky-like)?
   - License Ventusky templates? (вы упоминали это)

**Почему критично**: Это может быть 20% проекта или 50% проекта. Нужна clarity для accurate timeline.

**Мое предложение**:
- MVP = 3-5 basic templates (pre-designed, auto-populated data)
- Phase 2 = Expanded template library + full customization

Вы согласны с этим approach?

---

### Q2: Xweather API Access & Capabilities
**Контекст**: Проект heavily зависит от Xweather API.

**Вопросы**:
1. Когда вы сможете предоставить Xweather API credentials?
   - Нужны immediately после hiring для exploration

2. Какой plan/tier у вас для Xweather?
   - Free tier?
   - Developer plan?
   - Professional/Enterprise?
   - (Некоторые advanced layers могут требовать higher tier)

3. У вас есть access к Xweather documentation?
   - Можете поделиться links?

4. Есть ли какие-то specific Xweather layers которые MUST work?
   - Future radar = highest priority?
   - Snow accumulation?
   - Другие?

5. Rate limits или usage restrictions?
   - Сколько API calls в день/час allowed?
   - Это повлияет на design decisions

**Почему критично**: Не могу начать Milestone 1 без API access. Timeline starts после получения credentials.

---

### Q3: AI-Generated Prototype Code
**Контекст**: Вы упомянули что ChatGPT создал prototype code (60% якобы).

**Вопросы**:
1. Вы загрузили этот код в job post? (Я пока не вижу)
2. На каком stack написан? (React? Vanilla JS? Other?)
3. Вы хотите чтобы я:
   - **Option A**: Build on top of AI code (integrate)
   - **Option B**: Review AI code, use useful parts, build mostly fresh
   - **Option C**: Ignore AI code, use my demo as base

**Мое мнение**:
У меня уже есть working demo с правильной architecture. Если AI код quality, я интегрирую useful parts. Если качество сомнительное, лучше build чисто.

Вы согласны?

---

## 💬 ВАЖНЫЕ ВОПРОСЫ (Should Answer Soon)

### Q4: OBS Integration Requirements
**Вопросы**:
1. Вы планируете использовать это в OBS только как:
   - **Browser Source** (read-only display)?
   - **Interactive Browser Source** (clicking controls во время broadcast)?

2. OBS version вы используете?
   - OBS Studio (latest)?
   - Streamlabs OBS?

3. Должно работать в green screen setup?
   - Transparent background option нужен?

**Мое предположение**: Browser Source с interact mode для controls. Подтверждаете?

---

### Q5: Export Format Priorities
**Вопросы**:
1. Какой export format MOST important для MVP?
   - [ ] PNG (single frame) - Easy
   - [ ] PNG sequence (multiple frames) - Medium
   - [ ] MP4 video - Hard (может быть Phase 2)

2. Для social media, вы чаще используете:
   - Static images (PNG)?
   - Short videos (MP4)?

3. Если MP4 export сложно implement в MVP timeline, ok отложить на Phase 2?

**Мое предложение**: MVP = PNG + PNG sequence. MP4 = Phase 2 или use external tool (OBS recording).

---

### Q6: User Authentication - MVP Scope
**Вопросы**:
1. Для MVP auth, нужно ли:
   - [ ] Email/password signup (simple)
   - [ ] Social login (Google, Facebook) - adds complexity
   - [ ] Email verification
   - [ ] Password reset

2. Payment integration для MVP?
   - **Option A**: Simple flag (isPaid: true/false) - вы manually activate
   - **Option B**: Full Stripe integration - adds significant complexity

**Мое предложение**: MVP = Email/password + simple flag. Full payment = Phase 2.

---

### Q7: Landing Page Content
**Вопросы**:
1. Вы предоставите:
   - Product description text?
   - Pricing information?
   - Logo/branding assets?

2. Или я должен draft это? (Can do, но ваш input лучше)

3. Domain уже есть?
   - Или нужна помощь с setup?

---

## 📋 NICE-TO-KNOW ВОПРОСЫ (Not Urgent)

### Q8: Target Audience Details
Это поможет мне design UX:
1. Типичный user - насколько tech-savvy?
   - Weather presenter (non-technical)?
   - Streamer (some tech experience)?
   - Educational outlet (varies)?

2. Age range?
   - Helps inform UI design choices

---

### Q9: Branding/Design Preferences
1. Есть ли specific color scheme?
2. Professional/corporate look vs fun/creative?
3. Reference apps вы любите (UI/UX wise)?

---

### Q10: Future Vision (Phase 2+)
Не для MVP, но полезно знать direction:
1. Планируете offering:
   - Free tier (limited features)?
   - Paid tier только?
   - Multiple pricing tiers?

2. Планируете team features? (Multiple users per account)

3. Planning mobile version в будущем?

---

# ПРЕДЛОЖЕННЫЙ APPROACH К ВОПРОСАМ

## Как отправить клиенту:

**Option A - В Upwork Message**:
Короткое сообщение:
> "Based on our call, I've prepared detailed proposal with milestones and timeline. Before finalizing, I have a few critical questions to ensure accurate scope (mainly around static templates and Xweather API access). Should I send questions here or would you prefer a quick call?"

**Option B - Google Doc**:
- Создать clean Google Doc с questions
- Отправить link клиенту
- Он может answer directly в doc (collaborative)

**Option C - В Final Proposal**:
- Include questions section в пропозале
- Client reviews all at once

---

# RISK MITIGATION SUMMARY

| Risk | Severity | Mitigation Strategy | Timeline Impact |
|------|----------|---------------------|-----------------|
| Static templates unclear | 🔴 High | Clarify scope, limit MVP to 3-5 templates | +0-7 days |
| Xweather API complexity | 🟡 Med-High | Early access, API exploration first | +0-5 days |
| Animation performance | 🟡 Med-High | Early testing, set limits, optimize | +0-4 days |
| AI code integration | 🟡 Medium | Review first, use selectively | +0-3 days |
| Curved fronts | 🟡 Medium | Use libraries, early prototype | +0-3 days |
| Export quality | 🟡 Medium | Test early, fallback options | +0-2 days |
| Client trust | 🟢 Low | Over-communicate, video demos | 0 days |
| Timezone diff | 🟢 Low | Async + scheduled calls | 0 days |

**Total Risk Buffer**: 5-10 days
**Base Timeline**: 28-35 days
**Safe Timeline**: 35-42 days (5-6 weeks)

---

# DECISION: FINAL TIMELINE COMMITMENT

На основе рисков, я предлагаю в пропозале:

**Conservative Estimate**: 5-6 weeks
- Учитывает все major risks
- Includes buffer для revisions
- Realistic для client expectations

**Best Case**: 4 weeks
- Если scope stays clear
- Если Xweather API straightforward
- Если minimal revisions

**Worst Case**: 7-8 weeks
- Если static templates scope explosion
- Если major technical blockers
- Not committing to this, but aware

**Рекомендация**: Commit to "5-6 weeks for MVP, potentially faster pending scope clarity."
