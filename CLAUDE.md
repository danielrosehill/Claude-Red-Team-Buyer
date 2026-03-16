# Claude Red Team Buyer

## Purpose

This is a Claude Code agent template that evaluates websites from the perspective of a potential buyer/customer. It performs "red team" analysis of a website's UI/UX, branding, positioning, professionalism, and overall buyer experience, then generates a detailed PDF report.

## Workflow

1. **Onboard** (`/onboard`): User provides website URL and the objective/context of the evaluation
2. **Setup** (`/setup`): Configure browser access (Playwright local browser, or WebFetch fallback)
3. The agent dispatches a subagent (`buyer-evaluator`) to crawl and evaluate the website
4. The subagent returns structured findings
5. The main agent compiles findings into a Typst-formatted PDF report
6. Report is saved to `outputs/` with a timestamp

## Key Directories

- `.claude/agents/` — Subagent definitions (buyer-evaluator)
- `.claude/commands/` — Slash commands (onboard, setup, run-evaluation)
- `outputs/` — Generated PDF reports (timestamped)
- `templates/` — Typst report template

## Tools

- **Typst**: Used for PDF generation (`typst compile`)
- **Playwright**: Preferred method for visiting websites (screenshots, DOM inspection)
- **WebFetch**: Fallback method when Playwright is unavailable

## Configuration

The file `config.json` in the project root stores the onboarding state (target URL, objective, browsing method). It is created/updated by the `/onboard` command.

## Running an Evaluation

```
/onboard          # Set target URL and objective
/setup            # Configure browser method (optional, defaults to WebFetch)
/run-evaluation   # Execute the full evaluation and generate report
```
