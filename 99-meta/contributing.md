---
id: contributing
title: How to write and update pages
type: rules
status: verified
---

# How to write and update pages

1. Copy the `_TEMPLATE-*` file from the right folder.
2. Fill in every frontmatter field. `id` must be unique; `search_knowledge` uses it as the doc ID.
3. Use real, tested examples. Copy exact tool responses, including punctuation.
4. Set `status`:
   - `todo`: page exists but content is missing.
   - `draft`: partly known or not fully tested.
   - `verified`: every example was run in the sandbox on `last_verified`.
5. One topic per page; link related pages by path.
6. When an agent finds new behavior, it opens a pull request that adds a `KI-` entry
   and updates the tool page. A person reviews and merges.
