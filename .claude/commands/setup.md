# Setup: Configure Browser Access Method

Configure how the agent will access and evaluate the target website.

## Options

Present the user with three browsing method options:

### 1. WebFetch (Default — No Setup Required)
- Uses the built-in `WebFetch` tool to retrieve page content
- Works immediately, no installation needed
- Limitation: Cannot execute JavaScript, no screenshots, may miss dynamically rendered content

### 2. Playwright with Local Browser (Recommended)
- Uses Playwright to launch a real browser for full page rendering
- Captures screenshots, evaluates JS-rendered content, tests interactive elements
- **Setup steps**:
  1. Check if Playwright is installed: `which playwright`
  2. If not installed: `npm install -g playwright` or `npx playwright install`
  3. Install browser binaries: `npx playwright install chromium`
  4. Verify with: `npx playwright screenshot --browser chromium https://example.com /tmp/test-screenshot.png`

### 3. Playwright with Remote Browser
- Connects to a remote browser instance via CDP (Chrome DevTools Protocol)
- Useful for headless servers or when local browser install isn't possible
- **Setup steps**:
  1. Ask user for the remote browser CDP endpoint URL (e.g., `ws://localhost:9222`)
  2. Store the endpoint in `config.json` as `remote_browser_endpoint`

## After Setup

Update `config.json` with the chosen `browsing_method` value: `"webfetch"`, `"playwright-local"`, or `"playwright-remote"`.

If `config.json` doesn't exist yet, tell the user to run `/onboard` first.

Confirm the setup is complete and suggest running `/run-evaluation`.
