# HTML Demo Architecture Reference

This file describes the exact visual structure, color system, and JavaScript patterns used in the v3 reference demo (`AhmedabadEstate_ScaleYukti_Demo_v3.html`). Read this alongside the reference file itself.

---

## Color Palette (CSS Variables)

Defined as `:root` CSS variables at the top of the HTML:

```css
--navy:   #0D1B2A   /* primary background, darkest */
--navym:  #1A2E45   /* secondary background, panels */
--navy3:  #243B55   /* card backgrounds, slightly lighter */
--orange: #FF6B35   /* primary accent, CTAs, highlights */
--cyan:   #00B4D8   /* data/metric accent */
--green:  #06D6A0   /* success, confirmed states */
--red:    #E63946   /* warning, no-show, without-SY states */
--yellow: #FFD166   /* warm/standby states */
--purple: #9B5DE5   /* integration/automation accent */
--muted:  #8FA3B1   /* secondary text */
--white:  #FFFFFF
```

**Usage rules:**
- Backgrounds: navy → navym → navy3 (darkest to lightest)
- Primary actions / active states: orange
- System messages / automation: purple
- Good outcomes / confirmed: green
- Problems / current-state without SY: red
- Data callouts / metrics: cyan
- Never use white backgrounds — maintain the dark theme throughout

---

## Page Structure

```
<div class="demo-container">
  <!-- 1. Header bar: ScaleYukti logo + business name -->
  <div class="demo-header">...</div>

  <!-- 2. Tech stack banner: 6-node chain -->
  <div class="tech-stack-banner">
    <div class="stack-node">Meta Ads</div>
    <div class="stack-arrow">→</div>
    <div class="stack-node active">EasySocial WA API</div>
    ...
  </div>

  <!-- 3. Tab navigation -->
  <div class="tab-nav">
    <button class="tab-btn active" onclick="showTab('t1')">Full Integration</button>
    <button class="tab-btn" onclick="showTab('t2')">No-Show Recovery</button>
    <button class="tab-btn" onclick="showTab('t3')">Weekend Pipeline</button>
    <button class="tab-btn" onclick="showTab('t4')">Database Revival</button>
  </div>

  <!-- 4. Tab panels -->
  <div id="tab-t1" class="tab-panel active">...</div>
  <div id="tab-t2" class="tab-panel">...</div>
  <div id="tab-t3" class="tab-panel">...</div>
  <div id="tab-t4" class="tab-panel">...</div>
</div>
```

---

## Tab 1 — Full Integration (Hero Tab)

The most important tab. Shows the complete automated flow in real time.

### 4-column layout:

```
[ Journey Steps ] [ Lead's WhatsApp ] [ CRM Dashboard ] [ Team Member's WhatsApp ]
     (panel)          (phone UI)          (browser UI)         (phone UI)
```

**Journey Steps panel** (`#t1-journey`): Numbered list of 6–7 steps, each with an icon + title + subtitle. Steps activate sequentially during animation (class `active` applied with `step-dot` turning orange).

**Lead WhatsApp phone** (`#t1-lead-phone`): iPhone-style frame showing the WhatsApp conversation. Shows the chatbot qualification conversation — messages appear one by one.

**CRM panel** (`#t1-crm`): Browser-style frame (dots + URL bar) showing a CRM field list. Fields animate in one by one as the chatbot captures data.

**Team WhatsApp** (`#t1-team-phone`): Second phone showing the team member's personal WhatsApp receiving the ScaleYukti alert.

### Key data arrays (customize ALL of these for each business):

