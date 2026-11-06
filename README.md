# Simplify skill for OpenCode

An OpenCode skill inspired by Claude Code's `/simplify`. It reviews code changes for reuse, clarity, efficiency, and the right level of abstraction, then applies worthwhile improvements while preserving behavior.

By default, it reviews staged, unstaged, and relevant untracked changes. You can also specify a target or ask for a read-only report. If there are no changes and no target, it asks what to review. When permitted and available, four independent subagents review in parallel; otherwise, the review runs locally.

## Install

Clone this repository, then copy the skill into your global OpenCode skills directory:

```sh
git clone https://github.com/MatusTabi/simplify-skill.git
mkdir -p ~/.config/opencode/skills/simplify
cp simplify-skill/simplify/SKILL.md ~/.config/opencode/skills/simplify/SKILL.md
```