---
title: How to Install and Set Up GitKraken CLI
description: Install GitKraken CLI on macOS, Windows, or Linux, sign in, set your organization, and connect your Git providers and issue trackers.
product: "GitKraken CLI"
feature: "CLI Setup and Getting Started"
content_type: "install"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

GitKraken CLI (`gk`) brings GitKraken to your terminal. You can write commits with AI, untangle messy changes into clean commits, resolve merge conflicts, and see your pull requests and issues without opening a browser. It also gives AI coding agents such as Claude Code, Cursor, and GitHub Copilot access to GitKraken tools.

If you use GitLens or GitKraken Desktop, you may already have `gk` on your machine. GitLens uses it to run the GitKraken MCP server, and GitKraken Desktop, GitLens, and Kepler ADE by GitKraken use it to show live AI agent sessions. To learn more, see [How GitKraken CLI Works with GitLens and GitKraken Desktop](https://help.gitkraken.com/cli/GK-CLI-gitlens-and-gitkraken-desktop/).

This page shows you how to install `gk`, sign in, and connect your accounts on macOS, Windows, or Linux.

<figure>
  <img src="/wp-content/uploads/gk_cli_setup_new.png" class="help-center-img img-bordered" alt="GitKraken CLI welcome screen in a terminal after installation." />
  <figcaption style="text-align: center; color: #888">GitKraken CLI setup</figcaption>
</figure>

## Requirements

Before you start, check the following requirements:

- **Operating system:** macOS, Windows, Linux, or another Unix system.
- **Plan:** you can install and set up GitKraken CLI on any plan, including Community.
- **Account:** sign in with `gk auth login` to use GitKraken cloud features.
- **Organization:** set an organization with `gk organization set <ORG_NAME>` to use AI features.
- **AI features:** AI-powered features require a paid plan such as Pro, Advanced, Business, or Enterprise.
- **Integrations:** connect GitHub, GitLab, Bitbucket, Azure DevOps, Jira, Linear, or Trello. To see the full list, go to [How to Connect Providers in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-providers/).

The following table compares the ways to install GitKraken CLI:

| Install method | OS | Command or action | Best for | Needs admin access |
| --- | --- | --- | --- | --- |
| Homebrew | macOS | `brew install gitkraken-cli` | Standard macOS setup | No |
| Winget | Windows | `winget install gitkraken.cli` | Standard Windows setup | Usually no |
| Snap | Linux | `sudo snap install gitkraken-cli` | Managed Linux installs | Yes |
| npm | macOS, Linux, Windows | `npm install -g @gitkraken/gk` | Machines that already use Node.js | Depends on your npm setup |
| Binary download | macOS, Linux, Windows | Download from the releases page and add `gk` or `gk.exe` to your `PATH` | Manual or portable installs | Depends on install location |

***

## Quick Start

Follow these steps for the shortest path to a working setup. The sections later on this page explain each step in detail.

1. Install `gk` with your package manager (Homebrew, Winget, Snap, or npm), or download a binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest).
2. Sign in to your GitKraken account:
   ```
   gk auth login
   ```
3. Check your organizations and set the one you want to use. You need an organization for AI features:
   ```
   gk organization list
   gk organization set <ORG_NAME>
   ```
4. Sync the Git providers and issue trackers you already connected to GitKraken:
   ```
   gk provider list --sync
   ```
5. Confirm your setup:
   ```
   gk whoami
   ```

To use AI-powered features, such as commit message generation and pull request creation, you need to be signed in, have an organization set, and have a paid plan.

***

## Where to Find GitKraken CLI Documentation

This Help Center explains what you can do with GitKraken CLI and how to use it in real workflows. Start with the [installation instructions](https://help.gitkraken.com/cli/cli-home/#how-to-install-gitkraken-cli) and the [setup steps](https://help.gitkraken.com/cli/cli-home/#how-to-start-using-gitkraken-cli-after-installation) on this page. For every command and flag, see the [GitKraken CLI command reference](https://gitkraken.github.io/gk-cli/docs/gk.html).

***

## How to Install GitKraken CLI

Use a package manager for the simplest install and automatic updates. Use the downloadable binary for a manual or portable install, or when you can't use a package manager.

### How to Install GitKraken CLI on macOS

Use Homebrew for the standard macOS install with package-managed updates:

```
brew install gitkraken-cli
```

If you can't use Homebrew, download the binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and move it into a folder on your `PATH`:

```
mv ~/Downloads/gk /usr/local/bin/gk
```

### How to Install GitKraken CLI on Linux and Unix

You can install GitKraken CLI on Linux with Snap, a downloaded binary, or a `.deb` or `.rpm` package.

#### How to Install GitKraken CLI with Snap

Use Snap for a managed Linux install:

```
sudo snap install gitkraken-cli
```

#### How to Install GitKraken CLI from a Downloaded Binary

If Snap isn't available, or you need a portable install, download the binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and move it into a system folder:

```
mv ~/Downloads/gk /usr/local/bin/gk
```

To install `gk` without using a system folder, put it in a folder you own and add that folder to your `PATH`:

```
mkdir "$HOME/cli"
mv ~/Downloads/gk "$HOME/cli"
export PATH="$HOME/cli:$PATH"
```

If you downloaded a `.deb` or `.rpm` package from the releases page, install it with your system package manager. Replace the file name with the name of the file you downloaded:

```
sudo apt install ./gk.deb
```

or

```
sudo rpm -i ./gk.rpm
```

### How to Install GitKraken CLI on Windows

Use Winget for the standard Windows install with package management:

```
winget install gitkraken.cli
```

To install manually, download the binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest), move `gk.exe` to a folder of your choice, and add that folder to your system `PATH`:

