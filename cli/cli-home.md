---
title: GitKraken CLI
description: Learn how to work with the GitKraken CLI
taxonomy:
    category: cli
---

Welcome to the GitKraken CLI — an AI-powered, premium developer experience that enhances Git workflows across any repository.

<figure>
  <img src="/wp-content/uploads/gk_cli_setup.png" class="img-responsive center img-bordered" alt="Screenshot of the GitKraken CLI setup screen">
  <figcaption style="color:#888; text-align:center">Beep boop bop.</figcaption>
</figure>

GitKraken CLI is available on macOS, Windows, and Unix systems.

***

## Documentation

Check out the [installation instructions](/gitkraken-client/gitkraken-cli/#Installation) and [examples](/gitkraken-client/gitkraken-cli/#Examples) below. To view full command references, [see the GitKraken CLI documentation](https://gitkraken.github.io/gk-cli/docs/gk.html).

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

GitKraken CLI works out of the box without requiring login. For advanced features such as AI commit and PR generation, cloud workspace support, and integration sync, log in to your GitKraken account:

```
gk auth login
```

This command opens your default browser to complete authentication.

### Set Your GitKraken Organization

To verify your current organization:

```
gk organization list
```

Set your organization (required for AI features):

```
gk organization set <ORG_NAME>
```

<figure>
  <img src="/wp-content/uploads/gk-cli-org-ls.png" class="img-bordered img-responsive center" alt="Organization list view in GitKraken CLI">
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

Supported integrations include GitHub, GitLab, and Jira.

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

<figure>
  <img src="/wp-content/uploads/gk-cli-ws-set.png" class="img-bordered img-responsive center" alt="Setting a GitKraken workspace via CLI">
  <figcaption style="color:#888; text-align:center">Switching and cloning repositories within GitKraken CLI workspaces.</figcaption>
</figure>


