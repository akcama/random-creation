Random Creation — WPF desktop app (C# / .NET 8)

**App:** Random Creation (Windows desktop) · **Current version:** 4.0, released August 2026
**Original working title:** Creature Crafter (v1.0), renamed in v2.0.

Random Creation generates random combinations from user-defined content. The user
creates **Collections** (Creatures, Starships, Guns), adds **Category Groups** to each
(HEAD, BODY, LIMBS), adds **Categories** to each group (Head Style, Head Count), and adds
**Options** to each category (Horned, Round, Tiny). Generate picks one random option from
every enabled category in every enabled group in every enabled collection and displays the
combination as grouped result cards. The system is deliberately general purpose — it works
for any kind of random combination generator, so never hard-code assumptions about
creatures or any other subject matter.

Personal creative tool, not a commercial product. Currently in personal use and
small-pool testing.

--- AI PM — keep this block intact ---
This project runs AI PM. The session-start hook delivers the method at
every session start; if this session opened without an AI PM opener,
type /ai-pm-setup. The project's memory is docs/; its map is docs/index.md.
--- end AI PM block ---

Where everything lives, what each record document is authoritative for, and its state:
`docs/index.md`. The facts about the toolchain, GitHub and the pipeline: `docs/environment.md`.

## ⚠️ Where the live code is

**Only one copy of the source is real:** the Visual Studio solution under
`Source\RandomCreation\`. Before editing any file, confirm the path starts there. If a
search turns up several copies of `ManageContentScreen.xaml.cs` (the pre-git snapshots under
`docs\archive\` hold older ones), the one to change is
`Source\RandomCreation\RandomCreation\ManageContentScreen.xaml.cs`.

## Version control

The developer is **new to git and GitHub — explain git operations plainly as they happen**,
in plain language, at the time they run. Build output, the `Releases\` archive and the
machine-local file are git-ignored; everything else, live source and `docs\`, is tracked.

The repository is **public, but not open source**: the root `LICENSE` is all-rights-reserved
and `README.md` declines code contributions, which is what keeps a future sale possible.
Commits use a GitHub noreply identity so the real address never reaches the public repo.
Push early and often: a push is backup, not publication. The full scheme is in the
development lifecycle guide.

**Deletions must be loudly flagged in advance or handed to the developer** — never
deleted quietly. Tracked files are recoverable from git history after deletion; ignored
and untracked files (anything under `Releases\`, or any `bin\`/`obj\` folder) have no
safety net at all, so those need an explicit ruling every time.

## Tech stack and build

- **C# / WPF**, targeting **.NET 8.0 (Windows)**
- **No NuGet packages.** Serialization is `System.Text.Json`, built into .NET 8. Keep it
  that way — do not add dependencies without asking.
- Single solution, single project. The .NET SDK installed with Visual Studio builds this
  project from the command line in about seven seconds, so Visual Studio does not need to
  be open to build or run.
- Assembly version lives in `RandomCreation.csproj` (`AssemblyVersion` / `FileVersion`),
  currently `4.0.0.0`. The Settings About section reads it from the assembly at runtime —
  never hard-code a version string in the UI. At release the pipeline overrides it from the
  git tag, so tag and assembly always agree.

```
cd "Source\RandomCreation"
dotnet build
dotnet run --project RandomCreation
```

Releases are built by GitHub Actions: pushing a tag like `v4.0` publishes a self-contained
single-file win-x64 build as both a portable zip (~70 MB) and an Inno Setup installer,
attached to a GitHub Release. The Actions "Run workflow" button is a dry run — builds
everything, publishes nothing. The old local publish profile
(`RandomCreation\Properties\PublishProfiles\FolderProfile.pubxml`) still exists but points
at a dead output path; the pipeline is the release mechanism.

The **product page** for non-technical visitors lives under `site\` (plain HTML and CSS)
and is served by GitHub Pages at https://akcama.github.io/random-creation/. **Any change
under `site\` that lands on main is live within a minute** — an edit there is publication,
not backup, so preview it first (`.claude\launch.json` serves it to the in-app browser).

## Architecture

**Navigation.** `MainWindow` owns everything. Screens are `UserControl` panels stacked in
a root `Grid`; exactly one is `Visible` at a time (`MainPanel`, `ManageContentPanel`,
`HistoryPanel`, `SettingsPanel`, `OverlayPanel`). Overlay screens (Collections Management,
Presets) go through `ShowOverlay(UserControl)` / `HideOverlay()`. `ResultDetailDialog` and
`PrintPreviewDialog` are separate `Window` instances.

**No MVVM.** There is no binding/command layer and none should be introduced. `DataService`
is a static class; screens read and write it directly, call `DataService.SaveX()` after
every mutation, then call their own `Refresh()` to rebuild their ItemsSource. ViewModel
classes in `Models.cs` are plain UI wrappers, not an MVVM layer.

**Services are all static classes with no UI:**

| Service | Responsibility |
|---------|----------------|
| `DataService` | All persistence — load, save, migrate, presets, history, changelog |
| `ThemeService` | Swaps merged resource dictionaries; resolves System theme |
| `UndoService` | In-memory undo stack, depth 10, lambda restore actions |
| `ClipboardService` | Internal clipboard (not the system one) at Option/Category/Group level |
| `ToastService` | Bottom-centre toast overlay, 150 ms in / 2 s hold / 300 ms out |

**Data hierarchy** (`Models.cs`):

```
CategoriesData → List<Collection> → List<CategoryGroup> → List<Category> → List<Option>
```

`CategoryGroup` is the v3.0 addition. The `Random` prefix was dropped from model names in
v3.0 (`RandomCollection` → `Collection`, etc.). Depth is exactly one group level — but do
not write code that would make adding child groups a rewrite.

**Generation rule.** A category is rolled only if its collection, its group, *and* itself
are all enabled. Weighted random selection over the enabled options.

## Conventions that matter

- **Theming: always `DynamicResource`, never `StaticResource`,** for any brush that differs
  between themes. Both `Themes\DarkTheme.xaml` and `Themes\LightTheme.xaml` must define
  every key. `App.xaml`-level resources outcompete merged dictionaries, which is why
  `ThemeService.ApplyTheme()` explicitly reassigns `SelectedCategoryBrush` after the swap.
  (The v3.0-shipped bug where `Themes\` held v2.0 dictionaries was fixed in v4.0 — BUG 1 in
  the release plan. Its lasting lesson: theme mistakes compile cleanly, so verify visually.)
- **Undo: one user gesture = one undo step.** A single click that changes many items
  (Enable All, multi-select paste) reverses as one step. Push to `UndoService` for delete,
  rename, add, drag reorder/move, cut, paste, enable/disable toggle, and weight change.
  Do *not* push navigation or dialog open/close. The stack is never persisted.
- **Font scaling** is a `LayoutTransform ScaleTransform` on `MainContentGrid`
  (Normal 1.0 / Large 1.3 / Extra Large 1.7). Any drag-and-drop coordinate maths must go
  through `TranslatePoint` / `TransformToAncestor` to stay correct at non-1.0 scale — this
  was a real v3.0 bug, don't reintroduce it with a raw `e.GetPosition(container)`.
- **Drag and drop exists in three places** — `ManageContentScreen`,
  `CollectionsManagementScreen`, `PresetsScreen`. A fix to one usually belongs in all three.
  Insertion index must clamp to `[0, count]` at both ends, and `_dropIndex` is re-validated
  at `MouseUp`.
- **Name collisions** use a counter suffix: `Name (2)`, `Name (3)` — lowest integer ≥ 2 that
  is unique in the target container.
- **UI aesthetic:** WinUI 3 / Windows 11. No gradients, no drop shadows, rounded corners,
  custom borderless window with matching title bar. Dark accent `#0a84ff`, result values
  `#60aaff`, destructive `#e05050`, drawn/success `#30d158`.
- **`ManageContentScreen.xaml.cs` is ~2,400 lines** and the most complex file in the
  project. Read the relevant region before editing; it has a right-panel state machine
  (Default / GroupDetail / Options) and several parallel selection HashSets.

## Data files

**Where user data lives depends on the build** (v4.0): a `portable.txt` marker beside the
exe (shipped in the portable zip, excluded by the installer) means data lives in `data\`
beside the exe, and copying that folder moves a user's whole setup; no marker means
`%LocalAppData%\RandomCreation\`, where installs and uninstalls cannot touch it.
`DataService.IsPortable` decides once at startup; `DataService.DataFolderPath` is the
public accessor, and Settings has an "Open data folder" button. The dev build in
`bin\Debug` carries the marker, so development always runs portable. **Program files**
(`changelog.txt`, `samples\categories.json`) sit beside the exe, are replaced every
release, and are never written by the app.

| File | Contents |
|------|----------|
| `settings.json` | Theme, font size, window geometry, sidebar width, history limit, confirm-on-delete, **`SchemaVersion`**, the ever-climbing **`GenerationCounter`** |
| `categories.json` | All collections/groups/categories/options. Intentionally **no version field** — kept clean for hand-editing and AI-assisted editing |
| `history.json` | Generation history with timestamps, serials, dim states, group membership, `IsDrawn` |
| `presets.json` | Named snapshots of enable/disable state down to option level |

**`SchemaVersion` in `settings.json` is the single source of truth for data recognition.**
`DataService.Initialise()` has exactly three cases (v4.0 removed the v1/v2 migrations —
nobody held pre-v3.0 data): no data files at all → fresh start, no dialog; `3` → load
normally; anything else → every file backed up with `.bak`, fresh start, one-time notice.
Never create the data folder before deciding which case applies — that ordering bug is
what shipped BUG 2.

**Sample content installs conditionally, and only ever onto nothing.** The sample lives at
`Source\RandomCreation\RandomCreation\SampleData\categories.json`, ships to `samples\`
beside the exe, and at startup is copied into the data folder **only when no
`categories.json` exists there** — so a new user starts with a working example and an
existing user's content can never be overwritten. The rule was always "never overwrite
user content," and the conditional copy honours it. The sample is the product's first
impression: three collections of visibly different kinds (Creature, Starship, Swords),
only Creature enabled, so it never reads as a monster generator.

**Serial numbers** (v4.0): every generation gets `#N` from `GenerationCounter` in
settings — stored, never derived from history, never reset (paper outlives the app's
history). Shown everywhere a result appears, including the print footer.

## Working agreements

- **Update `changelog.txt` in the same change** that adds a user-visible feature or fix.
  Newest version at top. It is the About section's content, so write it for a user.
- **Keep the docs in step.** The record documents under `docs\` (listed in the index) hold
  the architecture, the file index and the engineering notes. If a change alters
  architecture, data shape, or a screen's layout, say so rather than letting the records
  silently drift.
- Ask before adding a NuGet package, introducing MVVM, or changing the JSON shape of
  `categories.json` — the last one is user-editable by design.
- The `← Back` button styling, an A–Z sort button, `categories.json` import, and
  keyboard-shortcut customisation are **deliberately deferred**, not oversights. See the
  Deferred section of the v3.0 project context record before "fixing" them.
