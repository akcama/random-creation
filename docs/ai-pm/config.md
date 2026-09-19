# AI PM — Project Config

THIS PROJECT'S OWN FILE, settings only. The AI maintains it at close-out like any other memory; no release or upgrade ever replaces it, and none changes a value the developer chose. Which settings exist is the method's; what they are set to is the developer's. The settings block first, one `* Name: value` line each; then the definitions, one `* NAME — ...` line each; the release lint refuses a release when a setting has no definition. Everything that is not a setting lives elsewhere: where things are in `docs/index.md`, the story in the changelog, to-dos in the backlog.

* Project type: software build
* Handoff: on
* Feedback Pass: on
* Push: follow remote
* Allowed write locations: none
* Usage: on
* Dashboard: on
* Started Ceiling: 3

The settings:

* PROJECT TYPE — software build | knowledge. How AI PM itself runs, chosen first at the setup's door, before anything the type decides. SOFTWARE BUILD: a foundation from the company defaults' menu, a source tree, the handoff on. KNOWLEDGE: a project that is an assistant that knows everything about its subject, files what it is handed, plans, and answers; no foundation, a product folder of records beside `docs/`, the handoff off. A closed list: a type exists only when it changes how AI PM runs; what a product is built with is the foundation, never a type.
* HANDOFF — on | off. On: `docs/handoff.md` is rewritten at every close-out and read at every session start. Off: no file. The close-out skips it; the opener's Last session reads the changelog's newest entry and Today takes the session's first prompt, or asks "what are we doing today?" when the session opens with a hello; standing conditions live in the environment register's STANDING CONDITIONS table; the index check's handoff ceiling does not run. On is the software build's default, off the knowledge type's; either may change it.
* FEEDBACK PASS — on | off. The one auto-running behaviour: a self-check after each close-out, either mode, that may suggest a feedback report; it observes and notifies, never acts. Off stops the auto-notice; `/ai-pm-self-check` runs the audit by hand and `/ai-pm-feedback` writes a report on request.
* PUSH — follow remote | on (<remote>) | off. Governs every commit the AI makes. "Follow remote": no git remote → nothing pushes; a remote → push immediately after each commit. "Off" is the explicit opt-out. A refused push is merged only when the merge touches nothing this session changed; otherwise it is reported and never resolved alone.
* ALLOWED WRITE LOCATIONS — none | a list of paths. Adds to what the close-out's outside-the-project check treats as in bounds. Listing a location silences ordinary writes to it, nothing else: a change to what the AI is permitted to do in future sessions always flags. "None" means the project folder, the session's scratch area, the platform's own config folder, the shelf's inbox and each registered tool's clone, for the writes its registered steps direct, alone.
* USAGE — on | off. On: the close-out writes this session's usage row and detail and prints the usage line. Off: no row, no line, no rebuild; the dashboard's usage tabs stay empty; nothing else changes.
* DASHBOARD — on | off. On: once the dashboard page exists, the usage script rebuilds it in place after each close-out's row lands, no browser opened, no model tokens spent. Off: no rebuild at close-out; the dashboard command still builds and opens the page by hand.
* STARTED CEILING — a number, default 3. How many items one developer may have started at once. The close-out warns when a move to started would pass it; the opener flags a developer over it. Never blocks: a warning to finish or drop something before starting more.
