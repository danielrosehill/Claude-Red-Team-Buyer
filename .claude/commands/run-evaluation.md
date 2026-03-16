# Run Evaluation: Execute Red Team Buyer Analysis

This command runs the full red team buyer evaluation and generates a PDF report.

## Prerequisites

- `config.json` must exist in the project root (created by `/onboard`)
- If it doesn't exist, tell the user to run `/onboard` first and stop

## Steps

### 1. Load Configuration

Read `config.json` from the project root. Extract `target_url`, `objective`, and `browsing_method`.

### 2. Dispatch Buyer Evaluator Subagent

Launch the `buyer-evaluator` agent (from `.claude/agents/buyer-evaluator.md`) using the Agent tool with `subagent_type: "general-purpose"`.

Pass a detailed prompt to the subagent that includes:
- The target URL
- The objective/buyer persona context
- The browsing method to use
- Instructions to evaluate the following dimensions and return structured findings as a JSON block:

**Evaluation Dimensions:**
1. **First Impressions** — What does a buyer see/feel in the first 5 seconds?
2. **Value Proposition Clarity** — Is it immediately clear what the product/service does and who it's for?
3. **Trust & Credibility** — Social proof, testimonials, case studies, security badges, team info
4. **UI/UX Quality** — Visual design, layout, navigation, mobile responsiveness, loading speed
5. **Call-to-Action Effectiveness** — Are CTAs clear, compelling, and well-placed?
6. **Objections & Doubts** — What concerns would a skeptical buyer have? Pricing transparency, missing info
7. **Content Quality** — Writing quality, typos, tone consistency, jargon level
8. **Competitive Positioning** — How does this compare to what a buyer expects from competitors?
9. **Conversion Flow** — Is the path from landing to signup/purchase smooth?
10. **Friction Points** — Specific moments where a buyer might abandon

The subagent should return its findings as a structured JSON object with each dimension containing:
- `score` (1-10)
- `summary` (2-3 sentences)
- `positives` (list of strings)
- `improvements` (list of strings)
- `details` (longer analysis text)

**Browsing instructions for the subagent:**
- If `browsing_method` is `"webfetch"`: Use the WebFetch tool to retrieve the page HTML and analyze it
- If `browsing_method` is `"playwright-local"`: Use Bash to run Playwright commands for screenshots and page content
- If `browsing_method` is `"playwright-remote"`: Use Bash to run Playwright with the `--browser-endpoint` flag

The subagent should visit:
- The main/home page
- Any pricing page (if findable)
- Any about/team page (if findable)
- The signup/contact flow (if findable)

### 3. Process Subagent Results

Parse the structured findings returned by the subagent.

### 4. Generate Typst Report

Read the Typst template from `templates/report.typ`.

Create a timestamped `.typ` file in the `outputs/` directory (e.g., `outputs/evaluation-2026-03-16T14-30-00.typ`) by filling in the template with:
- The target URL
- The evaluation date
- The objective/persona context
- All dimension scores, summaries, positives, improvements, and details
- An overall score (average of dimension scores)
- An executive summary synthesizing the key findings
- A prioritized list of recommended improvements

### 5. Compile to PDF

Run: `typst compile outputs/evaluation-<timestamp>.typ outputs/evaluation-<timestamp>.pdf`

### 6. Report to User

Tell the user:
- The PDF has been generated at `outputs/evaluation-<timestamp>.pdf`
- Show the overall score and a brief executive summary
- List the top 3-5 most impactful improvements recommended
