# Random Creation — Backlog

Forward-looking work only; no status narrative, no history; done leaves and the changelog records it. Charter: the method's `charters.md`. A line may carry a state tag `[started · <developer>]` in CURRENT, a bring-up token `(bring up: YYYY-MM-DD)` anywhere, and points at the document with the full picture.

## Current

- Nothing underway.

## Planned

The post-release chores of v4.0, in intended order.

- DOWNLOAD-BACK VERIFICATION. Download the published v4.0 assets from GitHub and confirm
  they run: the lifecycle guide's precondition for retiring the local Releases folder. The
  developer tested the dry-run artifacts thoroughly; the published files are a fresh build
  of the same commit and still deserve the direct check. The download URLs go through the
  akcama redirect, so this doubles as a check that redirected downloads work.
- THE ONE LIVE USER'S UPGRADE, manual, and it must carry her data. Old app: Settings, Open
  data folder, copy everything. Install v4.0, Open data folder, paste. Without this her
  collections would appear to vanish (they would still be in the old portable folder). She
  has built no generations yet, which is what made the data relocation cheap, but she may
  have collections. Coordinate with the developer. The standing condition is in the
  environment register.
- v4.0 RECORD DOC, then retire the release plan. Write the v4.0 design record (what shipped,
  how each item was implemented, deviations: none), absorbing the release plan record in
  docs/design, which retires on absorption per its own header. A good candidate for a
  dedicated session; the file index in docs/reference is also a version behind (v3.0).
- RELEASES FOLDER RETIREMENT (781 MB, git-ignored, no safety net). After the download-back
  verification: upload the v3.0 zip to GitHub as a historical release (the only exact copy
  of what the live user runs; git history starts after v3.0 shipped), decide the v1.0 and
  v2.0 zips (their source is already safe in docs/archive), then delete the local folder on
  an explicit ruling.

## Proposed

- Updater. TRIGGER: a ruling to build it; deferred from v4.0 by ruling. Three options in the
  lifecycle guide section 6; the no-dependency GitHub Releases API check remains the
  recommended fit.
- Remaining v4.0 screenshots. TRIGGER: the v4.0 record doc wanting them, or a product-page
  section showing settings, printing or presets. The product page shipped on the five
  README-facing shots; the deeper v3.0 set (settings, dialogs, print preview, presets)
  still documents v3.0.
- Refactor and feature candidates from the v3.0 era: the ManageContentScreen refactor,
  ObservableCollection, Redo, weight tier customisation, categories.json import,
  single-collection export, full group detail interactivity. Recorded in the engineering
  notes in docs/reference.

## Ongoing

- Workflow action versions. The release pipeline's helper actions (checkout@v4,
  setup-dotnet@v4, upload-artifact@v4) run on Node.js 20, which GitHub is deprecating on its
  runners. A cosmetic warning today; bump the @vN numbers whenever the workflow is touched.
  Done when all three run on a newer Node.js.
