# Random Creation — Environment

The facts about the systems this project runs on, one fact per row. Machine facts live in `CLAUDE.local.md`; tool versions in their registrations; a secret's value nowhere here, only where it lives. Charter: the method's `charters.md`.

## Components

| Component | Value | As of | Verified how | Re-verify when |
| --- | --- | --- | --- | --- |
| Target framework | .NET 8.0 (Windows), C# / WPF, no NuGet packages; System.Text.Json for serialization | 2026-08-02 | RandomCreation.csproj at the v4.0 release | at each release |
| .NET SDK on the dev machine | 9.0.316, installed with Visual Studio 2022 Community; builds the net8.0 project from the command line in about seven seconds | 2026-08-01 | dotnet build | when Visual Studio updates |
| Shipped app | v4.0, tag v4.0, assembly 4.0.0.0; an installer and a portable zip on the GitHub Releases page | 2026-08-02 | the release page, the developer's install test and a proof print | at each release |
| Release pipeline | GitHub Actions on windows-latest: actions/checkout@v4, actions/setup-dotnet@v4 (8.0.x), actions/upload-artifact@v4; Inno Setup 6 from the runner image; a pushed tag publishes, the Run workflow button is a dry run | 2026-08-02 | the v4.0 release run | at each release |
| GitHub repository | akcama/random-creation, public, all rights reserved; remote origin; the old henry-akcama address redirects; the About box's website link points at the product page | 2026-09-12 | the About link set by API and read back; pushes throughout the session | if the repository moves again |
| Product page | GitHub Pages at https://akcama.github.io/random-creation/, source "GitHub Actions"; `.github/workflows/pages.yml` (checkout@v4, configure-pages@v5, upload-pages-artifact@v3, deploy-pages@v4, on Node.js 24) publishes `site/` on any change to it on main; the Download button reads the newest release's installer, portable zip, version and size from the Releases API at page load, falling back to the latest-release page | 2026-09-12 | Pages enabled by API; the deploy run succeeded on rerun; the live page opened, both download links resolving, version and size filled in | at each release |
| Commit identity | the GitHub noreply alias 311688069+henry-akcama, set globally on the dev machine; the real address exists nowhere in the history | 2026-08-01 | git log after the filter-branch rewrite | when a workstation joins |
| Installer | Inno Setup script: per-user, no UAC, %LocalAppData% data, the uninstaller keeps user content by default | 2026-08-02 | the developer's installer and uninstaller test | at each release |

## When this changes

| Change | Then |
| --- | --- |
| Visual Studio or the .NET SDK updates | run `dotnet build` from the command line and update the SDK row |
| the repository moves again | sweep the references: CLAUDE.md, the index, the release workflow's notes link, the installer's publisher fields, the in-app GitHub link in DataService.cs, the lifecycle guide, the README's product-page link, `site/index.html` (the API address and every GitHub link) and the Pages workflow's comment; the Pages address itself changes with the owner, so the About link and every pointer to it move too; the 2026-08-03 changelog entry lists the eight files of the last sweep |
| a workstation joins | run `/ai-pm-setup` there; set the noreply commit identity globally before the first commit |
| a release is cut | push the tag; the pipeline overrides the assembly version from it, so tag and assembly agree; then open the product page and confirm the Download button shows the new version and size, since it reads them from the release's asset names |

## Standing conditions

| Condition | Since | Ends when | Treat as | Bring up |
| --- | --- | --- | --- | --- |
| The one live user runs app v3.0 portable, her data in the old data folder beside the exe | 2026-08-02 | her manual upgrade carries her data to v4.0 (backlog, Planned) | never change the data layout or the upgrade steps without checking her case | |
| The release pipeline's helper actions run on Node.js 20, deprecated on GitHub runners | 2026-08-02 | the @vN bumps land (backlog, Ongoing) | a cosmetic warning in the run log | |
