# sapphire
Sapphire Novel Engine
A small JavaScript framework for branching text stories — passages, links, and variables, with an in-browser editor and no build step.
It works like Twine: you write short chunks of story text ("passages"), link them together with [[choice->target]], and the engine handles the branching, state, and rendering. Unlike Twine, it's a single HTML file you can read, edit, and hand to anyone — no install, no app.
What's in the file
story-loom.html (rename it however you like) contains three things in one place:
The engine — a small SapphireNovelEngine.Story class that parses passage text, follows links, and tracks variables. This is the reusable "framework" part.
An editor — a plain, wiki-style interface for writing and organizing passages, with an Edit tab and a Play tab.
A demo story — four linked passages showing links and variables in action, so you can see it working the moment you open the file.
Quick start
Open the file in a browser (double-click it, or host it anywhere as a static page).
Click around the demo story in the Play tab to see how it works.
Switch to Edit and start replacing the demo passages with your own.
When you're ready to share it, click Export standalone HTML to download a clean, read-only player containing just your story.
See USAGE.md for the full guide to writing passages, links, and variables.
