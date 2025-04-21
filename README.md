# SCRC_Docs

This repository contains the official documentation for the NYU Stern Center for Research Computing (SCRC).

## 📚 Documentation Structure
- Organized by topic (Getting Started, Computing Resources, Storage, Datasets, Software, Linux Tutorials, Cloud Computing)
- Each section is in its own folder with Markdown files
- Main navigation is defined in `mkdocs.yml`

## 🚀 Building the Static Website
This documentation uses [MkDocs](https://www.mkdocs.org/) with the [Material theme](https://squidfunk.github.io/mkdocs-material/) for a beautiful, searchable static site.

### 1. Install dependencies
```sh
pip install -r requirements.txt
```

### 2. Serve locally for preview
```sh
mkdocs serve
```
Visit the local server URL shown in your terminal (usually http://127.0.0.1:8000).

### 3. Build static site
```sh
mkdocs build
```
The static site will be generated in the `site/` directory.

### 4. Deploy
You can deploy the `site/` directory to GitHub Pages or any static hosting provider.

---
For questions or contributions, please open an issue or pull request.