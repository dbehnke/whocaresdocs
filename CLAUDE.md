# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains documentation for the **Whocares Amateur Radio Group**. The site is built using MkDocs with the Material theme and will be published at https://whocaresradio.com/docs.

- **Repository**: dbehnke/whocaresdocs
- **GitHub Workflow**: Use the `gh` CLI tool for repository interactions
- **Deployment**: Manual deployment offsite (no CI deployment currently)

## Technology Stack

- **MkDocs** with Material theme for static site generation
- **uv** for Python dependency management
- **Markdown** as the primary documentation format
- **Shell Support**: Fish shell (primary author's preference) and Bash

## Project Structure

```
whocaresdocs/
├── docs/              # Source markdown documentation
│   ├── index.md      # Main landing page
│   ├── general/      # General category documentation
│   └── howto/        # How-to guides and tutorials
├── dist/             # Generated static site (gitignored)
└── mkdocs.yml        # MkDocs configuration
```

### Content Organization

- **Markdown-first**: Most documents are written in Markdown
- **Images**: Documents with images should be organized in their own folders following MkDocs best practices:
  ```
  docs/
  └── category/
      └── document-name/
          ├── index.md
          └── images/
              ├── image1.png
              └── image2.png
  ```
- **Categories**: Currently organized into `general/` and `howto/`. These may be reorganized in the future as content grows.

## Development Commands

### Initial Setup

```bash
# Install uv if not already installed
curl -LsSf https://astral.sh/uv/install.sh | sh

# Create virtual environment and install dependencies
uv venv
uv pip install mkdocs-material

# Or using Fish shell
uv venv
uv pip install mkdocs-material
```

### Development Server

```bash
# Start MkDocs with live reload (auto-refreshes on file changes)
uv run mkdocs serve

# The site will be available at http://127.0.0.1:8000
```

### Build

```bash
# Build static site to dist/ directory
uv run mkdocs build --site-dir dist
```

### Linting

```bash
# Check markdown files
# (specific linting commands to be added as tooling is configured)
```

### Dependency Management

```bash
# Check for updates to MkDocs and dependencies
uv pip list --outdated

# Update dependencies
uv pip install --upgrade mkdocs-material
```

## Development Workflow

1. **Branch-based Development**: All changes must be created in a feature branch
2. **Pull Requests**: Changes must be approved and merged by repository owners
3. **GitHub CLI**: Use `gh` for creating PRs, issues, and other GitHub interactions
   ```bash
   # Create a new branch
   git checkout -b feature/new-documentation

   # Push and create PR
   git push -u origin feature/new-documentation
   gh pr create --title "Add new documentation" --body "Description of changes"
   ```

## MkDocs Configuration Notes

- **Site URL**: The site is rooted at `/docs` (https://whocaresradio.com/docs), ensure `site_url` in `mkdocs.yml` is configured accordingly
- **Theme**: Material theme provides features like search, navigation, and responsive design
- **Live Reload**: The development server automatically reloads when files change
