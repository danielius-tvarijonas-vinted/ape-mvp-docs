# Pull requests

A pull request is the only route from APE into a real codebase. Everything else stays in your session.

**Projects only.** Templates have no upstream repository, so there's nothing to open a PR against – the equivalent for a template is [publishing](/ape-mvp-docs/APE/shipping/publishing.md).

## Before you open one[​](#before-you-open-one "Direct link to Before you open one")

Two things worth doing:

**Look at the Files tab.** It's the same diff a reviewer will see. If the change is wider than you expected, now is the time to narrow it.

**Connect a GitHub token** if you haven't, on the Onboarding page, with the `repo` scope. Without it the PR opens under a shared account rather than your name.

## Opening it[​](#opening-it "Direct link to Opening it")

**Advanced → Pull request → Create pull request.**

APE drafts a title and description from your diff. Read it – it's generated from the changes, so it describes *what* moved, and you usually know *why*, which is what the reviewer wants. Edit before submitting.

Then it opens the PR on the branch your session has been committing to all along:

```
prototype/session-a1b2c3d4e5  →  master
```

It carries an `AI Workspace prototype` label so these are easy to find in a review queue. Other than that it's an ordinary pull request – same reviewers, same checks, same process.

## After it's open[​](#after-its-open "Direct link to After it's open")

The session shows the PR's state in the header, and there's a link to it.

When the PR **merges**, the session becomes **completed** and read-only. The work has landed, and the session stays as a record of how it got there – the prompts, the intermediate steps, the comments. You can still read it; you can't prompt it.

If the PR is **closed** without merging, the session carries on as normal. Keep working and open another.

## If the button is disabled[​](#if-the-button-is-disabled "Direct link to If the button is disabled")

* **It's a template.** No upstream. Publish instead.
* **The project has PRs turned off.** Some do; the reason shows on the button.
* **You're a viewer.** Read-only links can't open PRs. Ask to be added as a collaborator.
* **Nothing has changed yet.** There's no diff to open a PR for.

## What reviewers should know[​](#what-reviewers-should-know "Direct link to What reviewers should know")

A PR from APE is a normal PR, but two things about it are worth saying out loud in the description:

* The commits are granular – one per change, with messages describing intent. The history is readable rather than squashed.
* The prototype it came from is still viewable. Linking the session in the PR description lets a reviewer click through the working thing rather than reading a diff cold.

That combination is most of the argument for prototyping this way: the review starts from something that runs.
