# Maintenance Handover

This document is for the maintainers of this repository. If you've just been added as an admin, read it in full before making any changes.

## Current maintainers

- Mike Hay
- Imad Dollie

*(GitHub handles to be added once admin access is granted.)*

## What this repo is for

A single source of truth for Black Cygnet Life brand assets — logos, colours, fonts, templates, guidelines. Every app, email, marketing site, or document that uses the BCL brand should pull its assets from here via jsDelivr URLs.

The consequence: if you change something here, it can change everywhere, instantly. That is the power and the risk of this setup. Read the versioning section of the [README](./README.md) and the "major changes" section below before making any change you'd call significant.

## Parent-brand assets in this repo

The [`parent-brand/`](./parent-brand/) folder contains the **Black Cygnet Group** (parent company) swan mark in 6 colour treatments. These are included here for convenience — BCL collateral often needs to reference the parent brand — but they are **not BCL brand assets**. When a dedicated Black Cygnet Group brand repo is eventually created, these assets will move there and this folder will be deprecated. For now, keep their filenames prefixed with `bcg-` so they can never be confused with BCL's own marks.

## What you'll actually do, realistically

Most months: nothing. Brand assets don't change often.

When they do change, one of these three things is happening:

1. **Fixing a small issue** (e.g. replacing an SVG with a cleaner export).
   → Commit directly to `main`. Bump the patch version. Done.

2. **Adding a new asset** (e.g. a new illustration, a new social template).
   → Commit directly to `main` or via a PR if you want review. Bump the minor version.

3. **Changing something that could break downstream apps** (e.g. a new logo design, a primary colour change, removing an old variant).
   → This is a major version. Read the "major changes" section below before doing anything.

## This repo is public — what you can and can't commit

Everything in this repo is visible to the entire internet. That's intentional — it's how jsDelivr serves assets to our apps. But it means you need to be careful about what you add.

**Never commit:**

- **Licensed fonts** (`.ttf`, `.otf`, `.woff`, `.woff2`). Almost all commercial font licences forbid redistribution, and a public repo counts as redistribution. If someone sends you a font file to add, don't — link to the vendor in `typography/fonts.md` instead.
- **Paid stock photos** (Shutterstock, Getty, Unsplash+). Only commit photos we own outright.
- **Unannounced brand work.** If a new logo or campaign hasn't been publicly launched yet, don't commit it until launch day. Committing to a public repo is effectively announcing it.
- **Client documents, internal docs, pitch decks, signed contracts.** Brand folders often accumulate these. They don't belong here.
- **Personal data you haven't confirmed is already public.** The current brand-guide PDF includes some named contact details that are already publicly available; that was a deliberate decision. Don't add anything new without confirming it's already public.
- **API keys, tokens, passwords.** If you're copy-pasting a template, check it for secrets first.
- **Client-specific insurance documents.** Black Cygnet Life is a regulated insurer — anything that looks like a policy schedule, client communication, or advice record does not belong here.

**Fine to commit:**

- Logos, marks, wordmarks (any format).
- Colour palettes and typography tokens.
- Publicly-available brand guideline PDFs.
- Email and social templates with no client data.
- Favicons, icons, illustrations we own.
- Own-brand photography.

**If in doubt, don't commit.** Ask. Removing something from git history after the fact is painful and, for anything sensitive, the damage is already done the moment it's pushed.

## How to make a small change (fix or add)

1. Go to the file in GitHub's web UI.
2. Click the pencil icon (or "Add file" → "Upload files" for new assets).
3. Follow the naming convention — see below.
4. Commit with a clear message: `fix: replace BCL primary logo with cleaner export` or `feat: add BCL social media templates`.
5. Go to the "Releases" page. Click "Draft a new release".
6. Create a new tag following semver (see the [README](./README.md)).
7. Write a one-line summary of what changed. Publish.
8. Update [`CHANGELOG.md`](./CHANGELOG.md) with the same summary (newest entry at top).

jsDelivr will serve the new files within a few minutes for `@main` URLs, and immediately for the new tag URL.

## How to make a major change (breaking)

A change is major if any of these are true:

- A logo file is being renamed or removed.
- A primary brand colour is changing.
- A file format is changing (e.g. dropping the PNG version of something).
- A folder is being restructured.

Before making the change:

1. Check who currently depends on the repo. Ask the engineering team (or search our GitHub org for uses of `cdn.jsdelivr.net/gh/Black-Cygnet-Group/black-cygnet-life-brand`).
2. Warn them in advance via Slack with a target date.
3. Tell them to pin to the current version (e.g. `@v1.5.0`) before you publish.

