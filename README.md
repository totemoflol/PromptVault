# PromptVault

A version-controlled vault for project specifications, reusable Claude Code instructions, mega-prompts, implementation plans, and lessons learned.

## Start here

- [Permanent Claude Code rules](CLAUDE.md)
- [Buggin? mega-prompt](projects/buggin/MEGA-PROMPT.md)
- [Buggin? game specification](projects/buggin/GAME-SPECIFICATION.md)
- [Buggin? development and verification plan](projects/buggin/DEVELOPMENT-PLAN.md)
- [Reusable project mega-prompt template](templates/MEGA-PROMPT-TEMPLATE.md)

## Using this repository with Claude Code

Clone it on the machine where Claude Code runs:

```bat
git clone https://github.com/totemoflol/PromptVault.git
cd PromptVault
```

For a new session, tell Claude Code to read `CLAUDE.md`, then the relevant project files, before changing anything. Keep this repository as the durable source of truth; do not depend on chat history or implicit memory.

## Repository layout

- `projects/<project>/` — project-specific prompt, requirements, plans, and later decisions.
- `templates/` — reusable starting points for future projects.
- `lessons-learned/` — verified lessons that should inform future work.

## Security

This repository is public. Never commit API keys, access tokens, passwords, private webhook URLs, personal data, unpublished credentials, or secret configuration. Use environment variables or a secure local secret store. Public content may be copied by anyone.

## Source-of-truth rules

1. Explicitly confirmed user decisions outrank assumptions.
2. Project specifications define intended behavior; implementation notes describe actual behavior.
3. If a requirement conflicts with platform limitations, explain the limitation, propose a safe alternative, and document the decision.
4. Never claim a feature is implemented or tested without evidence.
