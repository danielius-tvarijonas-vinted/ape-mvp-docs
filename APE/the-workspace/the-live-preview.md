# The live preview

The preview is your application running its own dev server inside your session's container. Not a render, not a screenshot, not an approximation.

That means it behaves like the app. Forms submit, routes navigate, state persists, animations run. It also means it can break like the app – if the dev server crashes, the preview goes with it.

## Navigating[​](#navigating "Direct link to Navigating")

**Type a path** in the URL bar and press Enter. Escape reverts what you typed.

**Pick from the route list** using the dropdown. This is populated from the project's known routes, plus any the system finds by scanning the running app.

The path shown updates as you click around inside the preview, so it always reflects where you actually are, including query strings and hashes.

**Open in a new tab** to use the app full-screen, outside the workspace. Handy for testing something fiddly.

## Device sizes[​](#device-sizes "Direct link to Device sizes")

Three widths, from the switcher in the URL bar:

|         | Size           |
| ------- | -------------- |
| Desktop | Fills the pane |
| Tablet  | 768 × 1024     |
| Mobile  | 390 × 844      |

These resize the actual viewport, so the app reflows the way it would on a real device. It's not a scaled-down picture – media queries fire, layouts break properly, and what you see is what you get.

## Reloading[​](#reloading "Direct link to Reloading")

The reload button restarts the preview frame. Use it when the app has got itself into a state, or when you've changed something outside the agent's normal flow.

Note that reloading loses in-app state. If you were four steps into a flow, you'll be back at the start.

The preview also refreshes on its own after the agent finishes a change.

## Sharing what you're looking at[​](#sharing-what-youre-looking-at "Direct link to Sharing what you're looking at")

The copy-link button gives you a URL that opens on the current route, in read-only mode. Send it and the other person lands exactly where you are rather than on the home page.

See [Sharing](/ape-mvp-docs/APE/working-with-others/sharing.md).

## Sign-in overlays[​](#sign-in-overlays "Direct link to Sign-in overlays")

`svc-shipping-frontend` and `svc-vcarrier-admin-frontend` have their own authentication. When you hit a protected route you'll get an overlay offering to open the sign-in page in a new tab.

Sign in there, come back, and click the "I've already signed in" option. This is the application's Okta, not APE's – signing into APE doesn't sign you into the app it's running.

## Splash screens[​](#splash-screens "Direct link to Splash screens")

What you see instead of the app, and what each means:

* **Starting** – the container is up, the dev server is coming up. Usually seconds.
* **Provisioning / installing** – first-time setup. The line underneath is the real log.
* **Restoring** – the session was archived after 24 hours idle and is being rebuilt from your branch. Shows a three-step progress: fetching, installing, starting.
* **Failed** – setup didn't complete. There's a Retry button; it usually works.
* **Completed** – the pull request merged, so the session is read-only now. There's a link to the PR.

## When the preview looks broken[​](#when-the-preview-looks-broken "Direct link to When the preview looks broken")

A blank page or an error overlay usually means the app itself is failing, not APE.

Say so in chat. The agent has a screenshot tool that captures the page *and* the browser console errors, which is how it finds problems that don't show up in the terminal. "The preview is blank on /checkout" is enough to start with.
