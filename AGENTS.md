# Repository Guidelines

## Project Structure & Module Organization

- `articles/` stores individual Zenn articles as Markdown. Each file should include full frontmatter (`title`, `emoji`, `type`, `topics`, `published`) so zenn-cli can publish without prompts.
- `books/` contains multi-chapter books; chapters live under `books/<slug>/chapters/`. Keep shared assets inside the sibling `images/` directory to avoid duplication.
- `CLAUDE.md` and `GEMINI.md` capture agent-specific instructions. Extend them rather than duplicating content.
- Tooling configs (`.oxlintrc.json`, `.oxfmtrc.json`, `package.json`, `pnpm-lock.yaml`) live at the root; avoid moving them so Corepack and CI resolve pnpm 10.22.0 consistently.

## Build, Test, and Development Commands

- `pnpm install` installs dependencies pinned in `pnpm-lock.yaml`; always rerun after changing zenn-cli or remark versions.
- `pnpm exec zenn new:article --slug your-slug` generates a pre-templated Markdown file in `articles/`. Use `new:book` similarly for books.
- `pnpm exec zenn preview --open` launches the local preview server on http://localhost:8000, enabling live reload for articles and books.
- `pnpm exec oxfmt` and `pnpm exec oxlint` keep JavaScript/TypeScript and config files compliant with `.oxfmtrc.json` / `.oxlintrc.json`.

## Coding Style & Naming Conventions

- Markdown files use 2-space indentation, fenced code blocks with explicit language tags, and hyphenated slugs (`cometa-terraform-guide`) matching filenames.
- Use descriptive headings that mirror the navigation titles, and keep frontmatter topics lowercase (`["terraform","analytics"]`).
- For images, place assets under `images/<feature>/` and reference them via relative paths so previews resolve offline.

## Testing Guidelines

- There is no automated test suite today; treat the preview as your integration test. Run `pnpm exec zenn preview` before each commit and verify links, diagrams, and code snippets render correctly.
- Validate Japanese Markdown with `pnpm exec textlint articles/**/*.md` and spelling with `pnpm exec cspell articles/**/*.md`.
- When adding scripts or code samples, execute them (or their dry-run equivalents) locally and paste the exact command/output pair into the article.

## Commit & Pull Request Guidelines

- Follow the existing log style: short, imperative summaries (e.g., `refine table formatting in Terraform...` or `claude init`). Reference issues with `#<id>` when relevant and keep scope limited to one content piece per commit.
- Pull requests should include: purpose, key edits, screenshots of the Zenn preview for visual changes, and checklist items for commands run (`pnpm install`, `pnpm exec zenn preview`, `pnpm exec oxlint`, `pnpm exec oxfmt --check`). Link related CLAUDE/GEMINI updates when modifying agent workflows.
