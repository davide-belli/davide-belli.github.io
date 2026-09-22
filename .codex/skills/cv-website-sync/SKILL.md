---
name: cv-website-sync
description: Sync this personal website with Davide Belli's latest CV when the CV PDF has changed. Use for requests to update the site from the CV, not for unrelated website edits.
---

# CV website sync

Update this repository from the authoritative CV at `https://github.com/davide-belli/curriculum-vitae/blob/master/CV_Davide_Belli.pdf`.

1. Work in a fresh directory created with `mktemp -d` under the system temporary directory. Download the PDF there using the raw GitHub URL: `https://raw.githubusercontent.com/davide-belli/curriculum-vitae/master/CV_Davide_Belli.pdf`. Check that it is a PDF before continuing.
2. Extract layout-preserving text from both the downloaded PDF and `assets/input/cv.pdf` with `pdftotext -layout`. Diff the extracted texts, then identify semantic changes rather than treating spacing, page headers/footers, or extraction artifacts as content changes.
3. Inspect the surrounding HTML before editing. Map CV content only to the corresponding existing sections:
   - `index.html`: role/about, stated patent totals, skills, and education.
   - `research.html`: publications and granted/pending patents.
   - `awards.html`: honors and volunteering/service.
   Preserve information in the website that has no corresponding CV section unless the CV directly contradicts it.
4. Follow the existing markup, ordering, typography, and editorial conventions in each page. Update matching records in place and add genuinely new records in the appropriate chronological group. Keep `D Belli` highlighted using the existing publication markup. Do not fabricate publication links, thumbnails, venues, dates, or descriptions: use the existing placeholder thumbnail and an empty links container when the CV does not supply a source URL or image.
5. Treat source anomalies carefully. Deduplicate identical patents by title and application/patent number; do not add the same patent twice merely because it appears twice in extracted text. Report contradictions such as a stated total that does not reconcile with unique entries. Do not silently remove unrelated website content to force a match.
6. Validate every edited HTML page with an HTML5-capable checker, or an equivalent structural check when only a legacy validator is available. Do not mistake a legacy validator's unsupported-HTML5 errors for website defects. Review `git diff` to ensure only CV-driven changes were made. Only after the website edits validate, replace `assets/input/cv.pdf` with the downloaded PDF so it becomes the baseline for the next run.
7. Report the semantic changes applied, the files changed, and any ambiguity or source-quality issue. Do not retain temporary copies of the downloaded CV after the run; `assets/input/cv.pdf` is the required baseline copy.
