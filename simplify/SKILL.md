---
name: simplify
description: Simplify, clean up, or improve recent code changes for reuse, clarity, efficiency, and appropriate abstraction while preserving behavior. Use for a focused cleanup pass on changed code or an explicitly named target, including requests to simplify after implementation. For correctness-only reviews, use the appropriate code review workflow instead.
---

# Simplify

Review the requested code for worthwhile cleanup, then apply safe improvements. Favor clarity over fewer lines and respect the project's instructions and established conventions. This is not a substitute for correctness review.

## 1. Establish the target

- Honor an explicit path, commit, branch, PR, focus, or read-only request. Resolve references with the tools available; if a target cannot be resolved, explain the limitation and ask for clarification.
- Otherwise inspect `git status --short` and `git diff HEAD` to identify staged and unstaged tracked changes, and inspect relevant untracked files as additions. Account for staged and unstaged versions when they differ; do not stage or unstage anything. In an unborn repository, inspect the index and working tree without relying on HEAD.
- If there is no target and no working-tree change, ask the user what to simplify. Do not silently choose the latest commit or the entire repository.
- Read the target's surrounding code and applicable project instructions. Capture enough change context for reviewers, including relevant untracked files. For a large diff, provide a reliable way to inspect all of it instead of silently truncating it.

## 2. Review in parallel

Launch four independent, read-only review subagents concurrently when delegation is available and permitted. Give each the same resolved target, change context, user focus, relevant instructions, and the guidance below. Ask for actionable findings with file locations, rationale, and behavior or verification risks; reviewers must not edit files. If delegation is unavailable or prohibited, perform the four reviews yourself and say so in the summary.

1. **Reuse:** Search adjacent code and shared utilities for existing helpers or patterns that genuinely replace duplication; check semantics before recommending reuse.
2. **Simplification:** Look for redundant state, needless branches or indirection, duplicated logic, excessive parameters, and confusing structure. Preserve useful comments and favor readable code over clever brevity.
3. **Efficiency:** Look for unnecessary computation, repeated I/O or requests, avoidable sequential work, hot-path overhead, no-op updates, and resource leaks. Consider observable ordering, error handling, and actual impact before proposing an optimization.
4. **Abstraction:** Check whether responsibilities and logic sit at the right level, interfaces expose unnecessary details, or new abstractions add complexity without paying for themselves. Follow existing architectural boundaries.

Review the current target's behavior, including edge cases and side effects, as the baseline—not the deleted side of a diff. Flag possible behavior changes separately rather than presenting them as safe cleanup. Avoid speculative or cosmetic findings.

## 3. Apply and verify

Wait for the reviews, inspect their evidence, deduplicate and reconcile overlapping findings, and apply worthwhile changes sequentially. Preserve existing user work. Stay within the requested scope; ask before changing behavior or expanding the scope. Skip uncertain or low-value suggestions rather than forcing a refactor. In read-only mode, report findings without modifying files.

Run appropriate focused tests or checks for the edits, and inspect the resulting diff. If verification cannot be run, say why; do not claim unrun checks passed. Briefly summarize the changes and verification, plus important skipped or behavior-changing findings. If nothing needs changing, say so.
