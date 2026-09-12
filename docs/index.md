# Random Creation — Index

`docs/` is this project's memory. This file is its map and the only where-is map in the project: every other file may cite a path it needs, none may carry a map. Three sections, fixed columns. Charter: the method's `charters.md`.

## Where things live

| Path | What is there | Rule |
| --- | --- | --- |
| `docs/` | the project's memory: the cadence files at its top, the record documents by kind below | memory is edited at close-out |
| `docs/ai-pm/` | AI PM's own: the config, the applied version, the tool registrations, the usage log | registrations belong to their tools |
| `docs/design/` | design records: the project context per app version, the v4.0 release plan | |
| `docs/reference/` | code-level reference: the engineering notes, the v3.0 file index | |
| `docs/guides/` | how the project is worked and shipped: the development lifecycle | |
| `docs/assets/icons/` | the app icon: the master and every exported size | design masters; the shipped icon is in the source tree |
| `docs/assets/screen-shots/` | UI screenshots by app version, v1.0 to v4.0; the v4.0 set feeds the README | |
| `docs/archive/` | pre-git source snapshots at v1.0 and v2.0, the only surviving copies; git history starts at v3.0 | source, not records; never edited |
| `Source/` | the source tree: one solution, one project | |
| `Source/RandomCreation/` | the live Visual Studio solution, the only real copy of the source | the only place to change code |
| `Source/RandomCreation/RandomCreation/SampleData/categories.json` | the sample content, shipped to `samples\` beside the exe | installs only onto nothing; never overwrites user content |
| `Source/RandomCreation/RandomCreation/changelog.txt` | the app's user-facing changelog, a program file beside the exe | updated in the same change as a user-visible feature or fix |
| `Source/RandomCreation/Installer/RandomCreation.iss` | the Inno Setup installer script: per-user, no UAC, the uninstaller keeps content by default | |
| `.github/workflows/release.yml` | the tag-driven release pipeline: portable zip and installer, attached to a GitHub Release | the Run workflow button is a dry run |
| `site/` | the product page: one HTML file, one stylesheet, its screenshots and icons copied under `assets/` | any change here that lands on main is published live within a minute |
| `.github/workflows/pages.yml` | the product-page deploy: publishes `site/` to GitHub Pages on any change to it on main | |
| `.claude/launch.json` | the browser launch config: serves `site/` on port 8765 for a local preview | tooling, not governance |
| `Releases/` | the local release archive, about 780 MB: the v1.0 source and build, the v2.0 and v3.0 zips; git-ignored | no safety net: any deletion needs an explicit ruling |
| `bin/`, `obj/`, `.vs/` | build output and IDE scratch, git-ignored | the dev build under bin carries the portable marker |
| `https://github.com/akcama/random-creation` | the repository (remote `origin`), public, all rights reserved; its Releases page holds the v4.0 installer and portable zip; its About box links to the product page | a push is backup, not publication; the old henry-akcama address redirects |
| `https://akcama.github.io/random-creation/` | the product page, the link to give people: one Download button reading the newest release from GitHub at page load | served by GitHub Pages from `site/` |
| `CLAUDE.local.md` | facts about this machine, never committed | its shape is `CLAUDE.local.template.md` |

## The documents

| Path | Authoritative for | State |
| --- | --- | --- |
| `docs/handoff.md` | where the work stands and the next move | LIVE |
| `docs/backlog.md` | the work ahead | LIVE |
| `docs/changelog.md` | what happened, when, and where the detail lives | LIVE |
| `docs/environment.md` | the facts about the systems the project runs on | LIVE |
| `docs/guides/development-lifecycle.md` | HOW THE PROJECT IS WORKED AND SHIPPED: storage scheme, build cycle, git and GitHub, licensing, packaging, sample content, the program-files versus user-data split. Distinct from every other record, which describe the app | LIVE |
| `docs/design/2026-08-01-release-plan-v4.0.md` | WHAT v4.0 CONTAINS, IN WHAT ORDER, AND WHY | LIVE; retires once absorbed into a v4.0 record doc (backlog, Planned) |
| `docs/design/2026-06-06-project-context-v3.0.md` | v3.0 design: architecture, every screen's layout, undo, toast, clipboard and drag specs, colour palettes, bug-fix table, deferred list. Still the deep architecture record until a v4.0 record absorbs it | FROZEN |
| `docs/reference/engineering-notes.md` | CODE-LEVEL ENGINEERING KNOWLEDGE: WPF traps, resource-precedence rules, weight-tier probability anchors, code-quality warnings, refactor candidates | LIVE |
| `docs/reference/file-index-v3.0.md` | what each source file does and what changed in v3.0 | STABLE; a version behind |
| `docs/design/project-context-v2.0.md` | the v2.0 design record | FROZEN |
| `docs/design/project-context-v1.0.md` | the v1.0 design record; its date is not established | FROZEN |

No amendment chain: each record is authoritative for its own scope and none amends another.

## What governs Claude

| Layer | Fires | File |
| --- | --- | --- |
| Always on | every session | `CLAUDE.md`; `CLAUDE.local.md` (per machine, uncommitted); the developer's user-level CLAUDE.md, which carries the working style |
| On task match | when the work matches a skill's description | the user-level skills (the AI PM commands among them); the project has no skills of its own |
| On file contact | when a file under a rule's paths is touched | none: the project has no `.claude/rules/` |
| Enforced | by the platform, no judgment | the user-level session-start hook and permissions; the project has no `.claude/settings.json` |
