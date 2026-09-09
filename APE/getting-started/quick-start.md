# Quick start

This walks through one complete loop: make a session, change something, point at what's wrong, and share it. We'll use a blank template, so nothing here depends on a large repo booting.

This assumes you've been through [Getting access](/ape-mvp-docs/APE/getting-started/getting-access.md). If you haven't, do that first – it takes about a minute.

## 1. Start a session[​](#1-start-a-session "Direct link to 1. Start a session")

On the home screen, click **Explore**.

That creates a session on the blank template and opens it. No project picker, no configuration – it's the fastest way in.

## 2. Wait for it to boot[​](#2-wait-for-it-to-boot "Direct link to 2. Wait for it to boot")

The right pane shows a splash while the session comes up, moving through **provisioning** → **installing** → **running**. The line under the spinner tells you what's happening.

Templates use a pre-built image, so this takes about five to ten seconds. A real repo like `marketplace-web` takes a couple of minutes the first time.

When the preview appears, the app is running.

## 3. Ask for something[​](#3-ask-for-something "Direct link to 3. Ask for something")

Type into the chat on the left and press Enter.

Be specific about what you want and where it goes:

> Add a pricing page at /pricing with three tiers – Free, Plus, and Pro. Use cards in a row, with the middle one highlighted.

Rather than:

> make a pricing page

You'll see the agent's steps appear as it works – reading files, writing them, running checks. When it finishes, the preview refreshes and the change is already committed.

## 4. Point at what's wrong[​](#4-point-at-whats-wrong "Direct link to 4. Point at what's wrong")

This is the part worth learning early.

Find the floating toolbar over the preview and turn on **Inspect**. Hover the preview – each element highlights and shows what it is and which file it comes from. Click the middle pricing card.

Now type:

> make this one taller and add more space around the price

The agent knows which element you mean, because you told it by clicking rather than describing. It goes straight to the right file.

[Pointing at things](/ape-mvp-docs/APE/the-workspace/pointing-at-things.md) covers the rest.

## 5. Check it on mobile[​](#5-check-it-on-mobile "Direct link to 5. Check it on mobile")

In the preview's URL bar there's a device switcher – desktop, tablet, mobile. Switch to mobile.

This genuinely re-renders the app at 390 × 844 rather than scaling a picture, so what you see is what the app does at that width. If it breaks, say so in chat.

## 6. Go back if you need to[​](#6-go-back-if-you-need-to "Direct link to 6. Go back if you need to")

Every prompt you sent is a commit. On any change card in the chat, click **Details** to open the history view, then **Preview** to see the app as it was at that point, or revert to it.

Nothing you do is one-way. See [How your work is saved](/ape-mvp-docs/APE/concepts/how-your-work-is-saved.md).

## 7. Share it[​](#7-share-it "Direct link to 7. Share it")

Click **Share** in the header to copy a link. Anyone on `backup-vinted-vpn` who opens it gets a read-only view – they can click through the prototype and leave comments pinned to specific elements, but they can't change anything.

To let someone drive the agent too, invite them as a collaborator from the same dialog.

## Where to go from here[​](#where-to-go-from-here "Direct link to Where to go from here")

* Prototyping on a real Vinted repo instead of a template → [Templates and projects](/ape-mvp-docs/APE/concepts/templates-and-projects.md)
* Getting better results out of the agent → [Prompting](/ape-mvp-docs/APE/the-workspace/prompting-the-agent.md)
* Putting it on a URL you can send to anyone → [Publishing](/ape-mvp-docs/APE/shipping/publishing.md)
* Turning it into a pull request → [Pull requests](/ape-mvp-docs/APE/shipping/pull-requests.md)
