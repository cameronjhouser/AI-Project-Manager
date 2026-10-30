# Lessons and automation

## Logging

Add an entry to the lessons file (format in `templates/lessons.md`) when:

- an approach is abandoned (type: dead end), or
- something went wrong or surprised you and the next session should know.

Give every entry one short **tag** (for example `stale-process`, `quota`, `race`). Reuse an existing tag when one fits.

## Counting a repeat

A lesson is a repeat when its tag, or two or more distinctive keywords from its title, already appear in the lessons file or in a Changelog entry. Search with `grep -n -i <tag>`. On a match, add the date to the existing entry's **Seen** line instead of writing a new entry.

## Automation proposals (off by default)

Proposals are governed by `LESSON_AUTOMATION` (default `off`). While off, log lessons and count repeats, but do not propose automation. When the user sets it to `on`, propose automation for a lesson on its second occurrence, or on its first if the Changelog or handoff records it as costing a day or more.

| If the fix is... | Then propose a... |
|---|---|
| Needed every time, no judgment (verify the deployed SHA matches the commit, scan for secrets before commit) | **Hook** or **script** |
| A repeatable procedure that needs judgment or context | **Skill** |
| Rules for how code is written | **Lint rule** or `CLAUDE.md` / `REVIEW.md` line |
| Happened once and is still changing | **Nothing**; keep the lesson note |

Record the choice and date in the entry's **Automation decision** line. Propose only; never create a hook, skill or script without the user's approval.