Then:

1. Make the change.
2. Cut a new major tag (e.g. `v2.0.0`).
3. Update [`CHANGELOG.md`](./CHANGELOG.md) with a clear "BREAKING:" note explaining what changed and how to migrate.
4. Post in Slack that the new tag is live.

Apps pinned to the previous major version keep working unchanged. Apps on `@main` will break immediately — that's why we tell them to pin.

## Naming convention — enforce this

Every BCL asset filename must be named:

    bcl-<asset-type>-<variant>-<colour-treatment>.<ext>

Icons use a single canonical form per icon:

    bcl-icon-<name>.<ext>

Parent-brand (Black Cygnet Group) assets use the `bcg-` prefix:

    bcg-<asset-type>-<variant>-<colour-treatment>.<ext>

**Examples:**

- `bcl-logo-primary-full-colour.svg`
- `bcl-mark-primary-mono-navy.png`
- `bcl-icon-piggy-bank.svg`
- `bcg-mark-primary-mono-black.svg` *(parent-brand swan mark)*

**Asset types in use today:** `logo`, `mark`, `icon`.

**Variants:** `primary`, `secondary`, `horizontal`, `stacked`, `compact`. For BCL today, only `primary` is used.

**Colour treatments:** `full-colour`, `mono-black`, `mono-white`, `reversed`.

**BCL-specific extension:** when an asset is a single-tone fill in a named brand colour, use `mono-<brand-colour-slug>`:

- `mono-navy` (Ocean `#001f49`)
- `mono-sky` (`#439bbb`)
- `mono-misty-rose` (`#f6e2e0`)
- `mono-candy` (`#fe3725`)

All lowercase. Hyphens only. No spaces. No underscores. No version numbers in filenames — that's what git tags are for.

If someone sends you a file called "Logo Final V3 (1).png", rename it before committing.

## Colour tokens — the three-file rule

The `colour/` folder contains three files with the same colour values in different formats:

- [`palette.json`](./colour/palette.json) — the source of truth, used by apps
- [`palette.css`](./colour/palette.css) — CSS custom properties, used by websites and emails
- [`tailwind.colours.ts`](./colour/tailwind.colours.ts) — Tailwind config, used by React apps

**When you change a colour, change it in all three files in the same commit.** There is no build script. This is deliberate — it means you don't need to know Node, npm, or any build tooling to maintain the repo.

Steps:

1. Edit `palette.json` with the new hex value.
2. Edit `palette.css` with the same hex.
3. Edit `tailwind.colours.ts` with the same hex.
4. Commit all three together, e.g. `feat: update Sky to #3b9bbc`.
5. Cut a new major version (colour changes are breaking).

## Who can write to this repo

- Org admins: full access. That's you.
- Anyone else: read-only, or contribution via PR.

Don't grant write access lightly. Brand consistency depends on a small number of people caring about naming and structure.

## Common problems

**"Someone committed a file with a weird name."**
Rename it. Revert the commit. Tell them about the naming convention.

**"jsDelivr is showing an old version."**
jsDelivr caches aggressively. Cache-bust by using a new tag, or append `?v=timestamp` to the URL temporarily. Never expect an instant update on `@main`.

**"An app broke after I changed something."**
They were on `@main` when they should have been on a tag. Send them the README's versioning section and help them pin. Don't roll back — fix their pin.

**"The fonts folder doesn't have actual fonts."**
We don't host licensed font files in this repo (licence terms usually forbid redistribution). [`typography/fonts.md`](./typography/fonts.md) tells you where to get them.

**"The logo colours look slightly off compared to the brand guide."**
Known issue — see [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 1. The brand team owns the decision on whether to re-export the logos or update the palette.

**"The parent-brand swan mark is in this repo but I thought BCG was a separate brand?"**
Correct — see the "Parent-brand assets in this repo" section at the top and [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 6. They're bundled here for convenience until a dedicated BCG repo exists.

## When to ask for help

- Anything involving licence questions (can we host this font? this stock photo?).
- Anything involving the folder structure — if you find yourself wanting to add a new top-level folder, pause and ask.
- Anything involving a new brand being added. (New brands get their own repo, not a subfolder here.)
- If an app team asks for an asset type that doesn't fit the current structure.

## Related repositories

- [Keveko brand assets](https://github.com/Black-Cygnet-Group/keveko-brand)

## Contact

- Repository: https://github.com/Black-Cygnet-Group/black-cygnet-life-brand
- Current owner of record: Gareth Quin (@garethquin) — pending handover to Mike and Imad.
