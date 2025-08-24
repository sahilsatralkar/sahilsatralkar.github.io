# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is Sahil Satralkar's personal website and portfolio built with Jekyll and hosted on GitHub Pages at sahilsatralkar.com. The site showcases iOS development work including published apps, blog posts, and professional experience.

## Common Development Commands

### Local Development
```bash
# Install dependencies (run once or when Gemfile changes)
bundle install

# Run development server with live reload
bundle exec jekyll serve

# Build site without serving
bundle exec jekyll build

# Clean generated files
bundle exec jekyll clean
```

### Testing Changes
```bash
# Build with production settings
JEKYLL_ENV=production bundle exec jekyll build

# Check for broken links and HTML issues
bundle exec htmlproofer ./_site --disable-external
```

## Architecture & Structure

### Content Management
The site uses Jekyll's content management system with the following key areas:

**Blog Posts** (`_posts/`): 
- Follow naming convention: `YYYY-MM-DD-title-with-hyphens.md`
- Include front matter with: layout, title, date, categories, tags, header
- Use `layout: single` for standard blog posts
- Images go in `/assets/images/` with optimized sizes

**Static Pages** (`_pages/`):
- `portfolio.md`: Showcases iOS apps with detailed descriptions
- `about.md`: Professional background and experience  
- `contact.md`: Contact information
- Use permalinks in front matter for custom URLs

**Navigation** (`_data/navigation.yml`):
- Main menu structure with title and url pairs
- Maintains site-wide navigation consistency

### Theme Customization
The site uses Minimal Mistakes theme with customizations:

**Configuration** (`_config.yml`):
- Site metadata, author info, social profiles
- Theme settings including skin, locale, search provider
- Build settings for Jekyll and plugins

**Styling** (`_sass/minimal-mistakes/`):
- Theme overrides go in component-specific SCSS files
- Custom styles can be added to `_sass/minimal-mistakes/_custom.scss`
- Color schemes defined in `skins/` directory

### Asset Management
**Images** (`assets/images/`):
- App screenshots and icons for portfolio
- Blog post headers and content images
- Keep originals in `assets/images_original/` for reference
- Optimize images before adding (reduce file size while maintaining quality)

## Adding New Content

### New iOS App to Portfolio
1. Add app section to `_pages/portfolio.md` following existing structure
2. Include: app name, description, key features, technical stack, links
3. Add app icon and screenshots to `assets/images/`
4. Optional: Create accompanying blog post in `_posts/`

### New Blog Post
1. Create file in `_posts/` with proper naming convention
2. Include required front matter (layout, title, date, categories, tags)
3. Add header image to `assets/images/` and reference in front matter
4. Use markdown for content with proper heading hierarchy

## Deployment
The site automatically deploys to GitHub Pages when changes are pushed to the master branch. No manual deployment steps required.

## Important Considerations
- Images should be optimized for web (compressed, appropriate dimensions)
- Blog post dates affect visibility - future dates won't appear until that date
- Changes to `_config.yml` require server restart during local development
- Use absolute paths for images when referencing from blog posts
- Maintain consistent naming conventions for files and URLs