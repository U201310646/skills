<!--
 * @Author: yurui cyrhust@163.com
 * @Date: 2026-06-29 21:31:36
 * @LastEditors: yurui cyrhust@163.com
 * @LastEditTime: 2026-06-29 21:40:25
 * @FilePath: /skills/git-commit/SKILL.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
---
name: git-commit
description: >-
  Review staged and unstaged changes, generate a Conventional Commit message,
  and create a git commit. Use when asked to commit, summarize diffs, stage
  changes, or write commit messages.
---

# Git Commit

## Workflow

1. **Inspect** — run `git status` and `git diff HEAD` to understand all changes.
2. **Stage** — add specific files with `git add <file>`. Avoid `git add -A` to prevent committing secrets (`.env`, credentials, etc.).
3. **Analyze** — read the staged diff, determine the best commit type.
4. **Commit** — write a message following the rules below and run `git commit`.

## Conventional Commit Format

```
<type>(<scope>): <subject>
                                    ← blank line
<body>                              ← optional
```

### Types

| Type       | When to use                                    |
|------------|------------------------------------------------|
| `feat`     | New feature or capability                      |
| `fix`      | Bug fix                                        |
| `refactor` | Code restructuring (no new feature, no bug fix)|
| `perf`     | Performance improvement                        |
| `build`    | Build system, dependencies, Docker, CI/CD      |
| `docs`     | Documentation only                             |
| `test`     | Adding or updating tests                       |
| `style`    | Formatting, whitespace (no logic change)       |
| `chore`    | Maintenance tasks that don't fit above          |

### Scope (optional)

Short module or area name in parentheses: `feat(detector)`, `fix(loss)`, `build(docker)`.

### Rules

- Subject: lowercase, imperative mood, no period, ≤ 72 chars.
- Body: explain **why**, not what. Only add when the diff is non-obvious.
- One logical change per commit. If the diff covers multiple topics, split into separate commits.

## Examples

**Single-line:**
```
feat(backbone): add DINOv3 backbone support
```

**With body:**
```
fix(voxel): resolve out-of-bounds access in scatter_points

The CUDA kernel assumed contiguous point indices. Added bounds
checking to handle sparse inputs from nuScenes sweeps.
```

**Build / infra:**
```
build(docker): migrate from shell scripts to docker-compose
```

## Guard Rails

- Never commit files matching: `.env*`, `*credentials*`, `*secret*`, `*.pem`, `*.key`.
- If unsure whether a file should be committed, ask before staging.
- Do not amend commits that have already been pushed.
- Do not use `--no-verify` unless explicitly requested.
