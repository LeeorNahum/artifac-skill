# artifac-skill

`artifac` is an Agent Skill for building and maintaining interactive static artifacts on [Artifac](https://artif.ac): creating and updating them, saved data, metadata, file transfer, and error recovery, through Artifac's MCP tools, HTTP API, and CLI.

## Files

- `SKILL.md` holds the working rules and routes to everything else.
- `references/saved-data.md` covers collection policies, the data and configuration files, and the runtime SDK.
- `references/errors.md` gives the next move for each error code.
- `references/http-and-cli.md` covers the `npx artifac` CLI and the HTTP API, uploads included.
- `assets/saved-data-starter.html` is a one-file page that keeps a shared list, to copy and adapt.
- `AGENTS.md` is the maintenance contract for editing this skill.

## Install

The [Artifac plugin](https://github.com/LeeorNahum/Artifac-Plugin) installs this skill together with the Artifac MCP server for Claude Code, Codex, and ChatGPT.

To add only the skill, copy `SKILL.md`, `LICENSE`, `references/`, and `assets/` into a folder named `artifac` in your agent's skills directory, or add this repository to another as a submodule:

```bash
git submodule add https://github.com/LeeorNahum/artifac-skill.git .agents/skills/artifac
```

Licensed under the [Apache License 2.0](LICENSE).
