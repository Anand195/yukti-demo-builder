---
name: yukti-demo-builder
description: >
  Build a fully customized, interactive ScaleYukti WhatsApp engagement demo for any business — from just a URL.
  Pass a business website link (and optional context about their sales motive) and this skill will research the business,
  understand their lead flow and pain points, then generate a branded interactive HTML demo showing exactly how ScaleYukti
  boosts their sales via WhatsApp automation.
  ALWAYS trigger this skill when the user says things like: "build a demo for [URL]", "create a ScaleYukti demo",
  "generate demo for this business", "make a WhatsApp engagement demo", "show ScaleYukti value for [business]",
  "demo for my prospect", or passes any website URL in a ScaleYukti / WhatsApp sales context.
---

# ScaleYukti Demo Builder

Turns a business website URL into a fully customized, interactive HTML demo showing how ScaleYukti's WhatsApp engagement platform would increase that business's sales.

The output mirrors the style and depth of the Ahmedabad Estate reference demo: animated lead qualification chatbot, live CRM update panel, team WhatsApp alert, recovery scenarios, pipeline math, and database revival — all adapted to the specific business.

## Input

- **url** (required): Business website URL
- **context** (optional): Extra info — sales motive, pain points they mentioned, tools they use, industry nuances

## Output

One file saved to your working directory (or a user-specified output folder):
- `[BusinessName]_ScaleYukti_Demo.html` — 4-tab interactive demo (open in browser)

> **Note:** If the user has a preferred output directory configured, save the file there. Otherwise, save to the current working directory.

---

## Step 1 — Read Your References First

Before researching or writing any code, read these two files in full:

- `references/scaleyukti-product.md` — ScaleYukti's 5 services, value props, and how they map to business types
- `references/business-scenarios.md` — Business type definitions, scenario mappings, qualification questions, and CRM field sets

This matters: matching the right ScaleYukti services to the right business pain points is what makes the demo feel specific and credible — not generic.

---

## Step 2 — Research the Business

Goal: understand what they sell, how leads arrive, what the team does manually today, and where the biggest friction is.

### Tool priority (try in order, stop when you have enough):

1. **Tavily** — call `tavily_search` (or `tavily_extract`) with these simultaneously:
   - `tavily_extract` on the URL itself to read the website content directly
   - `tavily_search` for `"[business name] [city] services reviews"`
   - `tavily_search` for `"[business name] how to buy / book / enquire"`

2. **Chrome MCP** — use `mcp__Claude_in_Chrome__*` to navigate to the URL and read the homepage + Services/About pages. Look for: team size signals, product catalogue, pricing, WhatsApp button, booking flow.

3. **WebSearch fallback** — if neither tool above is available, use the `WebSearch` tool.

### Extract and document:

```
Business Name:
Industry / Category:
City / Region:
Core product or service (what they sell):
How customers find them (Meta Ads / Google / walk-in / referral / etc.):
Approximate team size:
Tools mentioned (CRM, booking system, ERP, etc.):
Current WhatsApp usage (visible on site? click-to-chat?):
Key pain points (from reviews, FAQs, or service descriptions):
Business motive (sell property / book appointment / close B2B deal / drive purchase / etc.):
```

If the user provided extra context, merge it — user-provided facts take priority over inferred ones.

---

## Step 3 — Build the Business Profile

Using your research + `references/business-scenarios.md`, decide:

| Field | What to decide |
|---|---|
| Business type | One of the types listed in business-scenarios.md |
| Primary pain | The #1 thing ScaleYukti fixes for this type |
| Lead persona | Realistic name + one-line description of a typical inbound lead |
| Team persona | Name + role of the person who handles leads (e.g., "Rahul, Sales Executive") |
| Qualification filters | 4–5 WhatsApp chatbot questions specific to this business |
| CRM fields | 10–12 fields their CRM captures per lead |
| Matched offerings | 2–3 specific products/services from the business matching a typical inquiry |
| Tech stack story | Which tools connect (WhatsApp API → their CRM/booking system → team alert) |
| Recovery scenario | Which Tab 2 scenario from business-scenarios.md fits best |

---

## Step 4 — Generate the HTML Demo

### Reference implementation

If the user has provided a reference HTML demo file, read it. Otherwise, skip this step — the patterns in `references/html-architecture.md` are sufficient.

Study its:
- Overall tab structure and CSS variable definitions
- Tech stack banner pattern (6-node chain at the top)
- Tab 1 four-column layout: journey steps panel / lead WhatsApp phone / CRM browser panel / team member phone
- Animation engine: `LEAD_MSGS` array, `CRM_UPDATES` array, `TEAM_ALERT` string, `t1Play()` function, `MSG_DELAYS` timing array
- WhatsApp phone UI: `.phone-frame`, message bubbles (in/out), typing indicator
- CRM panel: browser chrome bar, field rows with live-dot indicator, `crm-assign` div
- Tab 2 recovery pattern: WITH/WITHOUT toggle, slot state transitions or recovery chat flow
- Tab 3 pipeline math: tier system + funnel + goal working-backwards
- Tab 4 database revival: segment breakdown + broadcast funnel

Then read `references/html-architecture.md` for the color palette, key CSS classes, and JavaScript pattern summary.

### Build rules

- Keep the SAME visual structure, dark navy theme, and animation engine as v3
- Replace ALL content with the researched business's specifics:
  - Business name in the header and Tab 1 headline
  - Tech stack banner showing their actual tools (or generic equivalents)
  - Qualification chatbot messages in industry-appropriate language
  - CRM fields relevant to their business (no "BHK Type" for a salon)
  - Recovery scenario adapted from business-scenarios.md
  - Pipeline numbers realistic for their scale
  - Database revival estimate based on their likely contact base size
- The lead persona's WhatsApp conversation must feel authentic — use vocabulary a real customer in that industry would use

### Output file

Save to the current working directory (or user-specified output folder):
`./[BusinessName]_ScaleYukti_Demo.html`

---

## Step 5 — Present Result

Provide a file path to the HTML output:

```
[BusinessName]_ScaleYukti_Demo.html — saved to your working directory
```

Follow with a 3–4 sentence summary covering:
- What type of business this is and their primary pain point
- Which ScaleYukti services are most relevant for them (from references/scaleyukti-product.md)
- The #1 value headline for this prospect (e.g., "3.5 hrs/person/day saved on manual calling")

---

## Edge Cases

**Website returns nothing useful**: Fall back to web search for the business name + city + industry. Use any public source (Google Maps, Justdial, IndiaMart, social profiles).

**Business type doesn't match any in business-scenarios.md**: Pick the closest type and adapt. The general pattern (qualification → CRM update → team alert → recovery → pipeline → revival) works for any lead-driven business.

**Non-Indian business**: Adjust persona names, currency, and cultural references. ScaleYukti product logic stays the same.
