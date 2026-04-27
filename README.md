# TWC AI Planning Agent · Prototype

A working multi-agent AI workflow built specifically for **The Wedding Company (TWC)** — automating the three most manual ops steps in early-stage wedding planning: intake structuring, vendor matching, and follow-up generation.

> Built as a proof-of-concept by **Hitaeshi Sehgal** (CS, BITS Pilani) in response to TWC's AI Engineering Wizard internship post.

---

## What It Does

Most wedding planning companies handle new couples like this:

1. Onboarding call → someone takes notes
2. Planner manually figures out which vendors fit
3. Planner writes 4–5 individual outreach emails
4. Repeat for every new couple

**That's 3–4 hours of ops work per couple. This pipeline does it in ~20 seconds.**

---

## The Agent Pipeline

```
Intake Form → Agent 1 → Agent 2 → Agent 3
              Brief     Vendor    Follow-Up
              Generator Matching  Generator
```

### Agent 1 — Planning Brief Generator
Takes raw intake form data (couple name, date, city, budget, guest count, style, notes) and outputs a structured planning brief with:
- Auto-assigned Couple ID
- Complexity scoring
- Planning timeline estimate
- Budget allocation breakdown
- Extracted special requirements

### Agent 2 — Vendor Matching Engine
Cross-references the couple's brief against the vendor database and returns ranked matches with:
- Match score per vendor
- Priority label (Must Have / Recommended / Optional)
- Reason for match referencing specific couple requirements

### Agent 3 — Follow-Up Generator
Writes personalised vendor outreach messages for the top matches — referencing the couple's specific style, date, and requirements. One-click copy to clipboard.

---

## Tech Stack

| Layer | Choice |
|---|---|
| Frontend | Vanilla HTML/CSS/JS — no framework, no build step |
| AI | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Agent pattern | Sequential chaining with structured JSON outputs |
| Vendor data | Hardcoded mock CRM (8 Mumbai vendors) |

**No backend. No server. Single file. Open and run.**

---

## Running It Locally

```bash
# 1. Clone
git clone https://github.com/yourusername/twc-ai-agent
cd twc-ai-agent

# 2. Open in Chrome
open twc-agent-demo.html
```

The app calls the Anthropic API directly from the browser. The API key is handled via Anthropic's Claude.ai artifact environment — if running outside that environment, add your key to the fetch headers in the script section.

---

## Architecture Notes

**Why sequential agents instead of one big prompt?**

Each agent has a single, well-defined job and returns structured JSON. This makes the system:
- Debuggable — you can see exactly where something went wrong
- Modular — swap out any agent independently
- Observable — the activity log shows per-step timing

**Why structured JSON outputs?**

Forcing the model to return JSON (with schema enforcement in the system prompt) makes downstream agent inputs reliable and parseable — critical for production systems where one agent feeds the next.

**What a production version would add:**
- Real CRM integration (vendor DB pulled via API)
- Persistent couple profiles and planning timelines
- Calendar availability checking for vendors
- WhatsApp/email send integration
- Multi-turn conversation for couple intake (instead of a form)

---

## About

Built by **Hitaeshi Sehgal** — CS student at BITS Pilani, currently building AI automation systems and LLM workflows at [Ideanix](https://ideanix.in).

This prototype was built to demonstrate applied AI agent architecture on a real, high-friction domain — not as a research exercise, but as something that could go into production.

→ [LinkedIn](www.linkedin.com/in/hitaeshi-sehgal-1b5aa32a8) · [Email](hitaeshi25sehgal@gmail.com)
