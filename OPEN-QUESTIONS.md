# Open Brand Questions — Black Cygnet Life

This file lists open questions the brand and marketing teams need to resolve before they can be incorporated into the brand assets repo.

Each item has:

- **Context** — what we found, and why it's a question.
- **Decision needed** — the options, laid out as a checklist.
- **Interim approach** — what the repo is doing today, until the decision is made.

**How to respond.** Reply to whoever shared this file with you (currently: Gareth Quin / @garethquin) with your decision on each numbered item. Your answers will then be applied to the repo in a new version (`v0.2.0` or similar), and the assets updated accordingly.

> **Heads-up on consistency with the Keveko repo.** Items 3, 4, and 5 below are the same questions as in the [Keveko `OPEN-QUESTIONS.md`](https://github.com/Black-Cygnet-Group/keveko-brand/blob/main/OPEN-QUESTIONS.md). The answers should be the same in both places (same font, same icon, same DOCX-publishing decision). Please answer them once and they'll be applied to both repos.

---

## 1. Logo SVG colours don't match the canonical brand palette

**Context.** The brand guide (`guidelines/black-cygnet-life-brand-guide.pdf`, page 15) and the internal brand notes both specify these canonical hex values for the primary brand colours:

- Ocean: **`#001f49`**
- Misty Rose: **`#f6e2e0`**
- Candy: **`#fe3725`**
- Sky: **`#439bbb`**

However, the supplied logo / symbol SVG files actually use:

- Navy in logos: **`#112148`** (not `#001f49`) — visibly lighter
- Misty Rose in logos: **`#f6e2df`** (not `#f6e2e0`) — last digit off
- Candy in logos: **`#ef3d2e`** (not `#fe3725`) — **visibly different**
- Sky in logos: **`#439bbb`** ✓ matches
- Also appearing: `#231f20` (a near-black) and `#142147` (a second navy), likely Illustrator-default approximations

Same pattern as the Keveko repo — the logos appear to have been exported against an older palette or drifted in export, and the Candy drift is noticeably off.

**Decision needed.** Which of the following is correct?

- [ ] **A. The brand guide is authoritative — re-export the logo SVGs.** The designer re-exports to match `#001f49`, `#f6e2e0`, `#fe3725`, `#439bbb`. New SVGs replace the current ones.
- [ ] **B. The logo SVGs are correct — update the brand guide instead.** Canonical palette becomes `#112148` / `#f6e2df` / `#ef3d2e` / `#439bbb`.
- [ ] **C. Other — specify:** ____________________

**Interim approach in the repo.** Token files (`colour/palette.json`, `colour/palette.css`, `colour/tailwind.colours.ts`) carry the brand-guide hexes. Logo SVGs are committed as-supplied. Apps pulling colour from tokens match the guide; logos render slightly off until re-exported.

---

## 2. No `mono-black` primary logo variant exists

**Context.** The BCL primary logo was supplied in 4 colour treatments: `full-colour`, `mono-navy` (from the source `dark-blue`), `mono-misty-rose` (from `light-pink`), and `mono-white`. There is no `mono-black` variant — neither as an SVG nor a PNG.

The Keveko repo has a `mono-black` variant, as do many brand systems. Its absence from BCL could be a deliberate decision or simply a gap in the supplied set.

**Decision needed.**

- [ ] **A. Intentional — no `mono-black` variant is required for BCL.** Acknowledge in the brand guide.
- [ ] **B. Missing — please produce one.** ETA: ____________________

**Interim approach in the repo.** The 4 supplied variants are in [`logo/primary/`](./logo/primary/) and usable now. If a `mono-black` is produced later, it will be added in a future release.

---

## 3. "Feeling Passionate" accent font — source and licence unknown

*(This is the same question as [Keveko `OPEN-QUESTIONS.md` item 3](https://github.com/Black-Cygnet-Group/keveko-brand/blob/main/OPEN-QUESTIONS.md). Answer once; applies to both.)*

**Context.** The internal BCL brand notes list three fonts:

- **Museo Sans** — primary; available via Adobe Fonts and MyFonts.
- **Century Gothic** — web fallback; widely licensed.
- **Feeling Passionate** — accent, for internal communication only. The DOCX explicitly says `"Licenses: Pending??"`.

The repo's font-sourcing document ([`typography/fonts.md`](./typography/fonts.md)) needs to tell developers where to obtain each font, but "Feeling Passionate" isn't immediately identifiable from any of the major font distributors, and the licence status is unconfirmed.

**Decision needed.**

- [ ] **A. The vendor and licence for the font is:** ____________________
- [ ] **B. We no longer use this font — remove it from all brand documentation.**
- [ ] **C. Replace it with:** ____________________

**Interim approach in the repo.** `fonts.md` lists the font with a "source to be confirmed" note pointing back at this open question. No font file is bundled (commercial font licences forbid redistribution via public repos regardless).

---

## 4. Confirm the `document-secure` icon rename

*(This is the same question as [Keveko `OPEN-QUESTIONS.md` item 4](https://github.com/Black-Cygnet-Group/keveko-brand/blob/main/OPEN-QUESTIONS.md). Answer once; applies to both.)*

**Context.** Two icon files were supplied named `socument-secure.svg` and `socument-secure.png`. The internal notes explicitly reference a "document secure" icon in the Protection category, so this appears to be a simple typo ("s" instead of "d"). During migration, the files were renamed to `bcl-icon-document-secure.{svg,png}` (and `keveko-icon-document-secure.{svg,png}` in the Keveko repo).

**Decision needed.**

- [ ] **A. Confirm the rename is correct.** *(Expected default — open the icon, verify it depicts a secured document, and tick this box.)*
- [ ] **B. The icon is not a "document secure" icon — the intended name is:** ____________________

---

## 5. Should the brand tone-of-voice notes be made public?

*(Same question as [Keveko `OPEN-QUESTIONS.md` item 5](https://github.com/Black-Cygnet-Group/keveko-brand/blob/main/OPEN-QUESTIONS.md). Answer once; applies to both.)*

**Context.** The internal brand notes document (`black-cygnet-life-assets-logos-fonts-icons-brand-notes.docx`) contains substantial tone-of-voice, vocabulary, and copy-style guidance — plus design-system specifications (spacing grid, button styles, icon stroke weight) — that is not duplicated in the public brand guide PDF.

However, the DOCX was authored as an internal handover document and contains rough design-process annotations that aren't polished for external use.

**Decision needed.**

- [ ] **A. Produce a polished public tone-of-voice guide** (markdown or PDF) to live alongside the brand guide in `guidelines/`. Who will own this: ____________________
- [ ] **B. Keep tone-of-voice internal only.** The current brand guide PDF is the only public documentation.
- [ ] **C. Commit the DOCX as-is** to `guidelines/`, acknowledging it's rough but useful.

**Interim approach in the repo.** The DOCX is **not** committed. Its palette, typography, and icon-usage facts have been extracted into the README and token files. Tone-of-voice content is not currently surfaced anywhere public.

---

## 6. Parent-brand swan mark — long-term home

**Context.** The BCL source folder contained a `Swan Icon/` subfolder with 6 colour treatments of the Black Cygnet Group parent-brand swan (filenames `black-cygnet-icon-<colour>.{svg,png}`). These are not BCL assets — they belong to the parent brand.

For v0.1.0 they have been committed into this repo under [`parent-brand/mark/`](./parent-brand/mark/) with a `bcg-` filename prefix so they can't be confused with BCL's own mark. This means consumers of BCL-related collateral can still reference the parent-brand mark from one place.

**Decision needed.**

- [ ] **A. Acknowledge this is a stop-gap.** Eventually a dedicated `Black-Cygnet-Group/black-cygnet-group-brand` repo should be created, the parent-brand assets moved there, and this folder deleted from the BCL repo. Target date: ____________________
- [ ] **B. Keep them here permanently.** Document that this repo is the canonical home for both BCL and BCG brand marks, and update the README accordingly.
- [ ] **C. Other — specify:** ____________________

**Interim approach in the repo.** Parent-brand assets live in [`parent-brand/mark/`](./parent-brand/mark/) with the `bcg-` prefix. The README and HANDOVER explain their presence. This is workable indefinitely, but creating a dedicated BCG repo is the cleaner long-term answer if the parent brand is actively maintained.

---

## 7. Brand guide PDF exceeds jsDelivr's 20 MB file limit

**Context.** The canonical brand guide PDF is ~26 MB, which exceeds jsDelivr's 20 MB per-file limit for GitHub-served content. The PDF is still committed to the repo and viewable on GitHub, but **cannot be fetched via jsDelivr URLs** — the CDN returns a 403 with the message "File size exceeded the configured limit of 20 MB."

This doesn't affect apps (they consume logos and tokens, not the PDF), but it's a friction point for anyone expecting to open the brand guide via a CDN link.

**Decision needed.**

- [ ] **A. Produce a compressed version of the PDF** (target: under 15 MB, with a comfortable margin). The designer can downsample embedded images, flatten to a single compressed image stream, and save with optimised settings. Replace the current PDF when ready; no versioning concern (it's a patch).
- [ ] **B. Split the PDF** into smaller sections (e.g. by chapter — manifesto, logo, colour, typography, applications) so each is under 20 MB and individually fetchable via jsDelivr.
- [ ] **C. Accept the limitation permanently.** The PDF is only for human reference; GitHub direct-download works fine. No change to the current setup.

**Interim approach in the repo.** The full uncompressed PDF is committed at its original size (~26 MB). The README includes a GitHub Raw URL for direct download. Apps that consume assets via jsDelivr are unaffected — they don't need the PDF.

---

*Last updated: 2026-04-22.*
