# ScaleYukti Demo Builder — Claude Code Plugin

> Turn any business website URL into a fully customized, interactive HTML demo showing how **ScaleYukti's WhatsApp engagement platform** drives sales.

[![Claude Plugin](https://img.shields.io/badge/Claude-Plugin-FF6B35?style=flat-square)](https://code.claude.com/docs/en/plugins)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](./LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-Repo-181717?style=flat-square&logo=github)](https://github.com/Anand195/yukti-demo-builder)

---

## Table of Contents

- [What It Does](#what-it-does)
- [Installation (Marketplace)](#installation-marketplace)
- [Installation (Manual)](#installation-manual)
- [Usage](#usage)
- [Demo Structure](#demo-structure)
- [Supported Business Types](#supported-business-types)
- [About ScaleYukti](#about-scaleyukti)
- [License](#license)

---

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

---

## Installation (Marketplace)

This repository is a **Claude Code plugin marketplace**. Installing via the marketplace is the recommended approach.

### Prerequisites

- [Claude Code](https://code.claude.com/docs/en/quickstart) installed and authenticated
- Claude Code v2.1.x or later

### Step 1: Add the marketplace

Open Claude Code and run:

```
/plugin marketplace add Anand195/yukti-demo-builder
```

This registers the marketplace catalog with Claude Code. You only need to do this once.

### Step 2: Install the plugin

```
/plugin install yukti-demo-builder@yukti-marketplace
```

### Step 3: Activate the plugin

```
/reload-plugins
```

### Step 4: Verify it's installed

Run `/plugin list` — you should see `yukti-demo-builder` listed.

Or run `/help` and look for the skill `yukti-demo-builder:yukti-demo-builder` under installed plugins.

### Updating

When a new version is released, update with:

```
/plugin marketplace update yukti-marketplace
/plugin update yukti-demo-builder@yukti-marketplace
/reload-plugins
```

### Uninstalling

```
/plugin uninstall yukti-demo-builder@yukti-marketplace
/plugin marketplace remove yukti-marketplace
```

---

## Installation (Manual)

If you prefer not to use the marketplace, you can load the plugin directly:

### Option A: Load with --plugin-dir

Clone the repo and load it when starting Claude Code:

```bash
git clone https://github.com/Anand195/yukti-demo-builder.git
claude --plugin-dir ./yukti-demo-builder
```

Then use the skill as `/yukti-demo-builder:yukti-demo-builder`.

### Option B: Skills-directory plugin

Clone into your personal skills folder:

```bash
git clone https://github.com/Anand195/yukti-demo-builder.git ~/.claude/skills/yukti-demo-builder
```

On your next Claude Code session, it loads automatically as `yukti-demo-builder@skills-dir`.

### Option C: Copy skills manually

Copy the `skills/` directory into your project:

```
your-project/
└── .claude/
    └── skills/
        └── yukti-demo-builder/
            ├── SKILL.md
            └── references/
                ├── business-scenarios.md
                ├── html-architecture.md
                └── scaleyukti-product.md
```

---

## Usage

Once installed, trigger the skill by saying something like:

- _"Build a demo for `https://example-business.com`"_
- _"Create a ScaleYukti demo for this salon website"_
- _"Show ScaleYukti value for this real estate company"_
- _"Make a WhatsApp engagement demo for my prospect"_

Or invoke it directly:

```
/yukti-demo-builder:yukti-demo-builder https://example-business.com
```

### Input Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | Business website URL to research |
| `context` | No | Extra info — sales motive, pain points, tools they use |

### Output

An interactive HTML file: `[BusinessName]_ScaleYukti_Demo.html`

Open it in any browser — no server required. The demo auto-animates a complete lead journey.

---

## Demo Structure

Each generated HTML demo contains:

- **Dark navy theme** with orange/cyan accent colors (`#0D1B2A` / `#FF6B35` / `#00B4D8`)
- **Tech stack banner**: Shows the 6-node integration chain (Meta Ads → WhatsApp API → ScaleYukti → Chatbot → CRM → Team)
- **Tab 1 — Full Integration**: 4-column layout with journey steps, lead WhatsApp phone, CRM dashboard, team member WhatsApp
- **Tab 2 — Recovery**: WITH/WITHOUT ScaleYukti toggle for no-show/cancellation recovery
- **Tab 3 — Pipeline**: Revenue pipeline math with realistic numbers
- **Tab 4 — Database Revival**: Segment breakdown + broadcast ROI

---

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

---

## About ScaleYukti

[ScaleYukti](https://scaleyukti.com) is a WhatsApp Customer Engagement Platform that connects to any WhatsApp Business API provider (EasySocial, Wati, AiSensy, Interakt, etc.) and adds five service layers:

- **Automation** — Instant WhatsApp responses to every lead
- **Chatbot** — AI-powered lead qualification on WhatsApp
- **Drip Campaigns** — Scheduled nurture sequences
- **Broadcasting** — Segmented bulk messaging
- **Voice Calling Agent** — AI voice call follow-ups

---

## Repository Structure

```
yukti-demo-builder/
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest (required)
│   └── marketplace.json      # Marketplace catalog (for /plugin marketplace add)
├── skills/
│   └── yukti-demo-builder/
│       ├── SKILL.md          # Core skill instructions
│       └── references/
│           ├── business-scenarios.md
│           ├── html-architecture.md
│           └── scaleyukti-product.md
├── package.json
├── README.md
├── LICENSE
└── .gitignore
```

---

## License

MIT — see [LICENSE](./LICENSE)

---

*Built with the [Claude Code plugin system](https://code.claude.com/docs/en/plugins). Inspired by the [superpowers](https://github.com/obra/superpowers) plugin architecture.*
