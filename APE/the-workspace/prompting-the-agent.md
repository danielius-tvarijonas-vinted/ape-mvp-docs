# Prompting the agent

The agent is Claude Code, running inside your session's container. It can read and write files, search the codebase, run commands, and check its own work against the running app.

What you get out of it depends mostly on how you ask.

## Writing a good prompt[​](#writing-a-good-prompt "Direct link to Writing a good prompt")

**Name the thing and the place.**

> Add a "Save for later" button to the item page, next to the Buy button.

Not:

> add a save button

**Say what shouldn't change.** The agent errs toward minimal changes, but being explicit removes any doubt.

> Change only the spacing. Don't touch the copy or the colours.

**One outcome per prompt.** Three unrelated changes in one message means three chances for one of them to be misread, and a single commit you can't partially undo. Send them separately.

**Point instead of describing** where you can. Clicking an element with Inspect is worth more than a paragraph of description – see [Pointing at things](/ape-mvp-docs/APE/the-workspace/pointing-at-things.md).

**Say what's wrong, not how to fix it,** unless you know the codebase. "The cards are uneven heights on mobile" gets a better result than a guess at the CSS.

## Big asks get planned first[​](#big-asks-get-planned-first "Direct link to Big asks get planned first")

For anything spanning several screens or a whole redesign, the agent won't just start typing. It writes a numbered plan – three to six slices – and asks you to confirm the scope before it begins.

Then it does **one slice per turn**, commits, and stops. You say continue, and it takes the next one.

This is deliberate. It gives you a checkpoint between each piece, so a wrong direction costs you one slice rather than an hour. If the plan is wrong, say so before confirming – that's what the confirmation is for.

## The agent asks you questions[​](#the-agent-asks-you-questions "Direct link to The agent asks you questions")

When something is genuinely ambiguous, the agent stops and asks, as a card in the chat with options to pick from.

The run is paused until you answer. Pick an option, or type a reply – while a question is open, what you type goes to the waiting agent rather than starting a new run.

If you refresh the page mid-question, the card is still there when you come back.

## Runs have a step budget[​](#runs-have-a-step-budget "Direct link to Runs have a step budget")

A run gets roughly 80 steps. Reading a file, writing one, running a command – each counts.

A run that hits the limit stops cleanly and shows a **Continue** pill. That's not an error and nothing is lost; the work so far is committed. Click Continue, or type your own instruction to redirect.

If you hit it often, your prompts are probably too big. Let the planning behaviour do its job rather than asking for everything at once.

## Sending while it's working[​](#sending-while-its-working "Direct link to Sending while it's working")

You don't have to wait. Anything you send while a run is going joins a **queue** and runs in order when the current one finishes.

The queue shows above the composer. You can remove individual items, or pause it if you want to see how the current change lands before the next one starts.

**Stop** aborts the current run. Work already committed stays.

## Attaching images[​](#attaching-images "Direct link to Attaching images")

Paste or drag up to four images per message. Screenshots, Figma exports, a photo of a whiteboard.

You can also capture straight from the preview – see [Pointing at things](/ape-mvp-docs/APE/the-workspace/pointing-at-things.md).

## Talking to people instead[​](#talking-to-people-instead "Direct link to Talking to people instead")

Start a message with `@` and someone's name and it becomes a **note** – it goes to that person, not the agent, and doesn't start a run. See [Comments and notes](/ape-mvp-docs/APE/working-with-others/comments-and-notes.md).

So Enter does one of three things depending on context: send a prompt, answer a pending question, or post a note. The composer changes colour to tell you which.

## Cost[​](#cost "Direct link to Cost")

Hover any of the agent's messages to see the tokens it used and a rough cost.

The numbers include *cache* tokens, which is why a first message in a session can look expensive relative to the ones after it – the agent is reading the codebase into its working memory once and reusing it. Long sessions get cheaper per prompt, not more expensive.

The figures are estimates against public list pricing. See [Reference](/ape-mvp-docs/APE/reference/reference.md).

## When it gets stuck[​](#when-it-gets-stuck "Direct link to When it gets stuck")

* **It changed the wrong thing.** Revert to the previous prompt rather than asking it to undo. See [Files and history](/ape-mvp-docs/APE/the-workspace/files-and-history.md).
* **It says it's done but the preview is broken.** Tell it. It has a screenshot tool that sees browser console errors, which is how it finds problems that don't appear in the terminal.
* **It's going in circles.** Stop the run, revert to the last good state, and re-prompt with more constraint. Continuing to add instructions on top of a confused state rarely recovers.
