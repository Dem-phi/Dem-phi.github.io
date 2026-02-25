# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal website (Zhenghan Chen/陈政翰) built with Hugo, using the hugo-coder theme. The site is deployed to GitHub Pages at `https://Dem-phi.github.io/`. It supports multilingual content (English and Chinese).

## Common Commands

### Development
- **Start development server**: `hugo server -D`
  - Serves the site locally at `http://localhost:1313/`
  - `-D` flag includes draft content
  - Files are automatically reloaded on changes

- **Build for production**: `hugo --minify`
  - Generates optimized static HTML files in the `public/` directory

- **Create new content**: `hugo new <path>/<filename>.md`
  - Uses the archetype template from [archetypes/default.md](archetypes/default.md)
  - Creates file with TOML frontmatter including date, draft status, and title

### Deployment
The [readme.md](readme.md) contains the deployment workflow:
```bash
hugo --minify
cp -r public/* .
git add .
git commit -m "commit"
git push
```
Note: This copies built files from `public/` to the root, then commits and pushes.

## Architecture

### Theme Configuration
- Uses the hugo-coder theme as a Git submodule: [themes/hugo-coder](themes/hugo-coder/)
- Theme repository: https://github.com/luizdepra/hugo-coder
- Main configuration in [hugo.toml](hugo.toml)

### Multilingual Structure
The site is configured for bilingual content (English/Chinese) with these key settings:

- `defaultContentLanguage = "en"` - English is the default language
- `defaultContentLanguageInSubdir = false` - English content is served from the root path
- Chinese content uses language code prefix (e.g., `/about/` for English, handled by Hugo's i18n)

Language configuration in [hugo.toml](hugo.toml):
- `[languages.en]` - English language settings and menu
- `[languages.zh]` - Chinese language settings and menu

Each language has its own menu structure under `languages.<code>.menu.main`.

### Content Organization

Content files use TOML frontmatter (delimited by `+++`):
```toml
+++
title = "Page Title"
description = "Page description"
date = "YYYY-MM-DD"
aliases = ["alternative-url", "another-url"]
author = "Author Name"
+++
```

#### Key Directories
- `/` - Root contains main English pages (e.g., [about.md](about.md))
- `/static/` - Static assets served directly (images, files)
- `/static/images/` - Site images including profile photo
- `/static/files/` - Downloadable files
- `/content/` - Main content directory (currently minimal)
- `/archetypes/` - Content templates for `hugo new` command

#### Build Directories
- `/public/` - Generated static site (created by `hugo --minify`)
- `/cn/`, `/en/`, `/zh/` - Generated language-specific directories (build artifacts, do not edit)

### Taxonomies
Configured in [hugo.toml](hugo.toml#L30):
- `category = "categories"` - Content categorization
- `series = "series"` - Related content series
- `tag = "tags"` - Content tagging
- `author = "authors"` - Content authorship

### Menu Structure
Each language has its own menu configuration. Example for English:
1. Home (`/`)
2. About (`/about/`)
3. Projects (`/projects/`)

Chinese equivalents:
1. 主页 (`/`)
2. 关于我 (`/about/`)
3. 项目经历 (`/projects/`)

### Custom Assets
- `/css/` - Custom CSS overrides
- `/js/` - Custom JavaScript
- `/fonts/` - Custom font files
- `/data/` - Data files for templates

## Theme Customization

The hugo-coder theme is heavily customized. When modifying theme behavior:
1. Check [hugo.toml](hugo.toml) first for configuration options
2. Override templates in `/layouts/` if needed
3. Add custom CSS/JS in the respective directories
4. Theme documentation is available at https://github.com/luizdepra/hugo-coder/tree/main/docs
