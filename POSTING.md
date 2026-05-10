# How to Publish a New Blog Post

## The Short Version (3 commands)

```bash
git add src/data/blog/your-post-filename.md
git commit -m "post: add 'Your Post Title'"
git push
```

GitHub Actions will build and deploy automatically within ~2 minutes.

---

## Step-by-Step

### 1. Create the file

Add a new `.md` file inside `src/data/blog/`. The filename becomes the URL slug:

- `src/data/blog/tableau-rls-deep-dive.md` → `yourdomain.github.io/posts/tableau-rls-deep-dive/`

### 2. Add the frontmatter

Every post must start with this block (copy and fill in):

```yaml
---
title: "Your Post Title Here"
description: "One or two sentences. Shown in post cards and SEO meta. Keep under 160 characters."
pubDatetime: 2025-05-15T00:00:00Z
tags: ["tableau", "sql", "aws"]
draft: false
featured: false
---

Your post content starts here...
```

**Frontmatter fields:**

| Field | Required | Notes |
|-------|----------|-------|
| `title` | Yes | Shown as the page heading |
| `description` | Yes | Used in cards and Google preview |
| `pubDatetime` | Yes | Format: `YYYY-MM-DDT00:00:00Z` |
| `tags` | No | Lowercase, hyphenated. Powers the `/tags` page |
| `draft` | No | `true` = hidden from live site. Default: `false` |
| `featured` | No | `true` = appears in Featured section on homepage |

### 3. Write the post

After the frontmatter, write in standard Markdown. See `src/data/blog/post-formatting-template.md` for code block, callout, and image examples.

### 4. Publish

```bash
git add src/data/blog/your-post-filename.md
git commit -m "post: add 'Your Post Title'"
git push
```

That's it. Watch the **Actions** tab on GitHub — the build takes about 90 seconds.

---

## Tips

- **Start as draft:** Set `draft: true` while writing, flip to `false` when ready.
- **Add images:** Place them in `public/images/` and reference as `/images/your-image.png`.
- **Update a post:** Edit the file, optionally add `modDatetime`, then add/commit/push.
- **Preview locally:** Run `npm run dev` and open `http://localhost:4321`.
