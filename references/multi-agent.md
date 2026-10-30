# Working with other agents

- Re-read a state file immediately before editing it. Another agent may have changed it.
- Edit one TODO item at a time. Do not rewrite the file in one pass.
- If the project defines file or line-range ownership, follow it.
- If two agents must touch the same file, agree on boundaries first and merge sequentially, not in parallel.
- Keep every entry's actor tag. If you change an item another actor wrote, add your own dated, actor-tagged note beneath it (see section 6 of `SKILL.md`).
- If a file changed since you last read it and the change affects your edit, stop and report the conflict instead of overwriting.
