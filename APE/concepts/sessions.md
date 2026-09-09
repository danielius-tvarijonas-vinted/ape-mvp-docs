# Sessions

A session is one prototype. Creating one gives you three things at once:

* A **container** – a private machine running the application and its dev server.
* A **branch** – `prototype/session-…`, where every change is committed.
* An **agent** – Claude Code, running inside that container, doing the editing.

Everything else in APE is a view onto one of those three.

## Creating one[​](#creating-one "Direct link to Creating one")

From **Templates** or **Projects**, pick something and click **Create session**. On a real repo you can also choose which branch to start from; it defaults to the repo's default branch.

**Explore** on the home screen skips the picker and gives you a blank template immediately.

You can also duplicate an existing session from its menu. That forks it at its current state, useful for trying two directions from the same starting point.

## Statuses[​](#statuses "Direct link to Statuses")

| Status         | What it means                                                |
| -------------- | ------------------------------------------------------------ |
| `pending`      | Queued, waiting for capacity.                                |
| `provisioning` | The container is being created and the repo cloned.          |
| `installing`   | Dependencies are installing. Skipped on pre-built templates. |
| `running`      | Ready. Preview live, agent available.                        |
| `sleeping`     | Idle. Wakes when you open it. See below.                     |
| `failed`       | Something went wrong during setup. There's a Retry button.   |
| `stopped`      | You stopped it manually.                                     |
| `completed`    | The pull request merged. The session is now read-only.       |

The line under the splash during provisioning is the real setup log, so if it sits on "Installing dependencies" for a while, that's genuinely what it's doing.

## Sleep[​](#sleep "Direct link to Sleep")

Containers are expensive to keep running, so idle sessions wind down in three stages. **Your work is never affected by any of them** – only how long it takes to come back.

| After idle | State    | What happens                     | Coming back takes          |
| ---------- | -------- | -------------------------------- | -------------------------- |
| 15 minutes | paused   | The app is frozen in memory      | Instant                    |
| 1 hour     | stopped  | Memory freed, files kept on disk | A few seconds              |
| 24 hours   | archived | Container removed                | A rebuild from your branch |

Archived is the only one you'll really notice. The session rebuilds itself from your branch – same clone, same install as the first time – so a large repo can take a couple of minutes. The preview shows a restore screen with progress while it happens.

Two things stop the clock: a running agent, and an open SSH connection. A session won't sleep out from under work in progress.

**Sessions are never deleted automatically.** Sleep only ever costs you time.

## Ending a session[​](#ending-a-session "Direct link to Ending a session")

* **Stop** shuts the container down without touching anything else. Reopening restarts it.
* **Delete** removes the session and its branch. This is the one irreversible action in APE. If there's anything worth keeping, open a pull request or download the workspace first.
* When a pull request merges, the session becomes **completed** and read-only automatically. The work has landed; the prototype is a record of how it got there.

## Naming[​](#naming "Direct link to Naming")

Sessions get an automatic name from your first prompt. Click it in the header to rename. Worth doing once you have more than a handful – the session switcher and the prototypes list both use it.

## Capacity[​](#capacity "Direct link to Capacity")

Sessions run on shared infrastructure, so there's a ceiling on how many can be live at once. If you hit it, session creation fails with a capacity message rather than queuing forever.

Deleting sessions you've finished with is the fix. Sleeping sessions past the one-hour mark aren't holding memory, so old work isn't what's in your way – active sessions are.
