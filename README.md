# Add a Post

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
