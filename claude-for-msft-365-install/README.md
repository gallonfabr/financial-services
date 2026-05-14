# Claude for Office — Direct Cloud Setup

Admin tooling for configuring the Claude Office add-in to call your own cloud
(Vertex AI, Bedrock, or an LLM gateway) instead of Anthropic's API.

## Install

```bash
claude plugin marketplace add anthropics/financial-services-plugins
claude plugin install claude-for-msft-365-install@financial-services-plugins
```

Then inside the session: `/claude-for-msft-365-install:setup`

## Commands

| Command | What it does |
|---|---|
| `/claude-for-msft-365-install:setup` | Interactive wizard — provisions cloud resources, admin consent, writes manifest |
| `/claude-for-msft-365-install:manifest` | Generate the customized add-in manifest XML |
| `/claude-for-msft-365-install:consent` | Azure admin consent URL for the add-in's app registration |
| `/claude-for-msft-365-install:update-user-attrs` | Write per-user config via Microsoft Graph extension attributes |
| `/claude-for-msft-365-install:bootstrap` | Build the bootstrap endpoint — per-user MCP servers, skills, dynamic config |

## Notes (personal)

- I'm using this with **Bedrock** (us-east-1). Vertex AI setup is untested on my end.
- Run `:consent` before `:setup` if your tenant requires pre-approval for app registrations — saves having to re-run the wizard.
- The `:update-user-attrs` command requires `User.ReadWrite.All` in your app registration; easy to miss during initial consent.
- **Tip:** If the `:setup` wizard times out mid-run, it's usually the IAM role propagation lag on Bedrock — just wait ~30s and re-run; it's idempotent.
