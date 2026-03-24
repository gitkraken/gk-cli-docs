---
title: How to Install and Set Up GitKraken CLI
description: Install GitKraken CLI on macOS, Windows, or Linux, then authenticate, set an organization, sync providers, and load repositories into a workspace.
product: "GitKraken CLI"
feature: "CLI Setup and Getting Started"
content_type: "install"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-03"
taxonomy:
    category: cli
---

<kbd>Last updated: March 2026</kbd>

GitKraken CLI is the command-line tool for managing GitKraken workspaces, providers, and AI-assisted workflows from the terminal. This page helps developers and agents install `gk`, authenticate with a GitKraken account, set an organization, and start working on macOS, Windows, or Linux.

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk_cli_setup_new.png" class="img-responsive center img-bordered" alt="Screenshot of the GitKraken CLI setup screen">
  <figcaption style="color:#888; text-align:center">GitKraken CLI Setup.</figcaption>
</figure>

GitKraken CLI is available on macOS, Windows, Linux, and Unix systems.

## Requirements

- OS support: macOS, Windows, Linux, and Unix systems
- Plan support: installation and basic CLI setup are available on all plans, including Community
- Authentication: `gk auth login` is required for GitKraken cloud features
- Organization: `gk organization set <ORG_NAME>` is required for AI-powered features
- AI plan requirement: AI-powered features require a paid plan such as Pro, Advanced, Business, or Enterprise
- Integrations: GitHub, GitLab, Bitbucket, and Jira can be synced with `gk provider list --sync`

| Install method | OS | Command or action | Best for | Requires admin access |
| --- | --- | --- | --- | --- |
| Homebrew | macOS | `brew install gitkraken-cli` | Standard macOS setup | No |
| Winget | Windows | `winget install gitkraken.cli` | Standard Windows setup | Usually no |
| Snap | Linux | `sudo snap install gitkraken-cli` | Managed Linux installs | Yes |
| Binary download | macOS, Linux, Windows | Download from the releases page and add `gk` or `gk.exe` to `PATH` | Manual or portable installs | Depends on install location |

***

## Quick Start

Use this Quick Start when you want the shortest path to a working GitKraken CLI setup. The detailed installation and configuration walkthroughs appear later on this page.

1. Install `gk` using your platform's package manager (Homebrew, Winget, or Snap) or download a binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest).
2. Authenticate with your GitKraken account to enable cloud features:
   ```
   gk auth login
   ```
3. Confirm and set your organization (required to enable AI features):
   ```
   gk organization list
   gk organization set <ORG_NAME>
   ```
4. Sync your provider integrations (GitHub, GitLab, Bitbucket, Jira):
   ```
   gk provider list --sync
   ```
5. Set a workspace and clone repositories into it:
   ```
   gk workspace set <NAME>
   gk ws clone <name> <root-path>
   ```

An authenticated session, configured organization, and paid plan are required for AI-powered features including commit message generation and pull request creation.

***

## Where to Find GitKraken CLI Documentation

Check out the [installation instructions](https://help.gitkraken.com/cli/cli-home/#how-to-install-gitkraken-cli) and [examples](https://help.gitkraken.com/cli/cli-home/#how-to-start-using-gitkraken-cli-after-installation) below. To view full command references, [see the GitKraken CLI command list](https://gitkraken.github.io/gk-cli/docs/gk.html).

***

## How to Install GitKraken CLI

Use a package manager when you want the simplest install path with native updates. Use the downloadable binary when you need a manual or portable install, or when your package manager is unavailable.

### How to Install GitKraken CLI on macOS

Use Homebrew when you want the standard macOS install path with package-managed updates:

```
brew install gitkraken-cli
```

Use the downloadable binary when you need a manual install or cannot use Homebrew:

```
mv ~/Downloads/gk /usr/local/bin/gk
```

### How to Install GitKraken CLI on Linux and Unix

#### How to Install GitKraken CLI with Snap

Use Snap when you want a managed Linux install through the system package runtime:

```
sudo snap install gitkraken-cli
```

#### How to Install GitKraken CLI from a Downloaded Binary

Use the downloadable binary when Snap is unavailable or when you need a portable install from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest):

```
mv ~/Downloads/gk /usr/local/bin/gk
```

Use a user-owned directory when you do not want to install `gk` into a system path:

```
mkdir "$HOME/cli"
mv ~/Downloads/gk "$HOME/cli"
export PATH="$HOME/gk:$PATH"
```

Use native Linux packages when you already have a `.deb` or `.rpm` release artifact:

```
sudo apt install ./gk.deb
```

or

```
sudo rpm -i ./gk.rpm
```

### How to Install GitKraken CLI on Windows

Use Winget when you want the standard Windows install path with package management:

```
winget install gitkraken.cli
```

Use the downloadable binary when you need a manual Windows install. Download from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest), move `gk.exe` to your chosen directory, and update your system PATH:

1. Search for **Environment Variables**.
2. Click **Edit the system environment variables**.
3. Click **Environment Variables...**.
4. In **System Variables**, locate or create the **PATH** variable.
5. Append the path to `gk.exe`.

***

## How to Troubleshoot GitKraken CLI Installation

### How to Fix the Oh-My-Zsh `gk` Alias Conflict

Oh-My-Zsh may alias `gitk` as `gk`. To remove the alias:

```
unalias gk
```

***

## How to Start Using GitKraken CLI After Installation

Use GitKraken CLI without logging in when you only need local command-line workflows. Sign in with your GitKraken account when you need AI-generated commits or pull requests, cloud workspaces, MCP integration, or synchronized providers:

```
gk auth login
```

This command opens your default browser to complete authentication. 

If no default browser is set on your device, the URL will appear in your terminal. Copy this URL and open it in any browser, then enter the code provided by [gk.dev](gitkraken.dev) to complete the login process.

### How to Set Your GitKraken Organization

Use this step when you need AI-powered features that depend on an active GitKraken organization. To verify your current organization:

```
gk organization list
```

Set your organization (required for AI features):

```
gk organization set <ORG_NAME>
```

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-org-ls-new.png" class="img-bordered img-responsive center" alt="Organization list view in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Use <code>gk organization list</code> to confirm and set the correct GitKraken Organization.</figcaption>
</figure>

### How to Sync Your Git Provider and Jira Integrations

Use this step when you want GitKraken CLI to discover connected Git providers and Jira accounts. Once authenticated and your organization is set, synchronize integrations:

```
gk provider list --sync
```

To add a provider manually:

```
gk provider add
```

See `gk provider add --help` for available options.

Supported integrations include GitHub, GitLab, Bitbucket, and Jira.

### How to Load Repositories Into a GitKraken Workspace

Use this step when you want GitKraken CLI commands to run inside a selected GitKraken workspace. To work within a GitKraken workspace:

1. List available workspaces:
   ```
   gk workspace list
   ```
2. Set your desired workspace:
   ```
   gk workspace set <NAME>
   ```
3. Clone a repository into the workspace:
   ```
   gk ws clone <name> <root-path>
   ```

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-ws-set-new.png" class="img-bordered img-responsive center" alt="Setting a GitKraken workspace via CLI">
  <figcaption style="color:#888; text-align:center">Switching and cloning repositories within GitKraken CLI workspaces.</figcaption>
</figure>

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
