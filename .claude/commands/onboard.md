# Onboard: Configure Red Team Buyer Evaluation

Collect the target website and evaluation objective from the user, then save the configuration.

## Steps

1. Ask the user for:
   - **Website URL**: The full URL of the website to evaluate (e.g., `https://example.com`)
   - **Objective/Context**: What does the user's business do? What kind of buyer would be visiting this site? What should the evaluation focus on? (e.g., "We sell B2B SaaS for project management. Evaluate as a mid-market engineering manager looking for a tool.")

2. Once both are provided, write a `config.json` file in the project root with this structure:
   ```json
   {
     "target_url": "<the URL>",
     "objective": "<the objective text>",
     "browsing_method": "webfetch",
     "onboarded_at": "<ISO 8601 timestamp>"
   }
   ```

   - Default `browsing_method` to `"webfetch"`. The user can change this later with `/setup`.

3. Confirm to the user that onboarding is complete and suggest they run `/setup` if they want to use Playwright for richer evaluation (screenshots, JS-rendered content), or `/run-evaluation` to proceed directly with WebFetch.
