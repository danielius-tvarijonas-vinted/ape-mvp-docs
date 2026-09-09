# Files and history

Three ways to look at your session as code rather than as a running app.

## Files[​](#files "Direct link to Files")

The **Files** tab lists every file that changed in this session, with its diff.

Each file is marked added, modified, or deleted. Click one to see the diff; click it again to collapse.

This covers changes from every source – the agent, your own edits in the Code tab, work you did over SSH, and autosave. It's the same view a reviewer will see on the pull request, so it's worth a look before you open one.

The count on the tab tells you how many files are touched, which is a decent signal on its own. If a "change the button colour" prompt touched eleven files, something went wider than you meant.

## Code[​](#code "Direct link to Code")

The **Code** tab is a real editor – file tree on the left, tabs across the top, syntax highlighting, ⌘S to save.

Use it when describing a fix takes longer than making it. A typo, a hex value, a stray margin.

**What it can't do:**

* Create, rename, or delete files
* Find and replace across files
* Search within a file

For any of that, use SSH – see [CLI and SSH onboarding](/ape-mvp-docs/APE/reference/cli-and-ssh-onboarding.md).

Two things to watch:

* **Closing a tab with unsaved edits doesn't warn you.** Save with ⌘S.
* Saved changes are committed by autosave within 30 seconds, so they're safe once saved even if you don't do anything else.

There's also a **Download codebase** button here, which gives you the whole workspace as a `.tar.gz`.

## History[​](#history "Direct link to History")

Every change is its own commit, so your session has a real history you can move through.

On any change card in the chat, click **Details**. The chat switches to the history view: every commit, newest first, grouped by day.

From an entry you can:

* **Expand it** to see which files changed.
* **Open a file** at that point.
* **Preview** – the right pane checks out that version and shows you the app as it was. An amber banner appears; "Back to latest" returns you.
* **Undo** – revert to that point.

Reverted entries stay in the list, struck through, so the history is a record of what happened rather than a tidied version of it.

### Reverting[​](#reverting "Direct link to Reverting")

Reverting creates a new commit that undoes the change. It doesn't erase anything, so:

* You can revert a revert.
* Nothing is lost even if you revert too far.
* The history stays honest.

If you prompt the agent while previewing an old version, APE returns you to the latest state first. You can't accidentally build on a detached checkpoint.

## What this is for[​](#what-this-is-for "Direct link to What this is for")

The practical upshot: you can try things. A direction that turns out wrong costs one click, not an afternoon.

The background on how this works is in [How your work is saved](/ape-mvp-docs/APE/concepts/how-your-work-is-saved.md).
