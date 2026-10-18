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

## Source of truth

The skill teaches Artifac's public contract as built, never plans. The product is the Artifac-Web repository (`Web/Artifac-Web` under the Artifac folder), and the project's decisions are in Artifac-Planning's `Context/`. Check every claim against these before changing it:

- Tool names, arguments, descriptions, and outputs: `packages/domain/src/mcp-tools.ts`
- Error codes and hints: `packages/domain/src/errors.ts`
- Paths, reserved directories, serving candidates, binary types: `packages/domain/src/paths.ts`
- Policies, configuration rules, and record shapes: `packages/domain/src/saved-data.ts` and `packages/domain/src/path-access.ts`
- Entry metadata: `packages/domain/src/metadata.ts`
- Runtime SDK and the frame it runs in: `packages/runtime/src/sdk.ts`, `packages/runtime/src/frame.ts`, and `apps/edge/src/headers.ts`
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
- Run the skill sync before committing.

## Open checks

- **Viewer identity.** `SKILL.md` and `references/saved-data.md` state that artifact code sees a signed-in viewer only as a pseudonym of that artifact. Artifac-Web's `dev` still puts the person's account-wide public ID in the runtime token's `sub`, and the change that makes it a per-artifact pseudonym waits on an unmerged branch. Recheck `packages/backend/convex/model/runtimeTokens.ts` once it merges, then delete this entry.

## Before finishing

- `node <skill-forge>/scripts/validate.mjs .` passes, or `npx --yes github:LeeorNahum/skill-forge-skill .`.
- Every support file named by `SKILL.md` exists and has a direct loading condition.
- `README.md` matches the actual file layout.
