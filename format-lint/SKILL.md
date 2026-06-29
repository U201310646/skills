<!--
 * @Author: yurui cyrhust@163.com
 * @Date: 2026-06-29 21:31:26
 * @LastEditors: yurui cyrhust@163.com
 * @LastEditTime: 2026-06-29 21:40:28
 * @FilePath: /skills/format-lint/format-lint.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
---
description: Run ruff format and lint on git-changed Python files. Use with optional --staged flag for pre-commit check.
allowed-tools: Bash(git *), Bash(ruff *), Glob, Grep, Read, Edit
---

# Format & Lint (Changed Files Only)

## Steps

### 1. Get changed .py files

```bash
# Default: staged + unstaged + untracked
git diff --name-only HEAD --diff-filter=d -- '*.py'
git ls-files --others --exclude-standard -- '*.py'

# If $ARGUMENTS is --staged: only staged files
git diff --cached --name-only --diff-filter=d -- '*.py'
```

If no `.py` files changed, report "No changed Python files" and stop.

### 2. Format then lint

```bash
ruff format file1.py file2.py ...
ruff check --fix file1.py file2.py ...
```

### 3. Fix remaining errors

If `ruff check` reports unfixable errors, read the files and apply manual fixes:

| Rule | Fix |
|------|-----|
| `F841` | Remove unused variable |
| `F811` | Remove or rename redefined name |
| `F401` | Remove unused import |
| `E711` | `== None` → `is None` |

Re-run `ruff check` after fixes. Repeat until clean.

### 4. Report summary

List: files formatted, issues auto-fixed, issues manually fixed, issues remaining.
