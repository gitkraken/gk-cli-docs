---

title: GitKraken CLI
description: Learn how to work with the GitKraken CLI
taxonomy:
    category: cli

---
# GitKraken CLI
Welcome to the GitKraken CLI — an AI-powered, premium developer experience that enhances Git workflows across any repository.

<img src="/wp-content/uploads/gk_cli_setup.png" class="img-responsive center img-bordered">

GitKraken CLI is available on macOS, Windows and Unix systems.

***

## Documentation

Check out the [installation instructions](/gitkraken-client/gitkraken-cli/#Installation) and [examples](/gitkraken-client/gitkraken-cli/#Examples) below. For command usage [see the docs](https://gitkraken.github.io/gk-cli/docs/gk.html).

***

## Installation

### macOS 

`gk` is available from [Homebrew](https://brew.sh/) with the following command:

```
brew install gitkraken-cli
```
#### Downloadable Binary
Or download it from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and add it to your binaries folder:

```
mv ~/Downloads/gk /usr/local/bin/gk
``` 

### Unix / Ubuntu

### Snap

`gk` is available on [Snap](https://snapcraft.io/gitkraken-cli) with the following command:
```
sudo snap install gitkraken-cli
```

#### Downloadable Binary

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

#### Downloadable Binary

Download the binary from the [releases page](https://github.com/gitkraken/gk-cli/releases/latest) and place the `gk.exe` in a desired folder. Then edit your environment variables to add it to your PATH.

1. In Search, search for **Environment Variables**.
2. Click on the **Edit the system environment variables** result.
3. In the modal, click on the **Environment Variables...** button.
4. In the **System Variables** section, scroll until you find the **PATH** variable. Click on it.
    - If it doesn't exist, create a variable with the name **PATH**. 
5. Add the path to the `gk` binary at the end.

***

## Troubleshooting

### gk from Oh-My-Zsh

Oh-My-Zsh has ```gitk``` aliased as ```gk``` and that can create some problems. To fix this, type in your terminal:

```
unalias gk
```

***

## Get Started with GitKraken CLI

```
GitKraken CLI does not require login to your GitKraken account, and most features are available immediately. However, to access advanced functionalities such as AI Commit and PR generation, cloud workspace management, and integration syncing, follow the steps below to enable these features.
```

To unlock the full potential of GitKraken CLI login to your account using the `gk auth login` command. This will open a login in your default browser.

### Set Your GitKraken Organization

Once logged in, verify that you are in the correct GitKraken Organization by running: `gk organization list`. 

To match your plan with the correct organization, set your default organization using: `gk organization set <ORG_NAME>`.  **This step is important for unlocking AI features**.

<img src="/wp-content/uploads/gk-cli-org-ls.png" class="img-bordered img-responsive center">

### Synchronize Your Integrations

Once logged in and your organization is set, you can synchronize your integrations from [gitkraken.dev](https://gitkraken.dev/settings/integrations) by running `gk provider list --sync`. 

To manually connect to a provider, use: `gk provider add`. 

For a full list of strings please see `gk provider add --help`.

```
GitKraken CLI currently supports GitHub, GitLab and Jira.
```

### Load Your Repositories

Quickly load your repositories by opening your GitKraken workspace. 

First, list your available workspaces: `gk workspace list` 

Then, set your desired workspace: `gk workspace set <NAME>` 

<img src="/wp-content/uploads/gk-cli-ws-set.png" class="img-bordered img-responsive center">

To clone a repository within the workspace, use: `gk ws clone <name> <root-path>`

***


## Work Items

### Managing Work Items with GitKraken CLI

The `work` command suite provides a unified workflow for managing a work item throughout its lifecycle—from task initiation to cleanup. This command helps streamline the process of working on tasks, enhancements, or bug fixes by automating and centralizing actions like branch creation, starting work on code, committing changes, PR management, and more.

With the power of AI, `work` allows you to generate commit messages and create pull requests without ever leaving the terminal.

### Boost Efficiency with Parallel Execution

Speed up your tasks by seamlessly executing commands across multiple repositories in parallel.

***

### An Example of a Work Item Workflow

<img src="/wp-content/uploads/gk-cli-work.png" class="img-bordered img-responsive center">

To create a Work Item, run `gk work start <name>`. The `<name>` flag assigns a title to your work item. This command initializes all repositories in your workspace and checks for any **pending commits, pull requests, or other open work items.**

Run `gk work info` to see the list of pending changes. In this example we have two repostiories loaded with pending changes to both. 

<img src="/wp-content/uploads/gk-cli-w-info.png" class="img-bordered img-responsive center">

#### Committing Changes with AI

To commit multiple changes simultaneously and streamline your workflow, you can use AI to generate a commit message. Run the following command: `gk work commit --ai`

The GitKraken CLI will then:

* Analyze the staged content using AI.

* Generate a commit message based on the changes.

* Commit all pending changes in the work item in parallel.

By committing staged changes together, GitKraken CLI ensures **maximum efficiency** and keeps your workflow seamless.

<img src="/wp-content/uploads/gk-cli-w-commit.png" class="img-bordered img-responsive center">

#### Creating a Pull Request with AI

To commit multiple changes simultaneously while optimizing workflow, use AI to generate a commit message with the command `gk work pr create --ai`. 

Pull requests will be created for **all** pending changes in your work item. 

#### Finalizing a Work Item

Once you're satisfied with your changes and your work item is complete, run: `gk work end`. 

The `end` command finalizes a work item by **cleaning up the workspace** and ensuring it is ready for future tasks. It also provides options to **delete or preserve local changes** while removing any temporary setups associated with the work item.

