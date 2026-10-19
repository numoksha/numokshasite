---
title: "feat: Presse section with concert reviews"
type: feat
status: ready
date: 2026-10-19
repos:
  - numoksha/numokshasite
origin: "Chat brainstorming (opencodekit brainstorming skill); requested by Andre"
deepened: 2026-10-19
---

# feat: Presse section with concert reviews

## Summary

Create a "Presse" section on the NuMoksha static site (`numoksha/numokshasite`, GitHub Pages, no build) to show journalistic concert reviews to promoters and clubs. The section has a list page (`presse.html`) and one page per review. The first is Dr. Helmut Schönecker's review of the show at Jazzclub Biberach on 09.10.2026. The home page gains a quote slider, and the Galerie gains a new group with the 14 photos from the show.

## Problem Frame

The band wants to book more shows. Promoters and clubs judge a band by what others have written about it, but the site currently has no place for reviews. The first review exists only as a post on the Jazzclub Biberach Facebook page, which can disappear down the timeline or require a login. Bringing the full text, the photos, and the pull quotes onto the site itself makes that social proof visible and permanent.

## Requirements

- **R1.** The "Presse" item appears in the menu between "Galerie" and "Downloads" on all 7 pages (index, about, gallery, download, contact, presse, and the review page), on desktop and in the mobile menu.
- **R2.** On `presse.html` and on the review pages, the "Presse" item is marked as the current page (`current-menu-item`).
- **R3.** `presse.html` lists reviews from newest to oldest. Each card shows a photo, the show date, the venue, the title, the author, a 2–3 line excerpt, and a "Weiterlesen" button that opens the review page.
- **R4.** `presse-2026-10-09-jazzclub-biberach.html` shows the title "KONZERTKRITIK - NuMoksha: Hochenergetischer NuJazz aus der Nachbarstadt im Jazzkeller", the date and venue (09.10.2026, Jazzclub Biberach / Jazzkeller), the featured photo, the full text, the credit "Text und Fotos: Dr. Helmut Schönecker", a plain "Original auf Facebook" link (no embed), a grid with the 14 photos, and the "Zurück zur Presseübersicht" link.
- **R5.** The 14 photos on the review page open in the lightbox, with the credit "Fotos: Dr. Helmut Schönecker" immediately above the grid.
- **R6.** The new pages declare `lang="de"`.
- **R7.** The home page shows, below the upcoming-shows area, a slider that automatically rotates through 3 quotes, each signed "Dr. Helmut Schönecker, Jazzclub Biberach" and linking to the review page:
  1. „…zielt treffsicher in eine ‚ökologische Nische' des Nu-Jazz."
  2. „…wirkt zutiefst integer und wertschätzend."
  3. „…harmonisch und rund mit langem, nachhaltigem Abgang."
- **R8.** The Galerie has the new filter "09.10.2026 Jazzclub Biberach" (filter links on desktop and a `<select>` on mobile) that shows only the 14 photos from the show, which open in the lightbox, with credit to the photographer.
- **R9.** Published photos are at most ~1600 px on the longer side and are compressed (target: ≤ ~400 KB each), with thumbnails for grids and cards.
- **R10.** The plan (or a short README) documents the step-by-step process for adding a future review.

## Scope Boundaries

**In scope:** `presse.html`, the review page, the menu item on all 7 pages, the quote block on the home page, the resized photos in `images/galery/20261009/`, the new group in the Galerie, and minimal style adjustments (in `sass/` and `style.css` together).

**Out of scope:**
- "Copyright 2025" in the footer.
- The 9 Okt show that still appears as upcoming on the home page.
- The `dummy/` and `__MACOSX/` folders.
- The `lang="en"` of the existing pages.
- Embedding (embed/iframe) the Facebook post.
- Visual or template changes, and any build step.

**Later (follow-up):** clean up the items above in a separate task; a menu template/partial if the number of pages grows.

## Files NOT to modify

