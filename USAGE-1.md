# Usage guide

## The two tabs

- **Edit** — where you write. A list of passages on the left, an editor for the selected one on the right.
- **Play** — runs your story from the start passage, so you can test it as you go.

Switching to Play always rebuilds the story from your latest edits, so you're never testing stale text.

## Passages

A passage is one chunk of story — a scene, a page, a moment. Every passage has:

| Field | What it is |
|---|---|
| **ID** | A short internal name with no spaces (e.g. `forest`, `Chapter2Intro`). Used to link passages together. |
| **Text** | What the reader sees, written as plain prose in the textarea. |
| **Choices** | A list of ways the reader can leave this passage, each pointing to another passage. |

Blank lines between lines of text start a new paragraph. There's no other text formatting (no bold, italics, headers) — this keeps stories portable and the editor simple.

### Creating and editing passages

- **+ New passage** — adds a new, empty passage and selects it.
- Click any passage name in the left list to open it for editing.
- Changes to the text save automatically as you type.
- Changing the **Passage ID** field renames it everywhere it's used.
- **Delete passage** — removes the currently open passage. You can't delete the last remaining one.
- **Set as start** — marks the currently open passage as where the story begins when played. The start passage is marked `(start)` in the list.

> [!WARNING]
> Deleting a passage does **not** automatically remove choices in *other* passages that pointed to it. Those choices will show a warning (see [Choices](#choices) below) until you fix or remove them.

## Choices

Choices are how the reader moves from one passage to another — no typed syntax involved.

For the currently open passage:

1. Click **+ Add choice**.
2. Type the label the reader will see (e.g. `Take the left trail`).
3. Pick the destination passage from the dropdown next to it.
4. Repeat for as many choices as this passage needs, or leave it with zero choices for a dead end or an ending.

Each choice becomes one clickable line in Play mode. Click **✕ Remove** to delete a choice.

If a choice's dropdown points to a passage that no longer exists (because it was renamed or deleted), you'll see:

```text
⚠ Points to passage(s) that no longer exist: oldPassageName
```

Fix this by either picking a valid passage from the dropdown or removing the choice.

## Variables

Variables let a passage remember something and other passages react to it — a name, a choice made earlier, a score.

**Set a variable** (invisible in the rendered text):

```text
{{set:lantern=lit}}
```

**Show a variable's value:**

```text
The lantern is {{get:lantern}}.
```

Use the **+ Insert "set variable"** / **+ Insert "show variable"** buttons above the textarea to drop these in at your cursor instead of typing the braces yourself.

### Branching with variables

Sapphire CompileBox doesn't have `if/else` — branching happens by routing the reader to a different passage depending on the choice they made, and using variables just to remember *how* they got there:

```text
Passage: start
  Text: You see a locked door.
  Choices: "Search for a key" → search
           "Force it open"    → force

Passage: search
  Text: {{set:method=search}}
        You find a key under the mat.
  Choices: "Open the door" → reveal

Passage: force
  Text: {{set:method=force}}
        You kick it in. That'll leave a mark.
  Choices: "Go through" → reveal

Passage: reveal
  Text: However you got in ({{get:method}}), the room is empty.
```

Variables persist for the rest of the playthrough and reset when **restart** is clicked (by the reader, or by you in Play mode).

## Testing your story

Switch to the **Play** tab any time. At the bottom of each passage you'll see:

- which passage you're currently on
- the current value of every variable set so far

This debug line is only shown in the editor's Play mode — it does **not** appear in a compiled game.

Click **↺ restart** to reset variables and jump back to the start passage.

## Compiling

When your story is ready to share, click **▶ Compile Game** (on the Edit tab). This downloads `game.html`, containing:

- just your passages, choices, and variables — no editor UI, no editing code at all
- the same choice and variable behavior as Play mode
- a restart button

`game.html` is what you'd post publicly, email, or upload to a game page. It's a separate, plain file from the editor — safe to share without exposing your editing tools.

You can compile as many times as you like while you keep writing — each click produces a fresh `game.html` from whatever is currently in the editor.

## Tips

- [ ] Keep passage IDs short and consistent (`forest_entrance`, not `The Entrance To The Dark Forest`) — you'll be picking them from dropdowns often.
- [ ] Use **Set as start** early, so Play mode always opens where you expect.
- [ ] Test with **Play** frequently rather than writing many passages before checking any choices.
- [ ] There's no autosave to disk — your story only lives in the browser tab until you **Compile**. Compile often, especially before closing the tab.
