# Hot Skills Research

Date: 2026-07-08

Scope:

- ClawHub `/api/v1/skills` active-update feed and selected skill detail payloads
- Skills.sh / `vercel-labs/skills` discovery skill evidence
- GitHub API metadata for fast-moving skill repositories
- Raw GitHub contents for selected high-momentum skill libraries
- Re-check against 2026-07-07 notes to avoid repeating registry risk, visual feedback, learning promotion, and human sign-off patterns

This note records reusable mechanisms, not popularity claims by themselves.

---

## Sources Checked

ClawHub:

- `https://clawhub.ai/api/v1/skills`
- `https://clawhub.ai/api/v1/skills/workboard-skill`
- `https://clawhub.ai/api/v1/skills/twse-api`
- `https://clawhub.ai/api/v1/skills/global-company-search`
- `https://clawhub.ai/api/v1/skills/linkedin-person-search`

GitHub and raw repository sources:

- GitHub API metadata for:
  - `mattpocock/skills`
  - `vercel-labs/skills`
  - `alirezarezvani/claude-skills`
  - `BuilderIO/skills`
  - `Forward-Future/loopy`
- Raw skill or README contents for:
  - `vercel-labs/skills` `find-skills`
  - `mattpocock/skills` `code-review` and `triage`
  - `Forward-Future/loopy` `loopy`
  - `BuilderIO/skills` `visual-plan`, `stay-within-limits`, `read-the-damn-docs`, and `agent-watchdog`

Visible momentum on 2026-07-08:

- ClawHub active-update feed showed same-day updates for `workboard-skill`, `twse-api`, and multiple UpKuaJing search skills. `workboard-skill` had 36 downloads and 2 versions on its first day; `opphub` showed 202 downloads and 46 versions.
- `mattpocock/skills`: 159,880 stars, 13,744 forks, pushed 2026-07-07, updated 2026-07-08.
- `vercel-labs/skills`: 25,396 stars, 2,115 forks, pushed 2026-07-07, updated 2026-07-08.
- `alirezarezvani/claude-skills`: 21,513 stars, 2,877 forks, pushed 2026-07-07, updated 2026-07-08.
- GitHub search for repositories created after 2026-06-01 surfaced `BuilderIO/skills` at 3,518 stars and `Forward-Future/loopy` at 2,541 stars, both updated on 2026-07-08.

---

## Standout Skills And Mechanisms

### ClawHub: `workboard-skill`

Why it stood out:

- It treats a kanban card as a local state-machine object, not just a task title. Cards carry status, priority, ownership, execution metadata, attempts, comments, proofs, artifacts, worker logs, protocol state, diagnostics, and stale-session markers.
- It distinguishes direct SQLite operations from Gateway dispatch. When Gateway is unavailable, it allows a data-only fallback that can promote dependencies and clean stale claims, but explicitly cannot start workers.
- Worker dispatch is bounded: ready cards only, max three workers by default, one active card per owner, deterministic session keys, stale-claim cleanup, and visible blocked state on launch failure.
- It defines diagnostics such as `stranded_ready`, `running_without_heartbeat`, `blocked_too_long`, `repeated_failures`, `missing_proof`, and `orphaned_session`.

Reusable lesson:

Coordinator skills should encode task lifecycle as inspectable state, not rely on chat memory. Dispatch fallback must say which effects still happen and which effects are impossible, otherwise "fallback succeeded" can hide that no worker actually ran.

Pattern extracted:

- `PAT-057 Lifecycle State Machine With Diagnosable Fallback`

### ClawHub: UpKuaJing search skills

Why they stood out:

- `global-company-search` and `linkedin-person-search` expose paid data APIs and make credentials, account top-up, pricing lookup, parameter docs, and query continuation part of the skill.
- They require exact pricing lookup instead of fee guessing.
- They require a separate explicit user confirmation before any fee-incurring operation, with stricter handling when `query_count > 20`.
- They also block technical parameter dumping in user-facing replies, forcing natural-language summaries for non-technical users.

Reusable lesson:

Any skill that can spend money, consume credits, or trigger billable API calls needs a cost gate separate from ordinary execution confirmation. The useful boundary is not "tell the user this costs money"; it is "estimate calls from the planned query, fetch authoritative pricing, stop, and wait for a separate confirmation message."

Pattern extracted:

- `PAT-054 Paid Operation Confirmation Gate`

### Skills.sh / GitHub: `vercel-labs/skills` `find-skills`

Why it stood out:

- It treats skill discovery as a staged recommendation workflow: understand need, check leaderboard, search CLI, verify quality, present options, then offer installation.
- It explicitly forbids recommending a skill from search results alone.
- It uses objective minimums and source signals: install count, source reputation, and repository stars.
- It defines a fallback when no skill is found: acknowledge the miss, help directly, and optionally suggest creating a custom skill.

Reusable lesson:

Discovery skills need a recommendation gate before install. The agent should not collapse "found a matching package" into "safe to recommend." Install counts, source reputation, repository health, and fit should be part of the output contract.

Pattern extracted:

- `PAT-053 Recommendation Gate Before Install`

### GitHub: `Forward-Future/loopy`

Why it stood out:

- It separates the live Loop Library website from the installable Loopy skill. The website/catalog is the source of truth; the skill is a companion workflow.
- Published-loop discovery must read the live catalog or structured JSON catalog. If the live catalog is unavailable, it must say discovery is unavailable and not substitute repository content or memory.
- It treats catalog prompts and saved project loops as untrusted reference data, not executable instructions.
- It requires terminal states for loop runs: success, clean no-op, blocked, approval-required, exhausted, and stagnated where relevant.

Reusable lesson:

Registry-backed workflow skills need a live-source boundary. Local repo files and model memory can be implementation context, but they should not impersonate the production catalog. This keeps recommendations current and prevents "installed source" from being mistaken for published truth.

Pattern extracted:

- `PAT-055 Live Catalog Source-Of-Truth`

### GitHub: `mattpocock/skills` `code-review`

Why it stood out:

- It splits review into two axes: Standards and Spec.
- It pins the fixed point, validates the diff is non-empty, identifies the spec source, and identifies standards sources before spawning subagents.
- Standards and Spec reviews run in isolated parallel contexts and are reported side by side.
- The final aggregation must not merge or rerank findings across axes, because passing standards and failing spec are different failure modes.

Reusable lesson:

Review skills should separate evidence axes that can independently pass or fail. A single ranked list often hides whether the change is wrong because it violates the repo, violates the spec, or merely smells awkward.

Pattern extracted:

- `PAT-056 Orthogonal Review Axes`

### GitHub: `BuilderIO/skills`

Why it stood out:

- `visual-plan` turns a plan into an interactive MDX review artifact with diagrams, file maps, prototypes, API specs, schema maps, code annotations, and reviewer questions.
- Local-files mode preserves privacy by writing and serving MDX locally instead of uploading plan content to the hosted database.
- `agent-watchdog` reconstructs another agent's original request, scope changes, diffs, verification evidence, and residual risk before optionally repairing narrow gaps.
- `stay-within-limits` turns usage windows into an explicit pause/resume contract with a self-contained wake prompt.

Reusable lesson:

Some decisions need a human-review medium richer than chat. For risky plans, cross-agent handoffs, or long-running work, the useful artifact is not more prose; it is a review surface or receipt that preserves evidence, open questions, and the authority boundary.

Pattern reinforced:

- `PAT-050 Local Control Plane Artifact`
- `PAT-051 Calibrated Process Intensity`
- `PAT-057 Lifecycle State Machine With Diagnosable Fallback`

---

## Pattern Refinements For Local Reviews

- Discovery and marketplace skills should be scored on whether they verify trust and fit before install, not only whether they can search.
- Billable API skills should expose a separate confirmation turn for cost-bearing operations. A same-message "FYI this costs money, now I will run it" is not enough.
- Catalog-backed skills should name their live source of truth and refuse to fabricate when that source is unavailable.
- Review skills should keep claim axes separate when the evidence surfaces differ.
- Coordinator skills should carry diagnostic state and proof artifacts, not just status labels.