- `numoksha/numokshasite/blog.html` (template filler, not in the menu)
- `numoksha/numokshasite/CNAME`
- `numoksha/numokshasite/js/` (`app.js` already initializes `.quote-slider`, the lightbox, and Isotope; it should not need to change)
- `numoksha/numokshasite/images/galery/20260111/` and the other existing images
- `numoksha/numokshasite/downloads/`, `fonts/`, `dummy/`, `__MACOSX/`
- The existing content of `about.html`, `download.html`, and `contact.html` beyond the menu line

## Execution Context Lock

- Container: TODO (Andre's local folder that contains the checkout; set during implementation)
- Primary repo path: `<container>/numokshasite` (repo `numoksha/numokshasite`)
- Plan path: `numokshasite/.agents/plans/presse-section.plan.md` (the `.agents/plans/` folder will be created in this repo)
- Branch: `feat/presse-section` from `main` (the site has no `.agents/kit.toml`; `feat/` is the default prefix adopted)
- Forbidden execution roots: `/workspace/research/numokshasite` (read-only clone used for the research)
- Preflight before commit, push, or PR: `pwd; git rev-parse --show-toplevel; git branch --show-current; git status --porcelain`

## HyDE Outcome (Ideal Done State)

```text
HyDE Outcome (Ideal Done State)
- Goal: A "Presse" section that shows concert reviews to promoters and clubs; first review: Dr. Helmut Schönecker, Jazzclub Biberach, 09.10.2026.
- Required Deltas: presse.html (card list); presse-2026-10-09-jazzclub-biberach.html (featured photo, full text, credit, Facebook link, gallery of 14 photos); a "Presse" item in the menu on every page; a slider of 3 quotes on the home page; 14 resized photos in images/galery/20261009/ and a new filter in the Galerie.
- Optional Deltas: a written step-by-step for adding future reviews.
- Must Remain Unchanged: visual design/template, static hosting on GitHub Pages with no build, current content of the existing pages.
- Out of Scope: footer copyright, the old show on the home page, dummy/ and __MACOSX/, lang of the existing pages, embed of the Facebook post.
- Evidence of Success: `grep -c 'presse.html' *.html` = 1 menu line per page (7 pages); in the browser (desktop and mobile) "Presse" appears in the menu; a card opens the review; photos open in the lightbox; the "09.10.2026 Jazzclub Biberach" filter shows only the 14 photos; the home slider rotates and links through; `du -h images/galery/20261009/*` shows small files (≤ ~400 KB).
- Risks / Rollback Signals: a menu item missed on some page; style.css diverging from sass/. Rollback = revert the commit (static site).
```

## Context & Research

Research was done on the read-only clone `/workspace/research/numokshasite` (branch `main`). There is no `.agents/learnings` in the site repo; the opencodekit ledger has nothing about static sites.

- **Menu copied by hand:** `numokshasite/index.html:27`, `about.html:28`, `gallery.html:29`, `download.html:37`, and `contact.html:37` have `<li class="menu-item current-menu-item">` on that page's own entry. The mobile menu is cloned in `numokshasite/js/app.js:125` (`$(".mobile-menu").append($(".main-navigation .menu").clone())`), so only the desktop menu needs to be edited.
- **Gallery:** `numokshasite/gallery.html:44-55` has the `<select class="mobile-filter">` (options `*`, `.band`, `.11012026`) and the `.filterable-nav a[data-filter]` links. Items in `gallery.html:64-100`: `<div class="filterable-item 11012026"><a href="images/galery/20260111/20260111_1.jpg"><figure><img …></figure></a></div>`. Today the same image serves as both the thumbnail and the large image. Isotope is in `app.js:54-90`, and the lightbox is in `app.js:119` (`selector: '.filterable-item a'`).
- **Image folder:** `numokshasite/images/galery/YYYYMMDD/YYYYMMDD_N.jpg` (the folder name is misspelled; keep it). The current photos are ~3 MB and have not been resized.
- **Home:** the `.fullwidth-block.upcoming-event-section` block starts at `numokshasite/index.html:52`; `</main>` is at `index.html:93`. The new slider goes between the two.
- **Quote slider:** `numokshasite/js/app.js:27` already initializes `$(".quote-slider").flexslider(...)`. The markup the template expects is `.quote-slider > ul.slides > li > blockquote > p + cite` (check the styles in `sass/`).
- **Reusable pieces:** `.post` / `.entry-date` from `numokshasite/blog.html` for the cards; `.content` + `.featured-image` from `numokshasite/about.html` for the review page.
- **CSS:** `numokshasite/style.css` (+ `style.css.map`) is compiled by hand from `numokshasite/sass/`.
- **Source photos:** `/workspace/presse/fotos/01.jpg`–`14.jpg` (2048×1365; `05.jpg` is 2048×2048). Featured photo (decided): **`02.jpg`** → `20261009_2.jpg` (the whole band on stage, with the audience in the foreground).
- **Review text:** provided by Andre in chat; it is not in this plan. Copy it literally during implementation, without rewriting.
- **Show facts:** Jazzclub Biberach (Jazzkeller), 09.10.2026, 20:30. Lineup: Michael Dümmler (Sopran-/Baritonsaxofon), Ralle Fricker (Schlagzeug), André Lima (Bass), Hugo Nägele (Gitarren).

## Key Technical Decisions

- **KD1 — List + one page per review.** Each review has its own URL that can be sent to a promoter, and the list stays short. This was chosen over a single page containing every full text.
- **KD2 — Copied static HTML, no build and no new JS.** This follows the site's pattern (the menu is copied by hand on each page). A checklist (U1) makes sure the item is added on all 7 pages.
- **KD3 — A plain link to Facebook, no embed.** An embed only works with a public post, asks for cookie consent, and loads a third-party script. The link keeps the reference to the original.
- **KD4 — Reuse `.quote-slider`, already initialized in `app.js`.** No new JS is needed; to grow the slider, add an `<li>`.
- **KD5 — Resized photos (~1600 px, JPEG ~q80) + thumbnails.** Approved: `20261009_N.jpg` (large) and `20261009_N_thumb.jpg` (~600 px) in the same folder; the `<a href>` points to the large file and the `<img>` points to the thumbnail. The existing photos do not change.
- **KD6 — Filter class `.09102026` / folder `20261009`.** The class name follows the existing `.11012026` pattern (DDMMYYYY), and the folder follows the YYYYMMDD pattern. The label is "09.10.2026 Jazzclub Biberach".
- **KD7 — `lang="de"` only on the new pages.** Fixing the existing pages is out of scope.
- **KD8 — Styles: change `sass/` and `style.css` in the same commit**, and only if the existing classes are not enough.

## Implementation Units

- [ ] **U1 — "Presse" menu item**
  - Goal — add `<li class="menu-item"><a href="presse.html">Presse</a></li>` between Galerie and Downloads.
  - Requirements — R1
  - Dependencies — none
  - Files — modify `numokshasite/index.html`, `about.html`, `gallery.html`, `download.html`, `contact.html`
  - Test scenarios — happy: the item appears on each page on desktop and in the mobile menu; edge: the order is correct and `current-menu-item` remains only on the current page; error: `grep -L 'presse.html' index.html about.html gallery.html download.html contact.html` lists no files.

- [ ] **U2 — Resized photos**
  - Goal — generate 14 large photos and 14 thumbnails from `/workspace/presse/fotos/01–14.jpg`.
  - Requirements — R9
  - Dependencies — none
  - Files — create `numokshasite/images/galery/20261009/20261009_{1..14}.jpg` and `_thumb.jpg`
  - Test scenarios — happy: the longer side is ≤ 1600 px and the files are ≤ ~400 KB; edge: `05` (square) is not distorted; error: EXIF orientation is preserved.

- [ ] **U3 — Review page**
  - Goal — create `presse-2026-10-09-jazzclub-biberach.html` (header/footer copied, `lang="de"`, Presse marked as current).
  - Requirements — R2, R4, R5, R6
  - Dependencies — U1, U2
  - Files — create `numokshasite/presse-2026-10-09-jazzclub-biberach.html`
  - Test scenarios — happy: title, date, featured photo `20261009_2.jpg`, full text, credits, a link to Facebook (opens in a new tab, with `rel="noopener"`), and "Zurück zur Presseübersicht"; edge: the grid looks good on a phone; error: every photo opens in the lightbox, with no 404.

- [ ] **U4 — List page `presse.html`**
  - Goal — a card list, from newest to oldest.
  - Requirements — R2, R3, R6
  - Dependencies — U3
  - Files — create `numokshasite/presse.html`; modify `sass/` + `style.css` only if needed
  - Test scenarios — happy: the card shows the photo, date, venue, title, author, excerpt, and "Weiterlesen", and the button opens the review; edge: the excerpt stays at 2–3 lines on a phone.

- [ ] **U5 — Quote slider on the home page**
  - Goal — a `.quote-slider` block with the 3 quotes below `.upcoming-event-section`.
  - Requirements — R7
  - Dependencies — U3
  - Files — modify `numokshasite/index.html`
  - Test scenarios — happy: the slider rotates on its own and each quote opens the review; edge: the German quotation marks („ " ‚ ') render correctly (UTF-8); error: the concert carousel still works.

- [ ] **U6 — New group in the Galerie**
  - Goal — the "09.10.2026 Jazzclub Biberach" filter (`.09102026`) on desktop and in the `<select>`, with the 14 items and the credit.
  - Requirements — R8
  - Dependencies — U2
  - Files — modify `numokshasite/gallery.html`
  - Test scenarios — happy: the filter shows only the 14 photos and they open in the lightbox; edge: "Alle" shows everything and the initial ".band" filter does not change; error: the class selector that starts with a digit works in Isotope/jQuery (`.11012026` already works, but verify).

- [ ] **U7 — Step-by-step for future reviews + final verification**
  - Goal — record the procedure below and run the HyDE evidence.
  - Requirements — R10, all
  - Dependencies — U1–U6
  - Files — this plan

### How to add a future review

1. Resize the photos into `images/galery/YYYYMMDD/` (large + `_thumb`).
2. Copy a review page to `presse-YYYY-MM-DD-<venue>.html` and replace the title, date, venue, text, credits, link to the original, and gallery.
3. Add the new card at the top of `presse.html`.
4. Optional: add an `<li>` with a new sentence to the `.quote-slider` in `index.html`, and a new filter in `gallery.html`.
5. Check that the new page has the complete menu with "Presse" marked as current.

## Risks & Dependencies

| Risk | Mitigation |
|---|---|
| Menu item missed on some page | Checklist in U1 + `grep -L` in the evidence |
| `style.css` diverging from `sass/` | Change both in the same commit (KD8) |
| Heavy photos making the site slow | U2 with a size limit checked with `du` |

## Open Questions

**Resolved during planning:** structure (list + one page per review), menu placement, home-page sentences, photo treatment, a plain link instead of an embed, a single plan.

**Resolved with Andre (2026-10-19):**
- Featured photo: `02.jpg` → `20261009_2.jpg`.
- Thumbnails: `_thumb.jpg` in the same folder (approved).
- Permission to republish the text and the photos: confirmed by Andre. Credit to Dr. Schönecker remains required.
- The plan lives in the site repo, at `.agents/plans/presse-section.plan.md`, on the `feat/presse-section` branch.

**For implementation:** nothing pending. Only the container's local path, which is set at the start.

## Sources & References

- Original post: https://www.facebook.com/JazzclubBiberach/posts/pfbid02BERraRquetLA62vMcg3383c4XzFB9v74Y2RBf8SLvQ8DDVyQj8AzA9eFgbjGZvAyl
- Skill: `andrealveslima/opencodekit/.agents/skills/create-prd/SKILL.md`; format: `andrealveslima/opencodekit/.cursor/rules/prd-format.mdc`
