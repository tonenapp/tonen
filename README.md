# Tonen for Claude Code

Share a running prototype so anyone with the link can leave pinned comments and see who's there, like Figma comments on a real product.

## Install (once)

In Claude Code:

```
/plugin marketplace add tonenapp/tonen
/plugin install tonen@tonen
```

## Use

In your prototype's project:

- `/tonen:share` adds Tonen and gives you the link to share.
- `/tonen:remove` takes it out again, for example before you ship. Comments stay saved; `/tonen:share <id>` brings them back.

Works with plain HTML, Vite, Next.js, Create React App, Astro and similar. Tonen runs on localhost too, and on any host: GitHub Pages, Netlify, Vercel, staging.
