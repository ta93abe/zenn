# Repository Guidelines

## Project Structure & Module Organization
- `articles/` stores individual Zenn articles as Markdown. Each file should include full frontmatter (`title`, `emoji`, `type`, `topics`, `published`) so zenn-cli can publish without prompts.
- `books/` contains multi-chapter books; chapters live under `books/<slug>/chapters/`. Keep shared assets inside the sibling `images/` directory to avoid duplication.
- `CLAUDE.md` and `GEMINI.md` capture agent-specific instructions. Extend them rather than duplicating content.
- Tooling configs (`biome.json`, `package.json`, `pnpm-lock.yaml`, `volta` settings) live at the root; avoid moving them so Volta and CI resolve Node 24.11.1 consistently.

## Build, Test, and Development Commands
- `pnpm install` installs dependencies pinned in `pnpm-lock.yaml`; always rerun after changing zenn-cli or remark versions.
- `pnpm exec zenn new:article --slug your-slug` generates a pre-templated Markdown file in `articles/`. Use `new:book` similarly for books.
- `pnpm exec zenn preview --open` launches the local preview server on http://localhost:8000, enabling live reload for articles and books.
- `pnpm exec biome format .` and `pnpm exec biome lint .` keep Markdown and config files compliant with the shared `biome.json` rules.

## Coding Style & Naming Conventions
- Markdown files use 2-space indentation, fenced code blocks with explicit language tags, and hyphenated slugs (`cometa-terraform-guide`) matching filenames.
- Use descriptive headings that mirror the navigation titles, and keep frontmatter topics lowercase (`["terraform","analytics"]`).
- For images, place assets under `images/<feature>/` and reference them via relative paths so previews resolve offline.

## Testing Guidelines
- There is no automated test suite today; treat the preview as your integration test. Run `pnpm exec zenn preview` before each commit and verify links, diagrams, and code snippets render correctly.
- Validate Markdown structure with `pnpm exec biome lint articles books` to catch broken frontmatter, heading hierarchies, and unwanted tabs.
- When adding scripts or code samples, execute them (or their dry-run equivalents) locally and paste the exact command/output pair into the article.

## Commit & Pull Request Guidelines
- Follow the existing log style: short, imperative summaries (e.g., `refine table formatting in Terraform...` or `claude init`). Reference issues with `#<id>` when relevant and keep scope limited to one content piece per commit.
- Pull requests should include: purpose, key edits, screenshots of the Zenn preview for visual changes, and checklist items for commands run (`pnpm install`, `pnpm exec zenn preview`, `pnpm exec biome lint`). Link related CLAUDE/GEMINI updates when modifying agent workflows.
