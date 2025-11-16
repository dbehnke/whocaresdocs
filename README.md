# Whocares Amateur Radio Group Documentation

This repository contains the documentation for the Whocares Amateur Radio Group, built with MkDocs and the Material theme.

## Quick Start

### Prerequisites

- Python 3.8+
- [uv](https://github.com/astral-sh/uv) for dependency management

### Setup

```bash
# Create virtual environment and install dependencies
uv venv
uv pip install mkdocs-material
```

### Development

```bash
# Start the development server with live reload
uv run mkdocs serve
```

Visit http://127.0.0.1:8000 to preview the site.

### Build

```bash
# Build the static site
uv run mkdocs build --site-dir dist
```

## Project Structure

- `docs/` - Documentation source files (Markdown)
- `dist/` - Generated static site
- `mkdocs.yml` - MkDocs configuration

## Contributing

1. Create a feature branch
2. Make your changes
3. Submit a pull request for review

## License

Documentation content is maintained by the Whocares Amateur Radio Group.
