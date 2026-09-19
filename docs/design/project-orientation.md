# Random Creation — Project Orientation

What is true about the project now, for a session about to design or build anything: what it is and for whom, the stance the work takes, its environment, its scale. `CLAUDE.md` holds the routes and the always-on rules; this record holds the ground they stand on. History stays in the changelog; a date appears only where the date is the authority. Seeded by the setup's interview, the rest filled as the project learns it; an empty section is a question not yet answered, never deleted. Its state is in the index row.

| Section | What it answers |
| --- | --- |
| §1 The application | what the project is, who uses it, what users may and may not change |
| §2 Design philosophy | the stance the work takes |
| §3 Future plans | what is planned beyond the work in flight, with the record that rules each |
| §4 Team and the AI's role | who works on it and how |
| §5 Technical environment | the environment in a sentence; the register holds the facts |
| §6 Scale | the numbers that shape design |
| §7 Standing rulings | decisions about the project's ground, with dates |

## §1 The application

Random Creation is a Windows desktop app that generates random combinations from content the user defines: Collections hold Category Groups, groups hold Categories, categories hold Options, and Generate rolls one option from every enabled category and shows the combination as grouped result cards, numbered by an ever-climbing serial. It is deliberately general purpose, a generator for any kind of random combination, never a creature generator, whatever its first working title said. It is a personal creative tool, not a commercial product: the developer uses it, one live user runs it, and a small pool is testing it. Users own all their content, may hand-edit their categories.json, and may install or run portable; the program files beside the exe are the app's own and are replaced at every release.

## §2 Design philosophy

## §3 Future plans

## §4 Team and the AI's role

## §5 Technical environment

A C# / WPF app on .NET 8 (Windows) with no NuGet packages, built from one Visual Studio solution with the command-line .NET SDK, kept in git on a public all-rights-reserved GitHub repository, and released by GitHub Actions from a pushed tag as a portable zip and an Inno Setup installer, with a GitHub Pages product page as its front door. The facts are in the environment register, `docs/environment.md`; nothing from it is restated here.

## §6 Scale

## §7 Standing rulings
