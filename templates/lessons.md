# Lessons

> Append-only. One entry per lesson or dead end. Read this before starting a fix or feature.
> Tag each entry with the actor: [Codex], [Claude], [Sam].

## Entry format

### L-NNN Short title — YYYY-MM-DD [Actor]

- **Type:** lesson | dead end
- **Tag:** <one short tag, reused across entries so repeats can be counted>
- **What happened:** <what was tried or what went wrong>
- **Why:** <root cause, or why the approach failed>
- **Evidence:** <command output, commit, log path>
- **Do instead:** <the working approach, or "avoid">
- **Seen:** <count and dates of recurrences>
- **Automation decision:** hook | script | skill | lint rule | doc line | nothing — <date, reason>

---

## Example

### L-001 A running service keeps old code after a deploy — 2026-01-15 [Claude]

- **Type:** lesson
- **Tag:** stale-process
- **What happened:** A fix was committed and deployed, but live behavior did not change.
- **Why:** The service process started before the commit and held the old code in memory. The deploy did not restart it.
- **Evidence:** The health endpoint reported the previous release SHA.
- **Do instead:** After every deploy, check that the health endpoint reports the commit just deployed. Restart the process if it does not.
- **Seen:** 1 (2026-01-15)
- **Automation decision:** script — deterministic check, needed every deploy (proposed, not yet approved)
