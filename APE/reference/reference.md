# Reference

## Session statuses[​](#session-statuses "Direct link to Session statuses")

| Status         | Meaning                              | Can you prompt?   |
| -------------- | ------------------------------------ | ----------------- |
| `pending`      | Queued, waiting for capacity         | No                |
| `provisioning` | Container being created, repo cloned | No                |
| `installing`   | Dependencies installing              | No                |
| `running`      | Ready                                | Yes               |
| `sleeping`     | Idle – wakes when opened             | Yes, after waking |
| `failed`       | Setup didn't complete                | No – retry first  |
| `stopped`      | Stopped manually                     | No – reopen first |
| `completed`    | Pull request merged, read-only       | No                |

## Sleep tiers[​](#sleep-tiers "Direct link to Sleep tiers")

| After idle | State    | What happens                   | Coming back         |
| ---------- | -------- | ------------------------------ | ------------------- |
| 15 minutes | paused   | App frozen in memory           | Instant             |
| 1 hour     | stopped  | Memory freed, files kept       | Seconds             |
| 24 hours   | archived | Container removed, branch kept | Rebuild from branch |

A session won't sleep while an agent run is in progress or an SSH connection is open. Sessions are never deleted automatically.

## Limits[​](#limits "Direct link to Limits")

|                                      | Limit                                                                 |
| ------------------------------------ | --------------------------------------------------------------------- |
| Images per chat message              | 4                                                                     |
| Total message size, including images | 20 MB                                                                 |
| Comment screenshot                   | \~2.5 MB                                                              |
| File size in the Code editor         | 1 MB                                                                  |
| Steps per agent run                  | \~80                                                                  |
| Active sessions                      | Capped by available memory – you'll get a capacity error, not a queue |

## Costs[​](#costs "Direct link to Costs")

Hover any agent message for its token usage and an estimate.

| Term        | Meaning                                                                       |
| ----------- | ----------------------------------------------------------------------------- |
| Input       | Tokens the agent read – your prompt, plus files                               |
| Output      | Tokens it wrote                                                               |
| Cache write | Reading part of the codebase into working memory. Costs more than plain input |
| Cache read  | Reusing that memory on later turns. Costs much less                           |

This is why the first prompt in a session looks expensive next to the ones after it. The agent pays once to load context and reuses it. Long sessions get cheaper per prompt.

Estimates use public list pricing. They're for orientation, not accounting.

## `aiw` commands[​](#aiw-commands "Direct link to aiw-commands")

| Command                    | What it does                                        |
| -------------------------- | --------------------------------------------------- |
| `aiw enroll`               | One-time setup – sign in, create a key, register it |
| `aiw create [template]`    | Create a session and open it in Cursor              |
| `aiw connect [session-id]` | Configure SSH for an existing session               |
| `aiw list` / `aiw ls`      | List your sessions                                  |
| `aiw doctor`               | Diagnose setup problems                             |
| `aiw outdated`             | Check whether your CLI is behind                    |
| `aiw update`               | Install the latest CLI                              |
| `aiw logout`               | Clear your stored token                             |
| `aiw help [command]`       | Full help, or flags for one command                 |
| `aiw --version`            | Print the version                                   |

Session IDs accept the 8-character short form from `aiw list`.

Useful flags on `create` and `connect`:

| Flag             | Effect                            |
| ---------------- | --------------------------------- |
| `--open`         | Open Cursor and a browser preview |
| `--no-open`      | Don't open anything               |
| `--web`          | Open the session in the browser   |
| `--preview`      | Open just the preview             |
| `--name <label>` | Name the session on creation      |

Install:

```
npm i -g @bloom-ai-workspace/cli --registry=https://nexus.vinted.net/repository/npm-proxy-web
```

Full CLI and SSH documentation: [CLI and SSH onboarding](/ape-mvp-docs/APE/reference/cli-and-ssh-onboarding.md).

## URLs[​](#urls "Direct link to URLs")

|                     | Pattern                                                 |
| ------------------- | ------------------------------------------------------- |
| Session             | `<app>/sessions/<session-id>`                           |
| Read-only share     | `<app>/sessions/<session-id>?viewer=1`                  |
| Share on a route    | `<app>/sessions/<session-id>?viewer=1&path=/some/route` |
| Published prototype | Its own public URL, shown in the publish dialog         |

## Projects[​](#projects "Direct link to Projects")

| Project                        | Notes                                             |
| ------------------------------ | ------------------------------------------------- |
| `marketplace-web`              | Largest, slowest to provision. SCSS, not Tailwind |
| `vintedgo-ui`                  | –                                                 |
| `recommerce-ui`                | Points at the recommerce sandbox API              |
| `svc-shipping-frontend`        | Beta. Separate Okta sign-in inside the preview    |
| `svc-vcarrier-admin-frontend`  | Beta. Separate Okta sign-in inside the preview    |
| `bloom-web-ui-mobile-template` | Beta. Real repo that can also be published        |

## Templates[​](#templates "Direct link to Templates")

`blank-template` · `vinted-app` · `agentic-vinted-app` · `marketplace-web-template` · `bloom-design-system` · `bloom-internal-tools` · `vinted-go-bloom` · `vinted-go-mobile` · `vintedgo-internal-tools` · `web-admin`

See [Templates and projects](/ape-mvp-docs/APE/concepts/templates-and-projects.md).
