# Jifeng's Blog

A personal bilingual blog (English & 中文) built with [Jekyll](https://jekyllrb.com/) using the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme.

🌐 **Live site:** https://gejifeng.github.io

## Features

- Responsive design with dark/light mode
- Bilingual posts (English & Chinese) with language filter on home page
- Categories, tags, and archives
- Full-text search
- PWA support (installable as an app)

## Local Development

### Prerequisites

- Ruby 3.1+
- Bundler (`gem install bundler`)

### Setup

```bash
# Clone the repo
git clone https://github.com/gejifeng/gejifeng.github.io.git
cd gejifeng.github.io

# Install dependencies
bundle install

# Serve locally
bundle exec jekyll serve
```

Open http://127.0.0.1:4000 in your browser.

## Writing Posts

Create a new file in `_posts/` with the format `YYYY-MM-DD-title.md`:

```yaml
---
title: "Your Post Title"
date: 2025-01-01 10:00:00 +0800
categories: [Category, Subcategory]
tags: [tag1, tag2]
lang: en          # 'en' for English, 'zh-CN' for Chinese
---

Post content here...
```

The `lang` field enables the language filter on the home page.

## Deployment

Push to the `main` branch — GitHub Actions will automatically build and deploy
to GitHub Pages.

## Bilingual Architecture

- Posts tagged `lang: en` → English posts
- Posts tagged `lang: zh-CN` → Chinese posts  
- Home page has a **Language / 语言** filter bar (preference saved in localStorage)
- Navigation UI stays in English (set via `lang: en` in `_config.yml`)

## License

MIT License — see [LICENSE](LICENSE) for details.
