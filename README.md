# Yuyang Yang Blog

Markdown-first static blog built with Astro and deployed to GitHub Pages.

## Local Development

```bash
npm install
npm run dev
```

Open `http://127.0.0.1:4321/`.

## Docker

Build and run the production site without installing npm dependencies on the host:

```bash
docker build -t yy8402-blog .
docker run --rm -p 8080:80 yy8402-blog
```

Open `http://127.0.0.1:8080/`.

With Docker Compose:

```bash
docker compose up --build
```

Docker Compose serves the site at `http://127.0.0.1:8081/`.

## Add a Post

Create a new markdown file in `src/content/blog/`.

```markdown
---
title: "Post Title"
description: "One sentence summary for the homepage, RSS, and metadata."
subtitle: "Optional subtitle shown under the post title."
publishDate: 2026-05-27
tags:
  - AI
  - Architecture
heroImage: "/images/editorial-workspace.png"
draft: false
---

Write the post here.
```

The URL is generated from the filename. For example:

`src/content/blog/agentic-ai-workspace.md` becomes `/blog/agentic-ai-workspace/`.

## Publish

Push to `main`. The GitHub Actions workflow builds the site and deploys `dist/`
to GitHub Pages.

In the GitHub repository settings, configure Pages with:

- Source: `GitHub Actions`
- Repository: `yy8402/yy8402.github.io`
- Public URL: `https://yy8402.github.io/`
