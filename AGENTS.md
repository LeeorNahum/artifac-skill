# AGENTS.md

Rules for editing the **artifac** skill. User-facing guidance lives in `SKILL.md` and its references. `README.md` is the human skim layer.

## File roles

| File | Role |
| --- | --- |
| `SKILL.md` | Always-needed rules: surfaces, creating, changing files, transfer routes, metadata, paths, the page's runtime, viewer identity, errors, limits |
| `references/saved-data.md` | Collection policies, the configuration and data files, replacement semantics, the runtime SDK |
| `references/errors.md` | The next move for each error code |
| `references/http-and-cli.md` | The CLI's commands and the HTTP API's routes, uploads, receipts, and errors |
| `assets/saved-data-starter.html` | A copyable one-file page using the SDK the way the references teach |
| `README.md` | Short human summary |
| `LICENSE` | Apache License 2.0, the same as the plugin that bundles the skill |

## Source of truth

The skill teaches Artifac's public contract as built, never plans. The product is the Artifac-Web repository (`Web/Artifac-Web` under the Artifac folder), and the project's decisions are in Artifac-Planning's `Context/`. Check every claim against these before changing it:

- Tool names, arguments, descriptions, and outputs: `packages/domain/src/mcp-tools.ts`
- Error codes and hints: `packages/domain/src/errors.ts`
- Paths, reserved directories, serving candidates, binary types: `packages/domain/src/paths.ts`
- Policies, configuration rules, and record shapes: `packages/domain/src/saved-data.ts` and `packages/domain/src/path-access.ts`
- Entry metadata: `packages/domain/src/metadata.ts`
- Runtime SDK and the frame it runs in: `packages/runtime/src/sdk.ts`, `packages/runtime/src/frame.ts`, and `apps/edge/src/headers.ts`
- Viewer identity: `packages/backend/convex/model/pseudonyms.ts` and `model/runtimeTokens.ts`
- Link preview card: `apps/edge/src/shell.ts` and the site's `/{uid}/__artifac/card.png` route
- Receipts and replacement: `packages/backend/convex/model/receipts.ts`, `model/changes.ts`, and `model/data.ts`
- Transfer: `packages/gateway/src/transfer.ts`, `apps/api/src/contract.ts`, and `apps/cli/src/cli.ts`

## Editing

- Never copy a numeric allowance or limit into the skill. Point at where the product reports it at run time.
- Teach only what an agent would get wrong without it. Backend enforcement stays in the product, so the skill describes the contract, not how it is enforced.
- Keep one `index.html` a complete artifact in every example.
- Quote every frontmatter string value. Keys stay unquoted.
- No em dashes, and no semicolons joining what should be separate sentences.
- Capitalized bullets and parallel list voice.
- Bump `metadata.version` by the release-versioning skill's rules for skills.
- Before committing, bring the installed skills current with `git submodule update --remote -- .agents/skills`, and when one changes, regenerate `CLAUDE.md` with `npx --yes github:LeeorNahum/claude-code-compat-skill`.

## Before finishing

- `node <skill-forge>/scripts/validate.mjs .` passes, or `npx --yes github:LeeorNahum/skill-forge-skill .`.
- Every support file named by `SKILL.md` exists and has a direct loading condition.
- `README.md` matches the actual file layout.
