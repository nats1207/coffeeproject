# Repository Guidelines

## Project Structure & Module Organization

This is a content-only repository for Markdown guides, ideas, and AI-agent context. There is no application source tree, package manager setup, or generated build output.

- `simplify_your_life.md`: core lifestyle and habit reference.
- `blog_posts_ideas.md`: content ideas derived from the lifestyle guide.
- `homelab_starting_kit.md`: homelab-oriented guide content.
- `gemini_cli_architecture_overview.md`: reference notes about Gemini CLI architecture.
- `GEMINI.md`, `CLAUDE.md`, and `AGENTS.md`: tool-specific contributor guidance. Keep overlapping guidance consistent across these files.
- `.claude/agents/`: Claude agent definitions used by local tooling.

Add new long-form content as top-level `.md` files unless a clear subdirectory becomes necessary.

## Build, Test, and Development Commands

There are currently no build steps, runtime dependencies, or automated tests. Useful local commands are:

- `rg "phrase"`: search all Markdown content quickly.
- `git status`: review changed files before committing.
- `git diff -- *.md`: inspect Markdown edits.

If tooling is added later, document the exact commands here before relying on them.

## Coding Style & Naming Conventions

Use Markdown with ATX headings (`#`, `##`, `###`) and short, scannable sections. Prefer bullet lists for actionable guidance. Existing content often uses bold labels inside bullets, for example `- **Digital Life:** ...`.

Use lowercase snake_case for new Markdown filenames, such as `weekly_reset_checklist.md`. Keep filenames descriptive and content-focused. Avoid unnecessary HTML, embedded scripts, or formatting that makes plain-text review difficult.

## Testing Guidelines

No formal test framework exists. Treat review as editorial validation:

- Confirm headings form a logical outline.
- Check examples and commands for accuracy.
- Run `rg` to catch duplicated titles, inconsistent terminology, or stale references.
- Preview Markdown when layout matters.

## Commit & Pull Request Guidelines

Git history currently contains one simple commit: `First commit`. Until a fuller convention emerges, use concise, imperative commit messages such as `Add homelab guide outline` or `Update agent guidance`.

Pull requests should include a short description, list the files changed, and explain the purpose of content additions. Link related issues when available. Include screenshots only when Markdown rendering or visual layout is important.

## Agent-Specific Instructions

This repository is mostly prose. Preserve the authorial tone, avoid broad rewrites unless requested, and keep new guidance aligned with `CLAUDE.md` and `GEMINI.md`.
