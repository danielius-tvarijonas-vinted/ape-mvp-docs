# Getting access

Setup happens once per machine. Two clicks in the browser, one command in a terminal.

No prior terminal experience needed. This page tells you exactly what to type.

## Before you start[​](#before-you-start "Direct link to Before you start")

### Connect to the right VPN[​](#connect-to-the-right-vpn "Direct link to Connect to the right VPN")

> **Connect to `backup-vinted-vpn`.** Vinted has two VPNs and APE only works on this one. If you're on the other, the app won't load at all – no error, just nothing. This catches most people once.

### Open Terminal[​](#open-terminal "Direct link to Open Terminal")

Terminal is the app where you type commands. You'll use it three times on this page and then probably never again.

**On a Mac:** press `⌘` + `Space`, type `Terminal`, and press Enter. A window opens with a line of text and a blinking cursor. That's it – you're in the right place.

**On Windows:** press the Start button, type `PowerShell`, and open it.

Each command below can be copied and pasted in. Paste it, press Enter, and wait for it to finish before moving on. Some take a minute and print a lot of text along the way – that's normal.

### Check you have Node[​](#check-you-have-node "Direct link to Check you have Node")

Node is the software the APE command-line tool runs on. Most likely you already have it. Paste this and press Enter:

```
node -v
```

**If you see a version number** like `v22.14.0`, you're set. Move on to step 1.

**If you see `command not found`**, or a version lower than `v20`, install it:

1. Go to [nodejs.org/en/download](https://nodejs.org/en/download).
2. Download the version marked **LTS** – that's the stable one.
3. Open the downloaded file and click through the installer, accepting the defaults.
4. **Close Terminal and open it again** – it won't notice the new install otherwise.
5. Run `node -v` once more. You should now see a version number.

## 1. Sign in[​](#1-sign-in "Direct link to 1. Sign in")

Open the app and click **Sign in with Okta SSO**. Your account is created on first sign-in; there's nothing to request. Vinted accounts only.

You'll land on the **Onboarding** page, which is where the next two steps happen.

## 2. Install the CLI[​](#2-install-the-cli "Direct link to 2. Install the CLI")

`aiw` is APE's command-line tool. You need it once, to give your machine a key that identifies you to the workspace.

Back in Terminal, paste this and press Enter. It takes a minute or so and prints a lot of text.

```
npm i -g @bloom-ai-workspace/cli --registry=https://nexus.vinted.net/repository/npm-proxy-web
```

Check it worked:

```
aiw --version
```

That should print a version number. If it says `command not found`, see [Troubleshooting](/ape-mvp-docs/APE/reference/troubleshooting.md).

> The Onboarding page tells you to run `aiw enroll` but doesn't show you this install line first. If you get `command not found`, this is why.

## 3. Run `aiw enroll`[​](#3-run-aiw-enroll "Direct link to 3-run-aiw-enroll")

```
aiw enroll
```

It does three things:

1. **Signs you in.** A browser tab opens showing a short code – check it matches the one in your terminal, then click **Confirm**.
2. **Creates a key for this machine.** If you don't already have one, it runs `ssh-keygen` and asks for an optional passphrase. Pressing Enter twice is fine.
3. **Registers the key** with the workspace and opens your browser back at Onboarding.

Then wait about ten seconds. The page shows a progress bar and unlocks itself.

**You don't need to wait for an admin.** Some copy in the app still says otherwise – "Awaiting admin approval", "wait for an admin to enable it". Ignore it. Approval is automatic.

Once the page says **You're all set**, the whole app is open to you.

## Optional: connect GitHub[​](#optional-connect-github "Direct link to Optional: connect GitHub")

If you want pull requests to open under your own name rather than a shared account, add a GitHub token on the Onboarding page. It needs the `repo` scope.

This is only for PRs. You don't need it to create sessions, prototype, or publish.

## What's next[​](#whats-next "Direct link to What's next")

* **[Quick start](/ape-mvp-docs/APE/getting-started/quick-start.md)** – build something.
* **Engineers:** [CLI and SSH onboarding](/ape-mvp-docs/APE/reference/cli-and-ssh-onboarding.md) covers `aiw create`, `aiw connect`, and working in Cursor over SSH.

If something went wrong, [Troubleshooting](/ape-mvp-docs/APE/reference/troubleshooting.md) covers the two common failures: `command not found`, and the approval not landing.