```javascript
// Lead's WhatsApp chatbot conversation
// direction: 'in' = lead message (right side), 'out' = bot message (left side)
const LEAD_MSGS = [
  { text: "Hi, I'm interested in...", dir: 'in' },
  { text: "Welcome! I'm the ScaleYukti assistant for [Business]. ...", dir: 'out' },
  // ... 10-14 messages total covering all qualification questions + project match + booking
];

// Timing delays in ms for each message
const MSG_DELAYS = [800, 2200, 2800, 4200, 5000, 6200, 6800, 8000, 8600, 9400, 10000, 12000, 12200, 13000];

// CRM field updates: which field to update, with what value, at what delay
const CRM_UPDATES = [
  { id: 'crm-name', val: 'Priya Patel', delay: 1200 },
  { id: 'crm-phone', val: '+91 98XXX XXXXX', delay: 1800 },
  { id: 'crm-budget', val: '60L–80L', delay: 4800 },
  // ... one entry per qualification answer captured
];

// Team alert message (full formatted WhatsApp message the team member receives)
const TEAM_ALERT = `🔔 *HOT LEAD ALERT — ScaleYukti*
━━━━━━━━━━━━━━━━
👤 *Name:* Priya Patel
📞 *Phone:* +91 98XXX XXXXX
💰 *Budget:* 60L–80L
📍 *Location:* Bopal
🏠 *BHK:* 3BHK
✅ *Site Visit:* Saturday 11 AM
━━━━━━━━━━━━━━━━
*Matched Projects:*
• Shivalik Greens
• Royal Orchid

*Score: 🔥 HOT (87/100)*
*Action: Call before Friday 6 PM*`;
```

### Animation engine (`t1Play()` function):

```javascript
function t1Play() {
  // Reset all panels to initial state
  // Then fire a cascade of setTimeout calls:

  // Journey steps activate sequentially
  setTimeout(() => activateStep(1), 500);
  setTimeout(() => activateStep(2), 1500);
  // ...

  // Lead messages appear one by one
  LEAD_MSGS.forEach((msg, i) => {
    setTimeout(() => appendMessage(msg), MSG_DELAYS[i]);
  });

  // CRM fields update as chatbot captures data
  CRM_UPDATES.forEach(u => {
    setTimeout(() => updateCRMField(u.id, u.val), u.delay);
  });

  // Team alert arrives after CRM is populated
  setTimeout(() => showTeamAlert(), 12500);
  setTimeout(() => showTeamReply(), 14000);
}
```

---

## WhatsApp Phone UI

```html
<div class="phone-frame" id="t1-lead-phone">
  <div class="phone-status-bar">9:41 AM · ●●●●●</div>
  <div class="wa-header">
    <div class="wa-avatar">SY</div>
    <div class="wa-info">
      <div class="wa-name">ScaleYukti Alerts</div>
      <div class="wa-status">Online</div>
    </div>
  </div>
  <div class="chat-messages" id="lead-messages">
    <!-- Messages injected by JS -->
  </div>
  <div class="typing-indicator" id="typing-ind" style="display:none">
    <span></span><span></span><span></span>
  </div>
  <div class="chat-input-bar">Type a message</div>
</div>
```

Message bubble classes:
- `.msg-out` — bot/business message (left-aligned, navym background)
- `.msg-in` — lead's message (right-aligned, orange/dark background)

---

## CRM Panel UI

```html
<div class="crm-panel" id="t1-crm">
  <div class="browser-chrome">
    <div class="browser-dots">
      <span></span><span></span><span></span>
    </div>
    <div class="browser-url">telecrm.app/leads/live</div>
    <div class="live-dot">● LIVE</div>
  </div>
  <div class="crm-fields">
    <div class="crm-row">
      <span class="crm-label">Lead Name</span>
      <span class="crm-value" id="crm-name">—</span>
    </div>
    <!-- repeat for each field -->
  </div>
  <div class="crm-assign" id="crm-assign">
    <!-- Assigned team member shown after qualification -->
  </div>
</div>
```

---

## Tab 2 — Recovery Scenario

### WITH/WITHOUT toggle pattern:

```html
<div class="toggle-bar">
  <button class="toggle-btn active" id="btn-without" onclick="showWithout()">
    ❌ Without ScaleYukti
  </button>
  <button class="toggle-btn" id="btn-with" onclick="showWith()">
    ✅ With ScaleYukti
  </button>
</div>

<div id="view-without">
  <!-- Shows: no-show happens, team day plan collapses, manual scramble -->
</div>
<div id="view-with" style="display:none">
  <!-- Shows: automated recovery, slot filled, revenue saved -->
</div>
```

