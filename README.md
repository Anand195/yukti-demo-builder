# ScaleYukti Demo Builder — Claude Plugin

> Turn any business website URL into a fully customized, interactive HTML demo showing how **ScaleYukti's WhatsApp engagement platform** drives sales.

This is a [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) skill that researches any business from its website, understands its lead flow and pain points, then generates a branded 4-tab interactive HTML demo.

![ScaleYukti Demo](https://img.shields.io/badge/ScaleYukti-WhatsApp%20Engagement-FF6B35?style=flat-square)

## What It Does

Give it a business URL, and it will:

1. **Research** the business using web search + website scraping
2. **Map** their lead flow to the right ScaleYukti services
3. **Generate** a fully interactive HTML demo with 4 tabs:

| Tab | Content |
|-----|---------|
| **Full Integration** | Animated lead qualification chatbot → CRM auto-fill → team WhatsApp alert |
| **Recovery Scenario** | WITH/WITHOUT ScaleYukti toggle showing no-show/cancellation recovery |
| **Pipeline Math** | Realistic pipeline numbers, tier system, working-backwards from revenue goal |
| **Database Revival** | Segment breakdown + broadcast funnel + ROI calculation |

## Installation

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) installed
- Your Claude Code agent has web search / browsing capability

### Quick Install

```bash
# Clone this repository into your Claude Code skills directory
git clone https://github.com/Anand195/yukti-demo-builder.git
```

Then in your Claude Code `CLAUDE.md` or project settings, reference the skills directory.

### Manual Setup

Copy the `skills/` folder into your Claude Code project:

```
your-project/
├── CLAUDE.md
├── skills/
│   └── yukti-demo-builder/
│       ├── SKILL.md
│       └── references/
│           ├── business-scenarios.md
│           ├── html-architecture.md
│           └── scaleyukti-product.md
```

## Usage

Trigger the skill by saying something like:

- _"Build a demo for `https://example-business.com`"_
- _"Create a ScaleYukti demo for this salon website"_
- _"Show ScaleYukti value for this real estate company"_
- _"Make a WhatsApp engagement demo for my prospect"_

### Input Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | Business website URL to research |
| `context` | No | Extra info — sales motive, pain points, tools they use |

### Output

An interactive HTML file: `[BusinessName]_ScaleYukti_Demo.html`

Open it in any browser — no server required. The demo auto-animates a complete lead journey.

## Demo Structure

Each generated HTML demo contains:

- **Dark navy theme** with orange/cyan accent colors
- **Tech stack banner**: Shows the 6-node integration chain
- **Tab 1 — Full Integration**: 4-column layout with journey steps, lead WhatsApp phone, CRM dashboard, team member WhatsApp
- **Tab 2 — Recovery**: WITH/WITHOUT ScaleYukti toggle for no-show/cancellation recovery
- **Tab 3 — Pipeline**: Revenue pipeline math with realistic numbers
- **Tab 4 — Database Revival**: Segment breakdown + broadcast ROI

## Supported Business Types

The demo adapts to 10 business types:

| Type | Primary Pain | Key ScaleYukti Service |
|------|-------------|----------------------|
| Real Estate | No-shows, manual calling | Chatbot + Broadcasting |
| Clinic / Healthcare | Appointment no-shows | Automation + Voice Calling |
| Salon / Spa | Cancellations, tracking | Automation + Drip Campaigns |
| Restaurant | Peak-hour calls, cart abandonment | Broadcasting + Chatbot |
| E-commerce / D2C | Cart abandonment, retention | Broadcasting + Automation |
| Education / Coaching | Demo no-shows, cold leads | Chatbot + Drip Campaigns |
| B2B / SaaS | Slow follow-up, long cycles | Chatbot + Drip Campaigns |
| Auto Dealership | Manual test drive booking | Chatbot + Voice Calling |
| Wedding / Events | Multi-channel tracking | Chatbot + Drip Campaigns |
| Travel / Hospitality | Slow inquiry response | Chatbot + Broadcasting |

## About ScaleYukti

[ScaleYukti](https://scaleyukti.com) is a WhatsApp Customer Engagement Platform that connects to any WhatsApp Business API provider (EasySocial, Wati, AiSensy, Interakt, etc.) and adds five service layers:

- **Automation** — Instant WhatsApp responses to every lead
- **Chatbot** — AI-powered lead qualification on WhatsApp
- **Drip Campaigns** — Scheduled nurture sequences
- **Broadcasting** — Segmented bulk messaging
- **Voice Calling Agent** — AI voice call follow-ups

## License

MIT — see [LICENSE](./LICENSE)

---

*Built with Claude Code skills system. Inspired by the [superpowers](https://github.com/obra/superpowers) plugin architecture.*
