# CLI SSH onboarding

For **developers who want to use `aiw` to SSH into a Bloom AI workspace session**.

> New to APE? Start with [Getting access](/ape-mvp-docs/APE/getting-started/getting-access.md) – everyone needs `aiw enroll` once, and this page picks up from there.

Run through this once and `ssh bloom-ai-workspace-<id>` will work from any terminal, Cursor's Remote-SSH will open the workspace at the project root, and Simple Browser will preview the running app.

***

## How the SSH chain works[​](#how-the-ssh-chain-works "Direct link to How the SSH chain works")

The orchestrator runs on an EC2 instance. Each workspace runs as a Docker container on that EC2, with its SSH port mapped to a per-session port on the host's loopback (`127.0.0.1:4001`, `:4003`, …). Container SSH ports are **not exposed to the network** – only the EC2's own `:22` is.

When you connect, your SSH client:

1. Reaches the EC2 (`ubuntu@<ec2>`) on port `22` – the *jump host*.
2. From there, opens a TCP tunnel to `127.0.0.1:<container-port>` inside the EC2.
3. Authenticates inside the container as the `worker` user with a per-session key.

```
your laptop ── ssh ──▶ ubuntu@<ec2>:22  ── tunnel ──▶ 127.0.0.1:<port>  ──▶ worker@<container>

       (your SSH key)                            (per-session ed25519 key)
```

Two keys, two hops. The CLI sets up both for you – you just need *your* SSH key on the EC2's allow-list.

***

## What you need (one-time)[​](#what-you-need-one-time "Direct link to What you need (one-time)")

1. **Vinted VPN – specifically `backup-vinted-vpn`.** Vinted has two; only this one reaches APE. The EC2's security group allows `:22` from Vinted-internal CIDRs.
2. **An SSH key on your machine** whose public half has been added to the EC2's `authorized_keys` by the admin.
3. **Node.js + npm** to install the CLI.

That's it. No manual `~/.ssh/config` edits – the CLI handles them.

***

## Step 1 – Install the CLI[​](#step-1--install-the-cli "Direct link to Step 1 – Install the CLI")

```
npm install -g @bloom-ai-workspace/cli@latest
```

Verify:

```
aiw --version
```

***

## Step 2 – Run `aiw enroll`[​](#step-2--run-aiw-enroll "Direct link to step-2--run-aiw-enroll")

```
aiw enroll
```

This will:

1. Check for an existing key at `~/.ssh/id_ed25519`.
2. If missing, run `ssh-keygen -t ed25519` interactively so you can set an optional passphrase.
3. Print your **public** key and copy it to your clipboard.

Paste that line into Slack DM to the admin who maintains the jump host.

> `id_ed25519` is your **private** key – never share it. `id_ed25519.pub` is your **public** key – safe to paste anywhere.

On macOS, if you set a passphrase, save it to your keychain so you only type it once:

```
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

They'll append it to `/home/ubuntu/.ssh/authorized_keys` on the box. Verify (with VPN on):

```
ssh ubuntu@<jump-host> hostname
```

If it prints the EC2's hostname and exits cleanly, you're in.

If you see *Permission denied (publickey)*, the admin hasn't added your key yet (or you're not on VPN).

***

## Step 3 – Use it[​](#step-3--use-it "Direct link to Step 3 – Use it")

**Create a new session interactively:**

```
aiw create
```

**Or connect to an existing session (full UUID or 8-char prefix):**

```
aiw connect 9db46916 --open
```

What `connect` does for you on first run:

1. Generates a per-machine ed25519 keypair under `~/.aiw/`.
2. Pushes the **public** key into the workspace container via the orchestrator API.
3. Writes a `Host bloom-ai-workspace-<id>` block to `~/.ssh/config` with `ProxyJump <jump-host>` and the per-session port.
4. Writes a `Host <jump-host>` block to `~/.ssh/config` so SSH knows which user to use for the jump (no IdentityFile – your default `~/.ssh/id_ed25519` is used).
5. With `--open`: launches Cursor on the remote folder **and** Cursor's Simple Browser on the session app URL.

After that, all of these work from any shell:

```
ssh bloom-ai-workspace-9db46916          # drop into /workspace as worker

cursor --remote ssh-remote+bloom-ai-workspace-9db46916 /workspace

aiw connect 9db46916 --open              # re-launch Cursor + Simple Browser
```

***

## Useful CLI commands[​](#useful-cli-commands "Direct link to Useful CLI commands")

| Command                                       | Description                                                         |
| --------------------------------------------- | ------------------------------------------------------------------- |
| `aiw list`                                    | Show your sessions                                                  |
| `aiw connect <id>`                            | Re-issue SSH config for a session (after a container restart, etc.) |
| `aiw connect <id> --open`                     | Connect + open Cursor folder + Simple Browser on the app URL        |
| `aiw connect <id> --web`                      | Connect + open the app URL in Chrome instead of Simple Browser      |
| `aiw connect <id> --preview`                  | Also open the raw preview URL in Chrome                             |
| `aiw connect <id> --cursor-prompt-text "..."` | Send a prefilled prompt into Cursor's chat panel                    |

`aiw help <command>` for full flag list per command.

***

## Troubleshooting[​](#troubleshooting "Direct link to Troubleshooting")

| Symptom                                                                     | Likely cause                                                | Fix                                                                                            |
| --------------------------------------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `Cannot reach API at http://localhost:3001`                                 | Old CLI version pinned to localhost                         | `npm install -g @bloom-ai-workspace/cli@latest`                                                |
| `ssh ubuntu@<jump>` → *Permission denied (publickey)*                       | Public key not added to the EC2 yet, or VPN off             | Verify VPN; ask admin to confirm; check `chmod 600 ~/.ssh/id_ed25519`                          |
| `ssh bloom-ai-workspace-<id>` hangs at the jump                             | EC2 `:22` unreachable from your network                     | `nc -z <jump-host> 22` – if that fails, VPN issue                                              |
| `aiw connect` SSH probe shows `✗` but commands then run fine                | Container was still booting                                 | Retry – `aiw connect` is idempotent                                                            |
| Cursor opens to the agents/chat panel instead of the editor                 | Cursor restores the last-active panel (not the CLI's doing) | In Cursor, close the chat panel, re-open the folder                                            |
| Old session block lingering in `~/.ssh/config` after the session is deleted | Cleanup misses some entries                                 | Open `~/.ssh/config` and delete the `# BEGIN bloom-ai-workspace-<id>` … `# END` block manually |

***

## For admins – adding a new dev[​](#for-admins--adding-a-new-dev "Direct link to For admins – adding a new dev")

When a new dev sends you their public key, append one line to the EC2's `authorized_keys`. From your machine:

```
PUBKEY="ssh-ed25519 AAAA... alice@laptop"

ssh -i ~/path/to/jump-host.pem ubuntu@<jump-host> \

  "grep -qxF '$PUBKEY' ~/.ssh/authorized_keys || echo '$PUBKEY' >> ~/.ssh/authorized_keys"
```

`grep -qxF` makes it idempotent, safe to run twice.

To revoke:

```
ssh -i ~/path/to/jump-host.pem ubuntu@<jump-host> \

  "sed -i '/alice@laptop/d' ~/.ssh/authorized_keys"
```

(Match by the trailing `user@host` comment on each key. `grep` first to be sure you're deleting the right line.)
