# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site for Curious Builds, a software/hardware/R&D company building. The site uses the hugo-coder theme (included as a git submodule in `themes/hugo-coder/`).

## Common Commands

### Build and Development
- `hugo server` - Start development server with live reload (typically runs on http://localhost:1313)
- `hugo server -D` - Start server and include draft content
- `hugo` - Build the static site to `public/` directory
- `hugo new content/blog/<name>.md` - Create a new blog post

### Theme Management
The hugo-coder theme is managed as a git submodule:
- `git submodule update --init --recursive` - Initialize/update the theme submodule
- Theme customization is done through:
  - `layouts/` - Override theme templates (e.g., `layouts/_partials/home.html`)
  - `assets/css/custom.scss` - Custom styles referenced in `hugo.toml`

## Site Architecture

### Configuration
- `hugo.toml` - Main site configuration
  - Theme: hugo-coder
  - Main content sections: `blog` (defined in `mainSections`)
  - Custom SCSS: `assets/css/custom.scss`
  - Syntax highlighting: github-dark style
  - Security allows asciidoctor executable for AsciiDoc content

### Content Structure
- `content/_index.md` - Home page content (rendered by `layouts/_partials/home.html`)
- `content/blog/` - Blog posts
- Content can be written in Markdown or AsciiDoc (`.adoc` files)

### Customization
- **Fonts**: Custom Lora variable fonts in `static/fonts/` loaded via `assets/css/custom.scss`
- **Styles**: Global typography and spacing overrides in `assets/css/custom.scss`
- **Layout overrides**: Theme templates can be overridden by placing files in `layouts/` with the same path as in the theme

### Image Handling
- Place images directly in `content/` alongside markdown files
- Use Hugo shortcodes for images: `{{< figure src="image.jpg" alt="Description" class="image-float-right" >}}`
- The `image-float-right` class is defined in custom.scss with responsive behavior

## Key Technical Details

- Hugo version: v0.152.2+extended
- The site uses Hugo's asset pipeline for SCSS compilation
- Theme documentation available in `themes/hugo-coder/docs/`
- Generated site output goes to `public/` (ignored by git)
