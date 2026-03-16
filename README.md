[![Part of the Claude Agent Blueprints Index](https://img.shields.io/badge/Claude%20Agent%20Blueprints-Index-blue?style=flat-square&logo=github)](https://github.com/danielrosehill/Claude-Code-Repos-Index)

# Claude Red Team Buyer

A Claude Code agent template that evaluates websites from the perspective of a potential buyer/customer. It performs "red team" analysis — identifying friction points, trust issues, UX problems, and conversion blockers that might cause a real buyer to leave.

## What It Does

1. You provide your website URL and describe your business/target buyer
2. A subagent visits your site as a skeptical potential buyer
3. It evaluates 10 dimensions: first impressions, value proposition, trust, UI/UX, CTAs, objections, content quality, positioning, conversion flow, and friction points
4. Generates a detailed PDF report with scores, findings, and prioritized improvements

## Quick Start

```bash
# 1. Set up your target website and evaluation context
/onboard

# 2. (Optional) Configure browser access for richer evaluation
/setup

# 3. Run the evaluation
/run-evaluation
```

## Browsing Methods

| Method | Setup | Capabilities |
|--------|-------|-------------|
| **WebFetch** (default) | None | HTML content analysis, link structure, meta tags |
| **Playwright Local** | `npx playwright install chromium` | Screenshots, JS rendering, interactive elements |
| **Playwright Remote** | Remote CDP endpoint | Same as local, runs on remote browser |

## Output

Reports are saved to `outputs/` as timestamped PDFs:

```
outputs/evaluation-2026-03-16T14-30-00.pdf
```

Each report includes:
- Overall score (1-10) across 10 evaluation dimensions
- Detailed findings with positives and improvements per dimension
- Prioritized list of recommended changes
- Buyer verdict — would this buyer convert?

## Evaluation Dimensions

1. **First Impressions** — Visual impact in the first 5 seconds
2. **Value Proposition Clarity** — Is the offering immediately clear?
3. **Trust & Credibility** — Social proof, team info, security signals
4. **UI/UX Quality** — Design, navigation, layout, responsiveness
5. **Call-to-Action Effectiveness** — CTA clarity and placement
6. **Objections & Doubts** — What would make a buyer hesitate?
7. **Content Quality** — Writing, tone, consistency
8. **Competitive Positioning** — Differentiation and market fit
9. **Conversion Flow** — Path from landing to signup/purchase
10. **Friction Points** — Specific moments where buyers might abandon

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- [Typst](https://typst.app/) for PDF generation
- (Optional) [Playwright](https://playwright.dev/) for browser-based evaluation

---

For more Claude Code projects, visit [my index](https://github.com/danielrosehill/Claude-Code-Repos-Index).
