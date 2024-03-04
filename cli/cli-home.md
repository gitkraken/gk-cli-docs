---

title: GitKraken CLI
description: Learn how to work with the GitKraken CLI
taxonomy:
    category: cli

---

`gk` is GitKraken on the command line. It makes working across multiple repos easier with Workspaces, provides access to pull requests and issues from multiple services (GitHub, GitLab, Bitbucket, etc.), and seamlessly connects with [GitKraken Client](https://www.gitkraken.com/git-client) and [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) in VS Code to visualize `git` information when you need it.

<img src="/wp-content/uploads/cli-gk.png" class="img-responsive center img-bordered">

GitKraken CLI is available on macOS, Windows and Unix systems.

***

## Documentation

Check out the [installation instructions](/gitkraken-client/gitkraken-cli/#Installation) and [examples](/gitkraken-client/gitkraken-cli/#Examples) below. For command usage [see the docs](https://gitkraken.github.io/gk-cli/docs/gk.html).

***

## Installation

### macOS 

`gk` is available from [Homebrew](https://brew.sh/) and [MacPorts](https://www.macports.org/) with the following command:

Homebrew:

```
brew install gitkraken-cli
```

MacPorts:

```
sudo port install gk
```

Or download it from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and add it to your binaries folder:

```
mv ~/Downloads/gk /usr/local/bin/gk
``` 

### Unix / Ubuntu

`gk` is available as a downloadable binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest). Once you have it, add it to your binaries folder:

```
mv ~/Downloads/gk /usr/local/bin/gk
``` 

Or create a new directory, move the binary and add it to $PATH:
```
mkdir "$HOME/cli"
mv ~/Downloads/gk "$HOME/cli"
export PATH="$HOME/gk:$PATH"
``` 

You can also [download](https://github.com/gitkraken/gk-cli/releases/latest) your corresponding package (`.deb`, `.rpm`) and install it with:

```
sudo apt install ./gk.deb
```

or 

```
sudo rpm -i ./gk.rpm
```

### Windows

`gk` is available from [Winget](https://github.com/microsoft/winget-cli) with the following command:

```
winget install gitkraken.cli
```

You can also download it using [Chocolatey](https://community.chocolatey.org/packages/GKCLI):

```
choco install gkcli
```

Or download the binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and place the `gk.exe` in a desired folder. Then edit your environment variables to add it to your PATH.

1. In Search, search for **Environment Variables**.
2. Click on the **Edit the system environment variables** result.
3. In the modal, click on the **Environment Variables...** button.
4. In the **System Variables** section, scroll until you find the **PATH** variable. Click on it.
    - If it doesn't exist, create a variable with the name **PATH**. 
5. Add the path to the `gk` binary at the end.

***

## Configuration

### Nerd Fonts

The GitKraken CLI supports Nerd Fonts to display icons for some commands. To ensure correct icon rendering, please obtain and install a Nerd Font available at https://www.nerdfonts.com/. After installation, set the selected Nerd Font as the default font for your terminal.

***

## Troubleshooting

### ```gk login``` freezes after authenticating in browser

This problem is due to the browser. Currently we know that Safari and Brave do not allow to respond to localhost through port 1314. To fix this, change your default browser or copy the URL before the redirect and open it in another browser.

### gk from Oh-My-Zsh

Oh-My-Zsh has ```gitk``` aliased as ```gk``` and that can create some problems. To fix this, type in your terminal:

```
unalias gk
```

***

## Examples

### 🎯 Focus View

```
gk focus
```

GitKraken Focus View is a unified dashboard that consolidates PRs, Issues, and WIPs across all of the repositories in a [Cloud Workspace](/cli/cli-home/#create-workspaces-to-group-repos). You can view the details of any item and take action on your most important tasks.

<img src="/wp-content/uploads/cli-focus-view.png" class="img-responsive center img-bordered">

#### Pin items to keep them at the top of your list

Use the shortcut <kbd>p</kbd> to pin any PR or Issue to the top of the list. You can unpin an item by using the same shortcut on any pinned item.

#### Snooze items to save them for later

Use the shortcut <kbd>s</kbd> to snooze any PR or Issue, removing them from the list of items. You can view snoozed items by navigating to the `Snoozed` tab in the Focus View. You can unsnooze items and bring them back into your Focus View lists by using the same shortcut on any snoozed item.

### Create Workspaces to group repos

```
gk ws create
```

GitKraken workspaces associate groups of repos and set the context for helpful commands that can operate on, or get information for, multiple repos at once. There are two types of workspaces:

#### Local

Local Workspaces exist only on your machine.

#### Cloud

Cloud Workspaces are accessible on any machine, and can be connected to hosting and issue providers like GitHub and GitLab to get additional information about pull requests and issues. Share Cloud Workspaces with your team to improve onboarding with the ability to clone all repos at once. To enable this extra functionality, Cloud Workspaces require a free GitKraken account. We are continuing to evolve and improve GitKraken Workspaces and welcome any feedback.

<img src="/wp-content/uploads/cli-ws-create.png" class="img-responsive center img-bordered">

### Adding and locating repos

```
gk ws add-repo
```

This will add a new repo to a workspace either by path or remote URL.

```
gk ws locate
```

If you're accessing a Cloud Workspace for the first time, you might need to `locate` the local repos on your machine. Run this command in the directory where youre repos are located so `gk` knows where they are.

```
gk ws clone
```

You can also `clone` all repos in a Workspace at once into a single directory. This is helpful for onboarding when your team works on multiple repos.

### Perform `git` actions on multiple repos at once

```
gk ws [action]
```

In any workspace, you can perform `git` operations like `fetch`, `pull`, `push`, and `checkout` across all repos in the workspace.

### Get pull requests and issues

```
gk provider add
```

Before fetching pull requests and issues, ensure that you have the appropriate provider (GitHub, GitLab, etc.) connected. This will open a browser to authenticate.

```
gk pr list
```

When a Cloud Workspace has a provider connected, you can list all pull requests and issues for repos in the workspace, and view details for a specific one.

<img src="/wp-content/uploads/cli-pr-list.png" class="img-responsive center img-bordered">

```
gk pr view
```

Returns a list of all pull requests for all repos in a workspace. Type to search for a specific pull request and press `enter` to view details.

<img src="/wp-content/uploads/cli-pr-view.png" class="img-responsive center img-bordered">

### Pull Request Insights

```
gk ws insights
```

See the following metrics for all repositories in a Cloud Workspace. The default time period is 7 days, but can be increased to 14 days with any paid GitKraken license.
- Average Cycle Time
- Average Throughput
- Merge Rate
- Opened Pull Requests
- Merged Pull Requests
- Closed Pull Requests

<img src="/wp-content/uploads/cli-ws-insights.png" class="img-responsive center img-bordered">

### Visual Commit Graph

```
gk ws graph
```

Open a visual graph of the repo in your current directory in either [GitKraken Client](https://www.gitkraken.com/git-client) or [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) in VS Code.

<img src='/wp-content/uploads/cli-gk-graph.gif' class='img-bordered img-responsive center'>

## Cloud Patches

### What are Cloud Patches and why would you want to use them

A Cloud Patch is a Git patch that GitKraken securely stores for you so it can be easily shared with others across the GitKraken CLI, GitKraken Client, and GitLens. The patch is directly transferred from your machine into secure storage. 

Cloud Patches allow the ability to engage early with your team before a pull request. They can be created as soon as you have a work in progress. This can help with collaborating on changes prior to a pull request and minimize the delay of pull request reviews.

### How to setup Cloud Patches 

Cloud Patches are enabled in the GitKraken CLI by default. 

### How to work with Cloud Patches

To work with Cloud Patches, use `gk patch [command]`. You can run `gk patch` to see all options offered and what they do.

<img src="/wp-content/uploads/gk-cli-gk-patch.png" class="img-bordered img-responsive center">

To create a Cloud Patch, run `gk patch create`. You will be prompted to provide information about the patch and what it should be created from. †You have the following sharing options:

- `Public`: Anyone that you share the public link with will be able to work with the Cloud Patch.

- `Invite Only`: Only users in the GitKraken Organization who have been selected when sharing will be able to work with the Cloud Patch. They will be required to authenticate with a GitKraken account to access it.

- `Private`: Anyone in the GitKraken Organization will be able to work with the Cloud Patch. They will be required to authenticate with a GitKraken account to access it.

Once the process is completed, you will be provided with a link that can be used by yourself or others to open the cloud patch in GitKraken Client or GitLens. From there, the patch can be applied in either client to work with those changes. To apply a Cloud Patch at a later time to the current repository, you can run `gk patch apply`.

<img src="/wp-content/uploads/gk-cli-patch-create-example.gif" class="img-bordered img-responsive center">

Cloud Patches can be viewed from URLs shared to you and they can be applied to your working tree or to a new or existing branch. Simply select or open the link and then follow the prompts within GitLens or GitKraken Client to apply the Cloud Patch.

<img src='/wp-content/uploads/gkc-apply-cloud-patch-example.gif' class='img-bordered img-responsive center'>

Here are some other helpful commands to be used with Cloud Patches:

* `gk patch view` - preview the changes of a Cloud Patch
* `gk patch list` - list all your Cloud Patches
* `gk patch delete` - delete a Cloud Patch

### Self-Hosting Cloud Patch data

If you do not want your Cloud Patch data stored on GitKraken Servers, we offer the ability for you to host Cloud Patches on your own AWS S3 storage instance. For more information on configuring this, see our documentation [here](/gk-dev/gk-dev-home/#self-hosted).
