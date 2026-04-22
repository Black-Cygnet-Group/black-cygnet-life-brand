# Changelog

All notable changes to the Black Cygnet Life brand assets repository will be documented here.
Newest entries at the top. Versions follow [Semantic Versioning](https://semver.org/).

## v0.1.1 — 2026-04-22

Documentation-only patch. No asset changes.

**Fixed:**

- Added a note to the README explaining that the brand guide PDF (~26 MB) exceeds jsDelivr's 20 MB per-file limit and therefore **cannot be fetched via jsDelivr**. The README now provides a GitHub Raw URL as the direct-download path instead. Apps consuming logos, tokens, and icons via jsDelivr are unaffected.
- Added [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 7 asking the brand team to produce a compressed version (or split the PDF) to make it CDN-accessible.

## v0.1.0 — 2026-04-22

Initial release. Migrated Black Cygnet Life brand assets from local source folders into this public repo, served via jsDelivr.

**Added:**

- Primary logo set — 4 colour treatments (`full-colour`, `mono-navy`, `mono-misty-rose`, `mono-white`) in SVG + PNG (1601 × 947). See [`logo/primary/`](./logo/primary/). No `mono-black` variant is currently supplied — see [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 2.
- Logo mark set — 6 colour treatments (`mono-black`, `mono-white`, `mono-navy`, `mono-sky`, `mono-misty-rose`, `mono-candy`) in SVG + PNG (1001 × 1001). See [`logo/mark/`](./logo/mark/).
- Black Cygnet Group parent-brand swan mark, 6 colour treatments in SVG + PNG, in [`parent-brand/mark/`](./parent-brand/mark/). Included here for convenience (BCL collateral frequently references the parent brand); will eventually move to a dedicated BCG brand repo. See [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 6.
- Icon library of 48 custom icons, each in SVG + PNG. **These icons are byte-identical to the set in the Keveko brand repo** — same source design system, shared across both brands. Any future icon update should be made in both repos in the same sprint to keep them in sync.
- Colour palette tokens in three hand-kept-in-sync formats: [`colour/palette.json`](./colour/palette.json), [`colour/palette.css`](./colour/palette.css), [`colour/tailwind.colours.ts`](./colour/tailwind.colours.ts). The BCL palette is 4 colours + white — Ocean, Misty Rose, Candy, Sky (note: BCL does not use Maroon, which is part of Keveko's palette).
- Typography spec ([`typography/typography.json`](./typography/typography.json)) and font-sourcing guide ([`typography/fonts.md`](./typography/fonts.md)).
- Canonical brand guidelines PDF ([`guidelines/black-cygnet-life-brand-guide.pdf`](./guidelines/black-cygnet-life-brand-guide.pdf)) — 33 pages, includes brand manifesto, personality, colour, typography, photography treatment, and application examples.
- Repository documentation: [`README.md`](./README.md), [`HANDOVER.md`](./HANDOVER.md), [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md).

**Renamed during migration:**

- All BCL files renamed to `bcl-<asset-type>-<variant>-<colour-treatment>.<ext>` — see [`HANDOVER.md`](./HANDOVER.md) for the full convention.
- Parent-brand assets renamed to `bcg-<asset-type>-<variant>-<colour-treatment>.<ext>` so they can never be confused with BCL assets.
- Symbol/mark variants renamed to the canonical brand-colour taxonomy: `dark-blue` → `mono-navy`, `light-blue` → `mono-sky`, `light-pink` → `mono-misty-rose`, `red` → `mono-candy`, `pink` → `mono-misty-rose`.
- Fixed a typo in the source PNG filename: `black-cygnet-life-logo-light pink.png` (containing a space) → `bcl-logo-primary-mono-misty-rose.png`. The sibling SVG already used hyphens correctly.
- Icon typo fix (same as Keveko): `socument-secure.{svg,png}` → `bcl-icon-document-secure.{svg,png}`.

**Skipped during migration (for reference):**

- 108 files in a Finder-duplicate `… 2/` folder (the macOS rename-on-conflict artifact from extracting the source zips twice). Byte-for-byte identical to the canonical folders — confirmed via `diff -rq`.
- 3 archive (`.zip`) files redundant with their extracted folders.
- 1 internal working DOCX (`black-cygnet-life-assets-logos-fonts-icons-brand-notes.docx`) — content used as a source for the tokens and README, but the document itself not committed. See [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) item 5.

**Known issues to be resolved by the brand / marketing team** — see [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md):

1. Logo SVGs use hex values that don't match the canonical palette — same issue as Keveko. Tokens use the canonical values; logo SVGs are committed as-supplied pending re-export.
2. No `mono-black` primary logo variant exists.
3. The "Feeling Passionate" accent font has no confirmed vendor source.
4. The `document-secure` icon rename (see above) should be verified by the brand team.
5. Tone-of-voice internal DOCX — decide whether to polish and publish.
6. Parent-brand swan mark currently lives here; long-term home is a dedicated BCG repo.
