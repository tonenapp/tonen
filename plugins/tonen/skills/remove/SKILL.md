---
name: remove
description: Remove Tonen from the current prototype (the comment layer), for example before shipping to production. Use when the user says "/tonen:remove", "remove Tonen" or "take the comments layer out".
---

# Remove Tonen

1. Find every Tonen tag: a `<script>` whose `src` ends in `/tonen.js` and that has `data-project`. Look in HTML files and in layouts or documents that render `<head>` (skip `node_modules` and build output).
2. Delete each one and keep the surrounding markup tidy.
3. Show the diff. Don't commit unless asked.
4. Say the comments are still saved, and give the command to bring them back: `/tonen:share <old data-project id>`.
