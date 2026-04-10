# SSK Security Review Skill

Run a security review following the Startup Security Kit AI review process.

## Steps

Execute the following steps in order.

### 1. Get the code to review

```bash
git diff HEAD
```

If there are no changes, use `git diff HEAD~1` to check the most recent commit.
If there is no diff, read the `app/` directory directly.

### 2. Load ai-review.md

Read `startup-security-kit/docs/ai-review/ai-review.md` to understand the review process,
required review points, and output format.

> **Note**: If `startup-security-kit/` does not exist, check:
> - Is the submodule initialized? Run: `git submodule update --init`
> - Is the local symlink in place? Run: `ls startup-security-kit/`

### 3. Run the review

Strictly follow the **Required Review Points** and **Output Format** defined in `ai-review.md`.

## Notes

- Do not mechanically list checklist items
- Only report findings tied to actual code
- If unsure, explicitly say "Needs confirmation"
- Do not over-report low-value issues

---

## Output Language

Output all review findings in **Japanese (日本語)**.

> To switch back to English (the default), remove this section or change the value to `English`.
