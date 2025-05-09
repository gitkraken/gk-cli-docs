---

title: Work Items
description: Learn how to take action on multiple repos at once with Work Items.
taxonomy:
    category: cli

---


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

***
