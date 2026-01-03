# Git Workflow Guide

## Conventional Commits

Use [Conventional Commits](../conventional-commits.md) for all commit messages.

**Format:**
```
<type>[optional scope]: <description>
```

**Types:**
| Type | Use for |
|------|---------|
| `feat` | New features |
| `fix` | Bug fixes |
| `docs` | Documentation only |
| `style` | Formatting, no code change |
| `refactor` | Code restructure, no behavior change |
| `perf` | Performance improvements |
| `test` | Adding/updating tests |
| `chore` | Maintenance tasks |
| `build` | Build system changes |
| `ci` | CI/CD configuration |

**Examples:**
```
feat(auth): add login screen with Supabase integration
fix(scanner): handle low-light QR scanning
docs: update README with setup instructions
refactor(drinks): extract age limit logic to hook
```

---

## Branch Naming

**Format:**
```
<type>/JSU-<issue-number>-<short-description>
```

**Examples:**
```
feat/JSU-42-add-qr-scanner
fix/JSU-99-login-session-persistence
refactor/JSU-150-drink-tracking-hooks
```

**Rules:**
- Use lowercase
- Use hyphens to separate words
- Keep descriptions short (3-5 words max)
- Always include the Linear issue number

---

## Pull Requests

**Title:** Follow conventional commit format
```
feat(scanner): implement QR code scanning [JSU-42]
```

**Description template:**
```markdown
## What
Brief description of changes.

## Why
Link to Linear issue and context.

## How to test
1. Step one
2. Step two
```

---

## Code Review

- **Minimum 1 reviewer** required before merge
- Reviewer checks:
  - Does it work on iOS and Android?
  - Does it match Figma design (if UI)?
  - Any edge cases missed?
  - Romanian text correct?
- Author addresses all comments before merge

---

## Merging

- **Never** commit directly to `main`
- Use **squash merge** to keep history clean
- Delete branch after merge
- Ensure CI passes before merging

**How to squash merge on GitHub:**
1. Open your PR on GitHub
2. Click the dropdown arrow on the green **Merge** button
3. Select **Squash and merge**
4. Edit the commit message to follow conventional commit format
5. Click **Confirm squash and merge**
6. Delete the branch when prompted
