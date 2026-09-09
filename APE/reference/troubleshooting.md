# Troubleshooting

## `aiw: command not found`[​](#aiw-command-not-found "Direct link to aiw-command-not-found")

The CLI isn't installed. The Onboarding page tells you to run `aiw enroll` without telling you to install it first.

```
npm i -g @bloom-ai-workspace/cli --registry=https://nexus.vinted.net/repository/npm-proxy-web
```

The `--registry` flag matters – the package isn't on the public npm registry. Then check with `aiw --version`.

If npm reports a permissions error, you have a system Node install. Use a version manager rather than `sudo`.

## "Your SSH access hasn't been approved yet"[​](#your-ssh-access-hasnt-been-approved-yet "Direct link to \"Your SSH access hasn't been approved yet\"")

**You don't need to wait for an admin,** even though this message and the badge on the Onboarding page both say so. Approval is automatic and takes about ten seconds.

If it's been longer than a minute:

1. Re-run `aiw enroll`. It's safe to run repeatedly.
2. Or open Onboarding and re-save your key.

Either re-triggers approval. In rare cases the first attempt is lost – re-registering is the fix.

Run `aiw doctor` to see which step is actually failing.

## Nothing loads at all[​](#nothing-loads-at-all "Direct link to Nothing loads at all")

You're probably on the wrong VPN.

Vinted has two, and APE only works on **`backup-vinted-vpn`**. Connected to the other one, the app simply doesn't resolve – no error page, no timeout message, nothing. Switch VPNs and reload.

This affects the preview and the CLI too, so if `aiw` commands are also failing to reach the server, check this first.

## The preview says "refused to connect"[​](#the-preview-says-refused-to-connect "Direct link to The preview says \"refused to connect\"")

Usually the dev server hasn't finished starting. Wait a few seconds and hit reload.

If it persists, the dev server may have crashed – often after a change that doesn't compile. Say so in chat; the agent can read the error and fix it.

## The session has been provisioning for several minutes[​](#the-session-has-been-provisioning-for-several-minutes "Direct link to The session has been provisioning for several minutes")

Normal for a large repo on first run. `marketplace-web` clones and installs from scratch. The line under the spinner is the real setup log, so if it's moving, it's working.

If it hasn't moved in five minutes or so, the session is probably stuck. Delete it and create another.

## The session says failed[​](#the-session-says-failed "Direct link to The session says failed")

Provisioning didn't complete. Click **Retry** – it usually works second time, particularly on the beta projects.

If it fails repeatedly on the same project, that's worth reporting rather than retrying.

## The agent stopped before it finished[​](#the-agent-stopped-before-it-finished "Direct link to The agent stopped before it finished")

If you see a **Continue** pill, the run hit its step limit. Nothing is lost and the work so far is committed. Click Continue.

If it happens repeatedly, break the request into smaller prompts. See [Prompting](/ape-mvp-docs/APE/the-workspace/prompting-the-agent.md).

## The agent says it's done but the preview is broken[​](#the-agent-says-its-done-but-the-preview-is-broken "Direct link to The agent says it's done but the preview is broken")

Tell it. "The preview is blank on /checkout" is enough.

The agent has a screenshot tool that captures the page *and* the browser console errors – that's how it finds problems that don't show up in the terminal, like a component that only throws in the browser.

If it's gone in circles, revert to the last good state rather than layering more instructions on a confused one. See [Files and history](/ape-mvp-docs/APE/the-workspace/files-and-history.md).

## I came back and my session was asleep[​](#i-came-back-and-my-session-was-asleep "Direct link to I came back and my session was asleep")

Expected. Sessions pause after 15 minutes, stop after an hour, and archive after a day.

Opening it wakes it. Archived sessions rebuild from your branch, which takes about as long as the original setup.

**Nothing is lost at any tier.** See [Sessions](/ape-mvp-docs/APE/concepts/sessions.md).

## The preview asks me to sign in[​](#the-preview-asks-me-to-sign-in "Direct link to The preview asks me to sign in")

`svc-shipping-frontend` and `svc-vcarrier-admin-frontend` have their own Okta. Use the overlay to open the sign-in page in a new tab, sign in there, come back, and confirm.

Signing into APE doesn't sign you into the application APE is running.

## My teammate can see the prototype but can't prompt[​](#my-teammate-can-see-the-prototype-but-cant-prompt "Direct link to My teammate can see the prototype but can't prompt")

They opened a share link, which is read-only by design. They can browse and comment but not change anything.

Add them as a collaborator from the Share dialog. See [Sharing](/ape-mvp-docs/APE/working-with-others/sharing.md).

## Publishing failed[​](#publishing-failed "Direct link to Publishing failed")

The dialog shows the end of the build log.

Most failures are things that work in the dev server but not in a production build. Paste the error into chat, let the agent fix it, then retry.

## I can't create a session[​](#i-cant-create-a-session "Direct link to I can't create a session")

Two possibilities:

* **Capacity.** Sessions run on shared infrastructure. Delete finished sessions to free space – active ones are what's in your way, not sleeping ones.
* **Setup isn't finished.** See the SSH approval entry above.

## I lost edits in the Code tab[​](#i-lost-edits-in-the-code-tab "Direct link to I lost edits in the Code tab")

Closing a tab with unsaved changes doesn't warn you. Use ⌘S.

Once saved, autosave commits within 30 seconds, so saved work is recoverable from [history](/ape-mvp-docs/APE/the-workspace/files-and-history.md) even if you never do anything else.

## Cursor can't connect over SSH[​](#cursor-cant-connect-over-ssh "Direct link to Cursor can't connect over SSH")

Covered in [CLI and SSH onboarding](/ape-mvp-docs/APE/reference/cli-and-ssh-onboarding.md) – the usual causes are the VPN being off, a stale entry in `~/.ssh/config` from a deleted session, or the container still booting.

`aiw connect` is safe to re-run and fixes most of these.

## Something else[​](#something-else "Direct link to Something else")

Run `aiw doctor` first – it checks connectivity, auth, your key, approval status, your editor, and your GitHub token, and tells you which one is wrong.
