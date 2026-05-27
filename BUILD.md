# Blog

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

## Publish

Push to `main`. The GitHub Actions workflow builds the site and deploys `dist/`
to GitHub Pages.

In the GitHub repository settings, configure Pages with:

- Source: `GitHub Actions`
- Repository: `yy8402/yy8402.github.io`
- Public URL: `https://yy8402.github.io/`
