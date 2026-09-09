# Templates and projects

There are two kinds of starting point, and the difference decides what you can do at the end.

|                             | Templates                                  | Projects                   |
| --------------------------- | ------------------------------------------ | -------------------------- |
| Based on                    | A self-contained scaffold                  | A real Vinted repo         |
| Starts in                   | Seconds                                    | Up to a couple of minutes  |
| Can open a pull request     | No                                         | Yes                        |
| Can publish to a public URL | Yes                                        | No                         |
| Good for                    | Concepts, explorations, things you'll show | Changes you intend to ship |

## Templates[​](#templates "Direct link to Templates")

Templates have no upstream repository. Nothing you do in one can affect a real codebase, which makes them the right place to try something ugly.

| Template                   | What it's for                                                                            |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| `blank-template`           | An empty canvas. What **Explore** gives you.                                             |
| `vinted-app`               | The consumer app shell – home, search, sell, inbox, sign-up.                             |
| `agentic-vinted-app`       | A newer app shell including catalog, chat, checkout, profile.                            |
| `marketplace-web-template` | A marketplace scaffold with the fullest route set – items, orders, settings, playground. |
| `bloom-design-system`      | The Bloom design system, with docs.                                                      |
| `bloom-internal-tools`     | Internal tooling patterns.                                                               |
| `vinted-go-bloom`          | Vinted Go's design system.                                                               |
| `vinted-go-mobile`         | Vinted Go mobile patterns.                                                               |
| `vintedgo-internal-tools`  | Vinted Go internal tooling patterns.                                                     |
| `web-admin`                | Admin interface patterns.                                                                |

Because a template has no upstream, its output is a link rather than a pull request. See [Publishing](/ape-mvp-docs/APE/shipping/publishing.md).

## Projects[​](#projects "Direct link to Projects")

Projects are real Vinted repositories. Your session branches off the repo's actual default branch, and the changes you make can become a pull request.

| Project                        | Worth knowing                                                                                                                                |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `marketplace-web`              | The largest. Slowest to provision. Styled with SCSS, not Tailwind – the agent knows this, but it's worth knowing too when you write prompts. |
| `vintedgo-ui`                  | –                                                                                                                                            |
| `recommerce-ui`                | Points at the recommerce sandbox API.                                                                                                        |
| `svc-shipping-frontend`        | Beta. Needs a separate Okta sign-in **inside** the preview.                                                                                  |
| `svc-vcarrier-admin-frontend`  | Beta. Needs a separate Okta sign-in **inside** the preview.                                                                                  |
| `bloom-web-ui-mobile-template` | Beta. Unusual – it's a real repo that can also be published.                                                                                 |

**Beta** means the setup is newer and more likely to fail on provision. Retrying usually works.

The two that require an in-preview sign-in will show a sign-in overlay on the preview when you first open a protected route. That's the app's own Okta, not APE's – sign in there and carry on.

### Choosing a base branch[​](#choosing-a-base-branch "Direct link to Choosing a base branch")

When you create a session on a project, you can pick which branch it starts from. The default branch is at the top and is what you want most of the time. Branch off something else when you're building on work that hasn't merged yet.

## Personal templates[​](#personal-templates "Direct link to Personal templates")

Any session can become a template. Open the project menu in the header and choose to use it as a template – it then shows up under **Templates** for your teammates, alongside the official ones.

This is the design system workflow. Someone maintains a well-built starting point, other people spin variations off it, and improvements travel in both directions:

* **Merge to template** – you built something in a variation that belongs in the template. This previews the change first and tells you whether it applies cleanly.
* **Sync from template** – the template has moved on and you want those updates in your variation.

Both live in the session's family switcher rather than the Advanced menu.

If a merge conflicts, you'll be told which files. In some cases APE can resolve it by having the agent finish the merge in the template session.
