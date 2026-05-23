# Playbooks

Reusable, cross-project tooling — a playbook codifies a repeatable task so any project's agents can run it consistently.

A playbook is one of two things:

1. A **properly-installed plugin skill** — auto-discovered by agents.
2. A **self-contained markdown file** — an agent is pointed at it explicitly ("Read this file and follow it as your instructions"). It must include a Prerequisites section (e.g. "request access to folder X") so it is robust to a fresh agent with no context.

A hand-written `SKILL.md` dropped in a plain workspace folder does **not** auto-register — it must be installed as a plugin, or treated as the markdown-file form above.

Add a playbook here when a task has been done the same way more than once and is worth standardizing.
