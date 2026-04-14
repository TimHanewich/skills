# Tim's Agent Skills
This repository contains a number of [agent skills](https://agentskills.io/home) I've created that can be used with tools like Claude Code, GitHub Copilot, and others.

## Skills in this Repo
All skills can be found in the `.github/skills/` folder [here](./.github/skills/), but are also listed below.
- [msx](.github/skills/msx/) - interface with MSX, Microsoft's CRM system.
- [power-platform-architect](.github/skills/power-platform-architect/) - Solution Architect for the Microsoft Power Platform.

## Using a Skill
For a project skill, specific to a single repository, store under `.github/skills` or `.claude/skills`.

For personal skills, shared across all projects, store under `~/.copilot/skills` or `~/.claude/skills` (i.e. `C:\Users\timh\.copilot\skills`).

See documentation on your particular agent tool for further instructions, like [this for GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/create-skills) for example.

### Example
So, if you wanted to use the [msx](./msx/) skill across all projects for example, you would:
1. Clone this repo
2. Place the [msx](./msx/) folder directly under `C:\Users\<USER>\.copilot\skills`.