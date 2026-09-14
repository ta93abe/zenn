# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Zenn content repository for publishing technical articles. Zenn is a Japanese technical publishing platform. The repository uses Zenn CLI to manage and preview content locally before publishing.

## Development Commands

### Content Management

- `npx zenn preview` - Start local preview server to view articles and books in browser
- `npx zenn new:article` - Create new article with proper frontmatter
- `npx zenn new:book` - Create new book
- `npx zenn list:articles` - List all articles
- `npx zenn list:books` - List all books

### Code Quality

- `pnpm exec oxlint --no-error-on-unmatched-pattern` - Run Oxlint
- `pnpm exec oxfmt` - Format with Oxfmt
- `pnpm exec oxfmt --check` - Check formatting without writing
- `pnpm run lint` - Run Oxlint, Oxfmt check, textlint, and cspell

### Package Management

- `pnpm install` - Install dependencies
- Package manager: pnpm@10.22.0

## Architecture

### Content Structure

- `articles/` - Markdown files for individual articles with YAML frontmatter
- `books/` - Directory for book content (currently empty)
- `images/` - Static assets for articles (PNG files)

### Article Format

Articles use YAML frontmatter with:

- `title` - Article title in Japanese
- `emoji` - Display emoji
- `type` - Either "tech" (technical) or "idea"
- `topics` - Array of topic tags
- `published` - Boolean publication status

### Configuration

- Oxlint configuration in `.oxlintrc.json` (correctness + suspicious)
- Oxfmt configuration in `.oxfmtrc.json` with:
  - Tab indentation
  - Double quotes for JavaScript
  - Import sorting enabled
  - Articles and books excluded from formatting

## Content Guidelines

All content is in Japanese and focuses on technical topics including:

- Infrastructure (dbt, Cloudflare Pages, Terraform)
- Development environment setup (WSL2)
- Data engineering workflows

When creating new articles, use `npx zenn new:article` to ensure proper frontmatter structure.
