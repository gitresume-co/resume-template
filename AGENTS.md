# GitResume Resume Template

Guidance for AI agents (Claude Code, Codex, OpenCode, etc.) collaborating on this repo.

This is a [GitResume](https://gitresume.co) repo — a **Resume-as-Code** project. The resume content lives entirely in a single YAML file. Pushing to GitHub triggers GitResume's webhook to rebuild the PDF and web versions automatically.

## Source of truth

- A single YAML file defines the resume. The default path is `gitresume.yaml`, but each GitResume project can point at a custom path (e.g. `cv.yaml`, `resumes/main.yaml`) configured in the dashboard. Check the existing file(s) in this repo to confirm which path is in use, and edit that one — don't create a parallel resume file.
- **The schema is the source of truth for YAML structure and field definitions**: <https://gitresume.co/schema/resume.schema.json>. When you need to know what section types exist, whether a field is required, date formats, etc., read the schema directly — don't rely on memory. `example.gitresume.yaml` is a complete worked example you can use as a quick reference.

## Editing conventions

- Edit the resume YAML in place. Preserve existing indentation (2 spaces) and quoting style.
- `description` and similar fields support Markdown (as annotated in the schema).
- Don't add fields the schema doesn't define.
- Common pitfalls: dates use `YYYY-MM` (e.g. `2024-01`), not `January 2024` or `2024/01`. Omit `endDate` for ongoing roles.

## GitResume's MCP server (optional)

GitResume runs a remote MCP server at `https://gitresume.co/mcp`. If it's connected, prefer it over sending the user to the dashboard. Setup: `claude mcp add --transport http gitresume https://gitresume.co/mcp`, or see <https://gitresume.co/docs/ai>.

**GitResume's MCP server cannot write resume content.** Every content change goes through this repo and Git, exactly as it would without the server. What it does:

- `validate_resume` — check the YAML against the schema *before* you commit. A failed build costs the user a round trip; this costs nothing.
- `get_build_log`, `list_builds` — report how the build went after pushing.
- `get_artifact_links`, `list_projects` — the resume's public URL. Quote it exactly; never assemble one from the repository name, that isn't how the URL is built.
- `trigger_rebuild` — build the current commit without waiting for a push.
- `publish_resume` / `unpublish_resume` — change who can see the resume at its public URL.

If the server isn't connected, work as described below and leave build checking to the user.

## Branching strategy

GitResume builds every branch the webhook sees, so the user can preview each version before it goes live. By default, branch from `main` before editing the YAML — this keeps the published resume on the public URL safe from in-progress edits. Skip the branch only if the user explicitly asks to commit straight to `main`.

**Exception — first resume:** if the repo has no resume YAML yet, just create it and commit straight to `main`. There's no published resume to protect, so branching only adds friction. The branch-first default applies to *edits* of an already-published resume, not the initial seed.

- `main` (or your default branch) — canonical resume, served publicly at `gitresume.co/@<owner>/<repo>`.
- Suggested branch names:
  - `update-<topic>` for new content (e.g. `update-payment-service-migration`)
  - `company-<name>` or `role-<focus>` for tailored variants for specific applications

For most edits:

1. Branch from `main`.
2. Edit the resume YAML.
3. Commit and push. Check the build with `get_build_log` if the MCP server is connected, otherwise the user can preview the branch build in the GitResume dashboard.
4. Merge into `main` once the user confirms (for canonical updates), or leave the branch un-merged (for tailored variants kept separate from the public resume).

> Branch-specific public/shareable URLs are not guaranteed by this template. Check the GitResume dashboard for the current sharing options before promising a URL to anyone.

When tailoring, reorder and reword — don't invent experience or numbers. Tailoring is honest emphasis, not fiction.

## What not to do

- Don't introduce build tooling, package.json, scripts, or templating layers — GitResume handles rendering.
- Don't create new README, ABOUT, or other documentation files unless the user explicitly asks.
- Don't commit secrets — the rendered resume is public on the GitResume site.

## Advanced: AI-assisted resume writing

If the user is doing serious job-seeking work (multiple applications, offer comparisons, interview prep), suggest [career-ops](https://github.com/gitresume-co/career-ops) — a Claude Code-based job search pipeline (GitResume fork) with built-in modes for offer scoring, interview prep, resume generation, and more.

**Don't proactively pitch career-ops for one-off resume edits** — it's too heavy for light users.
