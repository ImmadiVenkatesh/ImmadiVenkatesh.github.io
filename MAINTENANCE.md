# Site Maintenance Guide

## Local Development

```bash
cd site
npm run dev        # start dev server at http://localhost:4321
npm run build      # production build (runs type check + build + pagefind)
npm run preview    # preview the production build locally
```

---

## Updating Dependencies

Run this quarterly or when you see a security notice:

```bash
npm update                    # update within current semver ranges
npm outdated                  # see what has newer versions available
npx npm-check-updates -u      # upgrade everything to latest (caution: may break)
npm install
npm run build                 # verify build still passes before pushing
```

For the Astro framework specifically, check the [Astro changelog](https://github.com/withastro/astro/blob/main/packages/astro/CHANGELOG.md) before major version bumps — they sometimes require config changes.

---

## Changing Colors / Theme

AstroPaper uses CSS custom properties. Open `src/styles/global.css` (or the equivalent Tailwind config):

1. Colors are defined as HSL values on `:root` (light mode) and `.dark` (dark mode)
2. The primary accent color is `--color-accent`
3. Change values, run `npm run dev`, and verify in both light and dark mode before pushing

For a full color scheme swap, see the AstroPaper docs on predefined color schemes.

---

## Adding a New Page

1. Create `src/pages/your-page.astro` (or `.md` for Markdown pages)
2. Use an existing layout: `import Layout from "@/layouts/Layout.astro"` or `AboutLayout.astro`
3. Add a link to it in `src/components/Header.astro` if it should appear in the nav
4. Add/commit/push

Example minimal page:
```astro
---
import Layout from "@/layouts/Layout.astro";
import Header from "@/components/Header.astro";
import Footer from "@/components/Footer.astro";
---
<Layout title="My New Page">
  <Header />
  <main class="app-layout">
    <h1>My New Page</h1>
    <p>Content here.</p>
  </main>
  <Footer />
</Layout>
```

---

## Updating the Homepage Content

The homepage is `src/pages/index.astro`. All portfolio data (experience cards, skills) is defined at the top of that file as plain TypeScript arrays — no CMS or external files. Edit the arrays directly and push.

---

## Rolling Back a Bad Deploy

GitHub Pages deploys are git-based. To roll back:

```bash
# Option 1: Revert the last commit
git revert HEAD
git push

# Option 2: Reset to a known good commit (replace HASH with the commit hash)
git log --oneline     # find the good commit hash
git revert HEAD..HASH # revert each commit since then
git push
```

**Do not use `git push --force` on main** — it breaks the deploy history.

To find the deploy that caused the issue, go to **GitHub → Actions** and look at the failed or unwanted run.

---

## Adding a Resume PDF

Replace `public/resume.pdf` with your updated file:

```bash
# Copy your new PDF into the public folder
cp /path/to/new-resume.pdf public/resume.pdf
git add public/resume.pdf
git commit -m "chore: update resume PDF"
git push
```

---

## Monitoring the Live Site

After any push, go to **GitHub → Actions** to watch the deploy. The workflow takes ~90 seconds. If it fails, click the failed run to see the error log.

The live site is at: **https://ImmadiVenkatesh.github.io**
