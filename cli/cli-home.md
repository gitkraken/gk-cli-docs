---
title: GitKraken CLI
description: Learn how to work with the GitKraken CLI
taxonomy:
    category: cli
---

<kbd>Last updated: March 2026</kbd>

Welcome to the GitKraken CLI — an AI-powered, premium developer experience that enhances Git workflows across any repository.

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk_cli_setup_new.png" class="img-responsive center img-bordered" alt="Screenshot of the GitKraken CLI setup screen">
  <figcaption style="color:#888; text-align:center">GitKraken CLI Setup.</figcaption>
</figure>

GitKraken CLI is available on macOS, Windows, and Unix systems.

***

## Quick Start

To install and configure GitKraken CLI on macOS, Windows, or Linux:

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

An authenticated session and configured organization are required for AI-powered features including commit message generation and pull request creation.

***

## Documentation

Check out the [installation instructions](/gitkraken-client/gitkraken-cli/#Installation) and [examples](/gitkraken-client/gitkraken-cli/#Examples) below. To view full command references, [see the GitKraken CLI command list](https://gitkraken.github.io/gk-cli/docs/gk.html).

***

## Installation

### macOS

Install `gk` using [Homebrew](https://brew.sh/):

```
brew install gitkraken-cli
```

Or download a binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest):

```
mv ~/Downloads/gk /usr/local/bin/gk
```

### Unix / Ubuntu

#### Snap

Install via [Snap](https://snapcraft.io/gitkraken-cli):

```
sudo snap install gitkraken-cli
```

#### Downloadable Binary

From the [releases page](https://github.com/gitkraken/gk-cli/releases/latest):

```
mv ~/Downloads/gk /usr/local/bin/gk
```

Alternatively:

```
mkdir "$HOME/cli"
mv ~/Downloads/gk "$HOME/cli"
export PATH="$HOME/gk:$PATH"
```

Install `.deb` or `.rpm` packages:

```
sudo apt install ./gk.deb
```

or

```
sudo rpm -i ./gk.rpm
```

### Windows

Install via [Winget](https://github.com/microsoft/winget-cli):

```
winget install gitkraken.cli
```

Or download from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest), move `gk.exe` to your chosen directory, and update your system PATH:

1. Search for **Environment Variables**.
2. Click **Edit the system environment variables**.
3. Click **Environment Variables...**.
4. In **System Variables**, locate or create the **PATH** variable.
5. Append the path to `gk.exe`.

***

## Troubleshooting

### Oh-My-Zsh alias conflict

Oh-My-Zsh may alias `gitk` as `gk`. To remove the alias:

```
unalias gk
```

***

## Get Started with GitKraken CLI

GitKraken CLI works seamlessly right out of the box—no login required to get started. To unlock the full potential of your workflow with features like AI-powered commit and PR generation, cloud workspace support, MCP integration, and sync capabilities, simply login to your GitKraken account:

```
gk auth login
```

This command opens your default browser to complete authentication. 

If no default browser is set on your device, the URL will appear in your terminal. Copy this URL and open it in any browser, then enter the code provided by [gk.dev](gitkraken.dev) to complete the login process.

### Set Your GitKraken Organization

To verify your current organization:

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

### Synchronize Your Integrations

Once authenticated and your organization is set, synchronize integrations:

```
gk provider list --sync
```

To add a provider manually:

```
gk provider add
```

See `gk provider add --help` for available options.

Supported integrations include GitHub, GitLab, BitBucket and Jira.

### Load Your Repositories

To work within a GitKraken workspace:

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
.copy-wrap{position:relative;display:block}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
.copy-wrap:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.parentNode.classList&&p.parentNode.classList.contains('copy-wrap'))return;var w=document.createElement('div');w.className='copy-wrap';p.parentNode.insertBefore(w,p);w.appendChild(p);var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';w.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='\u2713';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