1. In the Windows search box, search for **Environment Variables**.
2. Click **Edit the system environment variables**.
3. Click **Environment Variables...**.
4. In **System Variables**, find or create the **PATH** variable.
5. Add the folder that contains `gk.exe`.

### How to Install GitKraken CLI with npm

If you already use Node.js, you can install GitKraken CLI on any platform with npm:

```
npm install -g @gitkraken/gk
```

***

## How to Troubleshoot GitKraken CLI Installation

Use the following fixes for common installation problems.

### How to Fix the Oh-My-Zsh `gk` Alias Conflict

Oh-My-Zsh defines `gk` as an alias for `gitk`, so typing `gk` may open `gitk` instead of GitKraken CLI. To remove the alias from your current terminal session, run:

```
unalias gk
```

### How to Sign In on a Machine Without a Browser

On a remote server or another machine without a browser, run `gk auth login` and open the URL it prints in a browser on any device. If the GitKraken login page shows you a single-use code, pass it to the CLI:

```
gk auth login --auth-code <CODE>
```

***

## How to Start Using GitKraken CLI After Installation

You can use GitKraken CLI without signing in for local Git work. To use the following features, sign in with your GitKraken account:

- AI-generated commits and pull requests
- The GitKraken MCP server for AI coding agents
- Pull request and issue lists from your connected providers

To sign in, run:

```
gk auth login
```

This command opens your default browser so you can finish signing in.

If you don't have a default browser set, the CLI prints a URL in your terminal. Open that URL in any browser, then enter the code from [gitkraken.dev](https://gitkraken.dev) to finish signing in.

To check who you're signed in as, which organization is active, and which providers you've connected, run:

```
gk whoami
```

To sign out, run `gk auth logout`. To sign out of every session, add `--all`.

### How to Set Your GitKraken Organization

AI features run under your active GitKraken organization. To see your organizations, run:

```
gk organization list
```

To set the organization you want to use, run:

```
gk organization set <ORG_NAME>
```

<figure>
  <img src="/wp-content/uploads/gk-cli-org-ls-new.png" class="help-center-img img-bordered" alt="Output of gk organization list showing the available GitKraken organizations and which one is active." />
  <figcaption style="text-align: center; color: #888">Use <code>gk organization list</code> to confirm and set your GitKraken organization.</figcaption>
</figure>

### How to Sync Your Git Provider and Jira Integrations

If you already connected GitHub, GitLab, Bitbucket, Jira, or other integrations in GitKraken Desktop, GitLens, or gitkraken.dev, sync them to the CLI. After you sign in and set your organization, run:

```
gk provider list --sync
```

To add a provider manually, run `gk provider add` with the provider name, such as `github` or `jira`:

```
gk provider add <PROVIDER>
```

To see the available options, run `gk provider add --help`. To connect a self-hosted instance or more than one account, see [How to Connect Providers in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-providers/).

### How to Load Repositories Into a GitKraken Workspace

> **Note:** As of GitKraken CLI 3.1.76, the `gk workspace` commands are deprecated and will be removed in a future release. They still work, but each command prints a deprecation warning.

To work with an existing GitKraken workspace from the CLI:

1. List your workspaces:
   ```
   gk workspace list
   ```
2. Set the workspace you want to use:
   ```
   gk workspace set <NAME>
   ```
3. Clone the workspace repositories into a local folder (`gk ws` is short for `gk workspace`):
   ```
   gk ws clone <name> <root-path>
   ```

<figure>
  <img src="/wp-content/uploads/gk-cli-ws-set-new.png" class="help-center-img img-bordered" alt="Terminal output after setting a GitKraken workspace and cloning its repositories." />
  <figcaption style="text-align: center; color: #888">Setting a workspace and cloning its repositories in GitKraken CLI.</figcaption>
</figure>

***

## What to Do Next

After setup, try the following:

- [Use AI features](https://help.gitkraken.com/cli/GK-CLI-ai-features/) to write commits, compose clean commits, and resolve merge conflicts.
- [Track pull requests and issues](https://help.gitkraken.com/cli/GK-CLI-pull-requests-and-issues/) across your providers.
- [Connect AI coding agents](https://help.gitkraken.com/cli/gk-cli-mcp/) to the GitKraken MCP server.

***

## How to Uninstall GitKraken CLI AI Hooks

GitKraken Desktop, GitLens, and Kepler can show live status for your AI coding agent sessions. To do this, GitKraken CLI registers hooks on the agent's lifecycle events, such as session start and end, tool use, prompt submission, and permission requests. Each hook sends the event to the local `gk` process, which saves the session on your computer and passes it to GitKraken apps running on the same computer.

Hook data stays on your computer. Depending on the event, it can include your prompt, the tool the agent is using and its arguments, and the files the agent changed. To learn more, see [How GitKraken CLI Works with GitLens and GitKraken Desktop](https://help.gitkraken.com/cli/GK-CLI-gitlens-and-gitkraken-desktop/).

To stop sending agent events to GitKraken apps, uninstall the hooks for that agent.

### Uninstall GitKraken CLI AI Hooks for Claude Code

```bash
gk ai hook uninstall claude-code
```

### Uninstall GitKraken CLI AI Hooks for OpenCode

```bash
gk ai hook uninstall opencode
```

To see which agents have hooks installed, run `gk agents list`. Hooks are also available for Cursor, Codex, GitHub Copilot CLI, Antigravity, Pi, Augment, and Grok Build.

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
