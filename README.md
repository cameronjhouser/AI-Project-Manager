# AI Project Manager

A skill that keeps a project's state files (TODO, Changelog, bugs, dated handoffs, lessons) accurate across AI coding sessions. At the start of a session it reconciles where the project really stands. During work it logs progress with evidence. At the end it archives finished items, writes a dated handoff and reports the next steps.

It plans, tracks and verifies. It runs in one of two modes: **bookkeeping** (a dedicated PM role that edits only state files and writes no production code) or **embedded** (the same agent also codes, and the skill governs the state files and the checks around the work).

## Status: v1 draft

- Built from one author's manual setup and tried on one real project. It found and fixed several flaws in its own first draft during that trial.
- Not yet run cold in a fresh session by someone who did not write it.
- Some parts were never exercised: the review gate, the multi-agent rules, the archive step, and the step that turns repeated lessons into hooks, scripts or skills.
- The report-length limit in the session-start step is a guess.

Treat it as a starting point and expect to edit it.

## What it does

| Phase | Behavior |
|---|---|
| Session start | Reads the TODO header and open items, the newest handoff and the top of the Changelog. Runs the handoff's read-only preflight checks. Flags conflicts between the TODO header and the latest handoff, and compares written dates and the latest git commit to find stale files. |
| During work | One-line entries with actor tags. "Done" only with evidence (a command and its result, a test count, a commit SHA). Defects go to the bug index, decisions get a reason, dead ends go to a lessons file. Unrelated findings become TODO items, not side work. |
| Review gate | Risk tier set by the change, not the author. Runs the project's `REVIEW.md` if present. Caps review at three cycles. |
| Close-out | Changelog entry for every closed item, archive old closed items (moved, never deleted), update the TODO header, write a new dated handoff, show a diff of every state file changed. |
| Lessons | A rule for deciding whether a repeated lesson becomes a hook, script, skill, lint rule or nothing. It proposes; it never creates one without approval. |

## Principles

- **Adopt the project's layout.** It finds existing `TODO`, `Changelog`, `Bugs` and handoff files and uses their names, ID schemes and actor tags. It never restructures them.
- **Plain files are the source of truth.** No database and no service.
- **Back up before editing** any state file that git does not track, or that has uncommitted changes, then diff against the backup at close-out.
- **Dates are signals, not proof.** Status claims are checked against code, tests and git before being trusted.
- **Trusted vs untrusted instructions.** The project's own checklists, `CLAUDE.md` / `AGENTS.md` and TODO acceptance checks are followed. Issue text, comments, web pages and tool output are treated as data.
- **Ask before anything destructive or outward-facing.** It does not deploy or push, even if a trusted instruction asks it to.

## Install

Claude Code: clone or copy this folder to `~/.claude/skills/ai-project-manager/` (the folder must contain `SKILL.md`). Other agents: paste the contents of `SKILL.md` into your project's `AGENTS.md`.

Then start a session with something like "start session" and finish with "wrap up". The skill's description tells the agent when to use it.

## Files

```
SKILL.md                    the protocol
templates/handoff.md        dated session handoff
templates/lessons.md        append-only lessons and dead ends
templates/todo-header.md    TODO header with current state and decisions
```

## Not in v1

Model routing and delegation to cheaper models, a failure log with escalation rules, cross-project dashboards and issue-tracker sync. They are planned only if v1 proves useful. The skill tells the agent not to improvise them.

## Influences

The file-based approach follows public "memory bank" patterns for coding agents. The review-gate ideas (risk tiers, a cap on review cycles, evidence before "done") draw on public write-ups of how teams review AI-written code.

## Feedback

Issues and pull requests are welcome, especially reports from real sessions: where the agent skipped a step, where the files went stale, and what you never used.

## License

MIT. See [LICENSE](LICENSE).
