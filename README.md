# Becoming Amu

AI-driven insights and automated knowledge curation.

**Blog**: [https://xulfereht.github.io](https://xulfereht.github.io)

---

## About

Personal blog powered by Jekyll and GitHub Pages, featuring automated content curation from AI research and knowledge synthesis.

## Tech Stack

- **Jekyll**: 4.3+ (Static site generator)
- **Theme**: [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 4.26+
- **Hosting**: GitHub Pages
- **Automation**: Claude Code + GitHub Actions

## Content Categories

- **Webclip**: Curated web articles with AI summaries
- **YouTube**: Video content analysis and learning notes
- **Research**: Deep research reports on AI/ML topics
- **Reading**: Book summaries and insights
- **Curation**: Daily AI news and trends

## Repository Structure

```
.
├── _posts/              # Published blog posts (auto-generated)
├── _archive/            # Legacy content (not published)
├── _config.yml          # Jekyll configuration
├── _includes/           # HTML components
├── _layouts/            # Page templates
├── _sass/               # Stylesheets
├── assets/              # Images, CSS, JS
└── README.md            # This file
```

## Automated Workflow

1. **Content Generation**: Claude Code processes URLs/topics
2. **Transformation**: Markdown with Jekyll frontmatter
3. **Deployment**: Auto-commit → GitHub Pages build → Live

## Local Development

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000
```

## Content Pipeline

Content is automatically published via `sync_to_blog.py`:

```bash
python scripts/sync_to_blog.py \
  --file source.md \
  --category webclip
```

**Required**: `BLOG_TOKEN` environment variable (GitHub Personal Access Token)

## Security

- Jekyll 4.3+ (latest stable)
- Auto-updates via Dependabot
- No client-side tracking
- HTTPS enforced

## License

- **Theme**: MIT License (Minimal Mistakes)
- **Content**: © 2025 Amu. All rights reserved.

---

**Last Updated**: 2025-11-11
**Status**: Active
**Build**: [![pages-build-deployment](https://github.com/xulfereht/xulfereht.github.io/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/xulfereht/xulfereht.github.io/actions/workflows/pages/pages-build-deployment)
