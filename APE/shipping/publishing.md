# Publishing

Publishing builds a production version of your prototype and serves it at its own URL.

**Templates only.** Real Vinted repos can't be published – those ship through [pull requests](/ape-mvp-docs/APE/shipping/pull-requests.md).

## Why publish[​](#why-publish "Direct link to Why publish")

A published prototype is a link. It works for anyone, on any device, without a VPN, without a Vinted account, and without APE.

That makes it right for user testing, a link in a doc, a stakeholder who won't install anything, or anything you need to still work in three weeks.

It also runs in its own container, so it stays up when your editing session goes to sleep. You can stop working on it and the link keeps working.

## Publishing[​](#publishing-1 "Direct link to Publishing")

**Advanced → Publish.**

You'll see a warning about the URL being public, an optional password field, and a checkbox to acknowledge. Tick it and publish.

The build takes a minute or two – **queued**, then **building**, then **live** with the URL and a copy button.

## Password protection[​](#password-protection "Direct link to Password protection")

**The URL is public to anyone who has it.** There's no VPN check and no sign-in. Anyone who receives the link, or forwards it, can open it.

**If your prototype contains anything sensitive – real customer data, unreleased pricing, internal metrics, anything not already public – set a password before you share it.**

Set it in the field when you publish, or add one afterwards without rebuilding. Then share the password separately from the link.

You can change or remove a password at any time from the same dialog. Removing one asks you to confirm, because it makes the prototype open to anyone with the URL.

## Keeping it current[​](#keeping-it-current "Direct link to Keeping it current")

Publishing takes a snapshot. Changes you make afterwards don't appear on the live URL until you rebuild.

When the session has moved on, the publish dialog shows an **outdated** notice. **Publish again** rebuilds from your current state, at the same URL. The link you already sent doesn't change.

## If a build fails[​](#if-a-build-fails "Direct link to If a build fails")

The dialog switches to a failed state with the end of the build log.

Most failures are build errors – something that works in the dev server but not in a production build. Paste the error into chat; the agent can usually fix it. Then retry.

## Unpublishing[​](#unpublishing "Direct link to Unpublishing")

**Unpublish** takes the site down and frees its container. The URL stops working immediately.

Your session is untouched. You can publish again later, though the URL may differ.

## Limits[​](#limits "Direct link to Limits")

* Templates only.
* One published site per session.
* Rebuilds take about as long as the first build.
* A build that runs too long is cut off, usually a sign the build is stuck rather than slow.
