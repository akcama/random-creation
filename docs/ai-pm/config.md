# AI PM — Project Config

THIS PROJECT'S OWN FILE, settings only. The AI maintains it at close-out like any other memory; no release or upgrade ever replaces it, and none changes a value the developer chose. Which settings exist is the method's; what they are set to is the developer's. The settings block first, one `* Name: value` line each; then the definitions, one `* NAME — ...` line each; the release lint refuses a release when a setting has no definition. Everything that is not a setting lives elsewhere: where things are in `docs/index.md`, the story in the changelog, to-dos in the backlog.

* Feedback Pass: on
* Push: follow remote
* Allowed write locations: none
* Usage: on

The settings:

* FEEDBACK PASS — on | off. The one auto-running behaviour: a self-check after each full close-out that may suggest a feedback report; it observes and notifies, never acts. Off stops the auto-notice; `/feedback-pass` still works by hand.
* PUSH — follow remote | on (<remote>) | off. Governs every commit the AI makes. "Follow remote": no git remote → nothing pushes; a remote → push immediately after each commit. "Off" is the explicit opt-out. A refused push is merged only when the merge touches nothing this session changed; otherwise it is reported and never resolved alone.
* ALLOWED WRITE LOCATIONS — none | a list of paths. Adds to what the close-out's outside-the-project check treats as in bounds. Listing a location silences ordinary writes to it, nothing else: a change to what the AI is permitted to do in future sessions always flags. "None" means the project folder, the session's scratch area, the platform's own config folder, the shelf's inbox and any registered companion alone.
* USAGE — on | off. On: the close-out writes this session's usage row and detail and prints the usage line. Off: no row, no line; the dashboard's usage tabs stay empty; nothing else changes.
