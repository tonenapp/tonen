---
name: share
description: Share the current prototype with Tonen, so anyone who opens it can leave pinned comments and see who's there. Inserts the Tonen script tag first in the HTML <head> and returns the link to share. Use when the user says "/tonen:share", "share this prototype", "add Tonen" or "get feedback on this with Tonen".
argument-hint: "[project id to reuse]"
---

# Share with Tonen

Tonen wraps the running prototype in a black frame with pinned comments and live visitors. It switches on with one script tag, first in the page's `<head>`:

```html
<script src="https://tonen-mvp.web.app/tonen.js" data-project="PROJECT_ID" data-branch="BRANCH"></script>
```

The user never edits this tag; you do. Steps:

1. **Find the head.** Locate every file that renders the document `<head>` for the app's pages. Skip `node_modules` and build output (`dist/`, `build/`, `.next/`, `out/`).
   - Static site, Vite, Parcel: `index.html` and any other `*.html` pages.
   - Next.js App Router: root `app/layout.tsx|jsx` (add `<head>` inside `<html>` if missing). Pages Router: `pages/_document.tsx|jsx`, inside `<Head>`.
   - Create React App: `public/index.html`. Astro, SvelteKit, Remix, Nuxt: the root layout, `src/app.html`, `app/root.tsx` or `app.vue`/`nuxt.config` head.
   If it's unclear which file is the real template, ask once.
2. **Project id.** Comments are tied to it. Use, in this order: an id the user passed (`/tonen:share k7f2q9xm3a`), the `data-project` of a Tonen tag already in the repo, or a new one: 10 random lowercase letters and digits, e.g. `node -e "console.log(require('crypto').randomBytes(16).toString('base64url').toLowerCase().replace(/[^a-z0-9]/g,'').slice(0,10))"`. One id per repo, the same on every page.
3. **Branch.** `repo/branch`, so people see which repository it is: the repo name from `git remote get-url origin` (last part, without `.git`; the git root folder name if there's no remote), then `git branch --show-current`. Example: `tonen-mvp/main`. Leave `data-branch` out when not in git.
4. **Insert or update.** The tag must be the first script in `<head>`: right after `<meta charset>` if there is one, otherwise the first child of `<head>`. It must be a plain blocking `<script src>`: never `async`, `defer`, `type="module"`, or Next's `<Script>` component. In JSX write it exactly as `<script src="…" data-project="…" data-branch="…"></script>`. If the tag is already there, only update `data-branch` and move it to the top if needed.
5. **Report.** Show the diff. Don't commit unless asked. Then give the link to share:
   - A dev server that's running or configured: its local URL. Tonen works on localhost too, but only people on this computer can open it.
   - A published URL you can find (GitHub Pages via `gh api repos/{owner}/{repo}/pages`, `homepage` in package.json, Vercel or Netlify config): that URL, once this change is pushed and deployed.
   - Otherwise: "Publish this branch anywhere (GitHub Pages, Netlify, Vercel, staging) and share that URL. Everyone who opens it sees the same comments."
   End with one line: run `/tonen:remove` before this ships to real users.
