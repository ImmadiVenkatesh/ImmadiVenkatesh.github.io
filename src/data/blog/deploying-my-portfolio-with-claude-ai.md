---
title: "How I Deployed My Portfolio Site in One Session Using Claude"
description: "I used Claude Code to go from zero to a live GitHub Pages portfolio in a single sitting — here's exactly what happened, what broke, and what surprised me."
pubDatetime: 2026-05-10T08:00:00Z
tags: ["ai-tools", "claude", "github-pages", "astro", "career"]
draft: false
featured: true
---

I've been meaning to build a personal site for years. Ten years of BI work across GE Healthcare, Citi Bank, State Street, Dell, and Capgemini — and nothing to show for it publicly except a LinkedIn profile. Last weekend I finally did it, and I did it entirely by talking to an AI.

Here's what actually happened.

## The Setup

I used **Claude Code** — Anthropic's CLI tool that lets Claude operate directly on your local file system, run commands, read files, and push to GitHub. It's a different experience from a chat interface. You give it a goal, it works through the steps, and you review what it's doing at each stage.

My goal: a live portfolio site at `ImmadiVenkatesh.github.io` with a homepage showcasing my BI experience, an About page, and a blog I can actually maintain.

I dropped both versions of my resume (DOCX files) into a working directory and gave Claude the full brief — tech stack (Astro + AstroPaper theme), content requirements, what I wanted the homepage to show, and explicit rules about what it was and wasn't allowed to do without asking me first.

## What Worked Well

**Resume extraction was instant.** Claude read both my DOCX files, compared them, picked the more polished one, and produced a clean structured summary — experience entries, skills grouped by category, achievements, certifications. I could verify everything was accurate before it touched any code.

**The security check.** Before running a single `npm` command, I asked Claude to scan the cloned AstroPaper template for malicious code. It ran a proper audit — checked `package.json` lifecycle hooks for postinstall scripts that could execute arbitrary code, grepped for `eval()` and obfuscated patterns, listed all external network calls, checked every dependency for typosquatting. Everything came back clean. This is the kind of thing most developers skip, and honestly I would have skipped it too if I was setting this up manually.

**The homepage structure.** The brief asked for: Hero section, Experience cards, Skills grid, Recent Posts, social icons. Claude built all of it in one Astro file with real data from my resume — actual achievements, actual team sizes, actual tools. No invented content.

**Handling `gh` CLI path issues.** The GitHub CLI wasn't in Claude's PATH even after I installed it and restarted my terminal. Instead of giving up or asking me to debug it, Claude found `gh.exe` at `C:\Program Files\GitHub CLI\gh.exe` and called it by full path for the rest of the session. Small thing but it would have blocked me for a while if I was doing this manually.

## What Broke (And How It Got Fixed)

**Frontmatter schema mismatch.** AstroPaper uses `pubDatetime` — Claude initially wrote `pubDate` in the blog post frontmatter. The build failed on CI with a clear schema error. Fixed in one edit, pushed, redeployed.

**Missing import.** I asked Claude to clean up unused imports in `constants.ts`. It removed `IconBrandX` from the import list, not noticing that the `SHARE_LINKS` array (post share buttons) still referenced it. The TypeScript check caught it on the first CI run. One-line fix, clean deploy on the next push.

Both failures were caught by the build step in GitHub Actions — not in production. That's exactly how it should work.

## The Actual Deploy Flow

1. Claude cloned the AstroPaper template and removed its git history
2. Customized `config.ts`, `constants.ts`, `index.astro`, and `about.md` with my real content
3. Cleared out all demo blog posts, added my seed posts
4. Ran `npm run build` locally — passed clean
5. Initialized a git repo, made an initial commit (114 files)
6. Used `gh repo create` to create `ImmadiVenkatesh.github.io` on GitHub and push
7. Configured GitHub Pages to deploy from GitHub Actions via the API
8. Triggered the first deploy and watched it live — build: 31 seconds, deploy: 8 seconds

Total time from "let's build this" to live URL: one session.

## What I'd Call Out for Other BI Professionals

The thing that struck me most wasn't the speed — it was the **review loop**. Claude didn't just do things silently. At each phase it showed me what it extracted, asked what contact info should be public, confirmed the GitHub username before creating anything, paused before pushing to a public repo. That structure made it feel safe to let it operate autonomously for the technical parts while I stayed in control of the decisions that matter.

For someone like me who knows data and SQL deeply but doesn't live in frontend tooling day-to-day, this is genuinely useful. I didn't need to learn Astro's content collection schema, or figure out GitHub Actions workflow syntax, or debug why `gh` wasn't in PATH. I just needed to know what I wanted.

The session also produced `POSTING.md` — a plain-language guide for future me explaining exactly how to add a new blog post with three commands. That's the kind of thing you write for yourself and then lose. Having it in the repo means I'll actually use it.

## What's Next

The site is live at [ImmadiVenkatesh.github.io](https://ImmadiVenkatesh.github.io). The next posts I want to write are about things I'm actively exploring: Tableau MCP, Power BI Copilot in a real enterprise setting, and what 10 years of regulated-industry BI teaches you about data trust.

If you're a BI professional who's been putting off building a public presence — the barrier is lower than it looks.
