# Journal: how to write articles

An article is a folder `YYYY-MM-DD/slug/` with `article.md` (and optionally `article.<lang>.md` translations, e.g. `article.ru.md`) plus a `media/` subfolder for images.

## Front matter

```
---
author: "Name"
description: "Short description for previews and meta"
published_at: 2026-09-22 03:00:00
modified_at: 2026-09-22 03:00:00
tags: ["axia"]
frozen: true
---
```

- `frozen` controls whether the article also gets an in-app "frozen" page, and what its link is called:
  - `frozen: true` — in-app link uses the folder's slug (the folder name itself).
  - `frozen: "custom-slug"` — in-app link uses `"custom-slug"` instead of the folder name.
  - omitted / `frozen: false` — no in-app page, site only.
- Title, description (first paragraph) and cover image (first image) are picked up automatically from the text — no need to set them separately.

Everything the languages share can live in `article.yml` next to `article.md` instead, leaving each `.md` only what differs (usually just `description`):

```
# article.yml
author: "Name"
published_at: 2026-09-22 03:00:00
modified_at: 2026-09-22 03:00:00
tags: ["axia"]
frozen: "custom-slug"
```

The `.md` front matter wins over `article.yml` when a key is in both.

## Naming screens and buttons

In English, UI names go in plain text with their own capitalization — no quotation marks:

> rebuilt Settings and added filters to Activity
> choose I owe or Owe me

Quotes there read as a quotation or as irony. In Russian the usual «ёлочки» are correct: «Настройки», «Активность».

Keep one term per thing across the whole article and across languages — if a record is an activity, it is never a transaction three paragraphs later.

## Images

```
![Alt text](./media/screenshot.jpg)
```

The first image in the article becomes the cover. Paths are relative to `media/` inside the article folder.

For a dark-theme version put a second file named `<name>.dark.<ext>` next to it (e.g. `screenshot.jpg` and `screenshot.dark.jpg`) — it's picked up automatically, nothing to write in the article. Works for regular images, the cover and `gallery` / `tabs` blocks alike.

Dark versions are used in the in-app (frozen) page only — the site is always light and keeps the original image.

## Site-only / app-only

Wrap parts that should differ between the site and the frozen in-app mode:

```
:::site
Visible on the site only.
:::

:::app
Visible in the app only.
:::
```

Markdown works inside. The other variant never gets into the HTML, so search engines don't index hidden content.

## Gallery / switcher (before-after, screen variants)

A code block with language `gallery` or `tabs` renders a switcher between several images. Line format: `Title | file.jpg | caption` (caption optional). The first item is open by default, put a `*` in front of a title to open that one instead.

````
```gallery
Before | before.jpg | Axia 1.6
*After | after.jpg | Axia 1.7
```
````

````
```tabs
Cards | cards.jpg | Debt totals on the accounts screen
List | list.jpg | Balance per person
```
````

Both work the same (click to switch); only the nav style differs:
- `gallery` — "pill" style, good for more than a few options, or a plain image gallery;
- `tabs` — segmented control, good for 2-3 options (e.g. a before/after comparison).
