# GEMINI.md

## Directory Overview

This directory is a content repository for the [Zenn](https://zenn.dev) platform. It contains technical articles and potentially books written in Markdown.

The project is set up to use the [Zenn CLI](https://zenn.dev/zenn/articles/zenn-cli-guide) for creating and previewing content.

## Key Files

*   `articles/`: This directory contains the articles, with each article being a separate Markdown file.
*   `books/`: This directory is likely for book-length content, also in Markdown.
*   `package.json`: This file defines the project's dependencies, which include `zenn-cli` and `remark`.
*   `pnpm-lock.yaml`: This is the lock file for the pnpm package manager, ensuring consistent dependency installation.
*   `README.md`: This file provides a link to the Zenn CLI guide.
*   `images/`: This directory stores images used in the articles and books.

## Usage

This repository is used for writing and managing content for the Zenn platform. The typical workflow would be:

1.  **Create new content:** Use the Zenn CLI to create new articles or books.
    ```bash
    npx zenn new:article
    npx zenn new:book
    ```

2.  **Write content:** Edit the Markdown files in the `articles/` or `books/` directories.

3.  **Preview content:** Run the Zenn CLI's preview server to see how the content will look on the Zenn website.
    ```bash
    npx zenn preview
    ```

4.  **Publish content:** Once the content is ready, it can be published to the Zenn platform by pushing the changes to the linked GitHub repository.
