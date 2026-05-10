---
title: "Post Formatting Template"
description: "A reference template showing how to format SQL, Python, callouts, images, and tags in a blog post."
pubDatetime: 2025-05-10T00:00:00Z
tags: ["template", "reference"]
draft: true
---

> This post is a formatting reference for future posts. Keep `draft: true` — it won't appear on the live site.

## SQL Code Block

Use triple backticks with `sql` as the language identifier:

```sql
-- Find top 10 Tableau workbooks by query count (last 7 days)
SELECT
    wb.name                    AS workbook_name,
    vw.name                    AS view_name,
    COUNT(*)                   AS query_count,
    AVG(q.duration)            AS avg_duration_ms
FROM
    _views              vw
    JOIN _workbooks     wb  ON wb.id = vw.workbook_id
    JOIN _http_requests q   ON q.currentsheet = vw.name
WHERE
    q.created_at >= CURRENT_DATE - INTERVAL '7 days'
GROUP BY 1, 2
ORDER BY query_count DESC
LIMIT 10;
```

## Python Code Block

```python
import pandas as pd
import tableauserverclient as TSC

# Authenticate to Tableau Server
server = TSC.Server("https://your-tableau-server", use_server_version=True)
tableau_auth = TSC.PersonalAccessTokenAuth("token-name", "token-value", "site-id")

with server.auth.sign_in(tableau_auth):
    # List all workbooks
    all_workbooks, pagination = server.workbooks.get()
    for wb in all_workbooks:
        print(f"{wb.name} — last updated: {wb.updated_at}")
```

## Callouts / Blockquotes

Use `>` for callouts. Keep them short — one key insight per callout.

> **Tip:** In Tableau Server, always set a `vizql_session_timeout` appropriate to your workbook complexity. The default (30 min) is too long for production environments with shared resources.

> **Warning:** Row-level security implemented via user filters in the workbook (not the data source) does NOT enforce at the data layer. Anyone with a direct database connection can bypass it.

## Images

Place images in `public/images/` and reference them like this:

```markdown
![Alt text describing the image](/images/your-image.png)
```

Provide descriptive alt text — it matters for accessibility and SEO.

## Tags

Add relevant tags in the frontmatter. Keep them lowercase and hyphenated:

```yaml
tags: ["tableau", "sql", "aws", "data-modeling", "row-level-security"]
```

Use tags consistently across posts — they power the `/tags` index page.

## Frontmatter Reference

```yaml
---
title: "Your Post Title"
description: "One or two sentences. Shown in cards and SEO meta tags."
pubDatetime: 2025-05-10T00:00:00Z          # YYYY-MM-DD
tags: ["tableau", "sql"]
draft: false                  # true = won't appear on live site
featured: false               # true = appears in Featured section on homepage
---
```

## Publishing Checklist

- [ ] `draft: false`
- [ ] `pubDate` set to today's date
- [ ] Description is ≤ 160 characters
- [ ] At least one relevant tag
- [ ] Code blocks have language identifiers (`sql`, `python`, `bash`, etc.)
- [ ] Images have alt text