### Slot system (for appointment/visit businesses):

```javascript
const BASE_SLOTS = [
  { id: 1, time: '10:00 AM', name: 'Rahul S.', type: 'Type A', tier: 1, status: 'confirmed' },
  { id: 2, time: '11:30 AM', name: 'Priya M.', type: 'Type B', tier: 1, status: 'confirmed' },
  { id: 3, time: '2:00 PM',  name: 'Amit K.', tier: 2, status: 'standby' },
  { id: 4, time: '4:00 PM',  name: 'Sneha R.', tier: 3, status: 'reserve' },
];

function renderSlots(overrides = {}) {
  // Renders slot cards with color-coded status (green=confirmed, yellow=standby, muted=reserve)
  // overrides allows showing mid-scenario state (e.g., slot 1 becomes no-show, slot 3 gets promoted)
}
```

---

## Tab 3 — Pipeline Math

For visit/appointment businesses:
- Sliders or static display: target visits per period, no-show rate before/after SY
- Working backwards from revenue goal to pipeline size needed
- 3-tier slot system visualization
- Day-by-day timeline (Mon–Sun) with task types

For e-commerce:
- Funnel visualization: visitors → add to cart → checkout → recovery → purchased
- Revenue recovered per week from cart abandonment sequences

Keep numbers realistic for the business scale. For a 4-person real estate team, 8–10 site visits/weekend is realistic. For a single-doctor clinic, 15–20 appointments/day is realistic.

---

## Tab 4 — Database Revival

Standard structure across all business types:

```
[Segment breakdown]           [Broadcast funnel]
  HOT (bought within 6 mo)     Send: X contacts
  WARM (7–18 months)           Opens: X (45%)
  COOL (18 months+)            Replies: X (12%)
  DORMANT (2+ years)           Appointments/Visits: X (4–6%)
  ─────────────────            Revenue potential: ₹X
  Total: [database size]
```

**Database size estimates by business type:**
- Real estate: 1,000–5,000 past leads
- Clinic: 2,000–8,000 past patients
- Salon: 500–2,000 past clients
- Restaurant: 1,000–10,000 past customers
- E-commerce: 5,000–50,000 past customers
- Education: 500–2,000 past inquiries
- B2B: 200–1,000 past prospects

**ROI calculation block** (at bottom of Tab 4):

```
If 5% respond → [X] appointments/visits/orders
Average order/deal value: ₹[Y]
Potential revenue from one broadcast: ₹[X × Y]
Cost of broadcast (₹2–3/message): ₹[X × 2.5]
ROI: [((X×Y) / (X×2.5)) × 100]% return
```

---

## JavaScript Utilities (include in every demo)

```javascript
// Tab switching
function showTab(id) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + id).classList.add('active');
  document.querySelector(`[onclick="showTab('${id}')"]`).classList.add('active');
}

// Message append with typing indicator
function appendMsg(containerId, text, dir, callback) {
  const c = document.getElementById(containerId);
  const typing = document.getElementById('typing-ind');
  if (typing) { typing.style.display = 'flex'; c.scrollTop = c.scrollHeight; }
  setTimeout(() => {
    if (typing) typing.style.display = 'none';
    const div = document.createElement('div');
    div.className = `msg-bubble msg-${dir}`;
    div.textContent = text;
    c.appendChild(div);
    c.scrollTop = c.scrollHeight;
    if (callback) callback();
  }, 600);
}

// CRM field update
function updateField(id, val) {
  const el = document.getElementById(id);
  if (!el) return;
  el.textContent = val;
  el.classList.add('updated');
  setTimeout(() => el.classList.remove('updated'), 1500);
}
```

---

## Responsive / Final Polish

- Set `max-width: 1400px; margin: 0 auto` on `.demo-container`
- Font: `'Inter', sans-serif` loaded from Google Fonts
- Mobile: stack the 4-column Tab 1 layout to 2 columns on screens < 768px
- Play button: large orange button `▶ Play Full Integration` centered below Tab 1 panels, calls `t1Play()`
- Add a reset button that clears all panels back to initial state for re-demo
