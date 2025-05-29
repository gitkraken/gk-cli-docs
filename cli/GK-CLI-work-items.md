---
title: Work Items
description: Learn how to take action on multiple repos at once with Work Items.
taxonomy:
    category: cli
---

<kbd>Last updated: May 2025</kbd> 

## Managing Work Items with GitKraken CLI

The `gk work` command suite provides a unified workflow for managing a work item throughout its lifecycle—from task initiation to cleanup. This command streamlines development tasks, enhancements, and bug fixes by automating actions like branch creation, committing changes, pull request creation, and workspace cleanup.

With the power of AI, `gk work` also enables automatic generation of commit messages and pull requests without leaving the terminal.

## Boost Efficiency with Parallel Execution

Execute commands across multiple repositories in parallel to complete tasks faster and more efficiently.

***

## Example Workflow

To create a work item, use:

```
gk work start <name>
```

The `<name>` assigns a title to your work item. This initializes all repositories in your workspace and checks for any **pending commits, pull requests, or open work items.**

<figure>
  <img src="/wp-content/uploads/gk-cli-work.png" class="img-bordered img-responsive center" alt="Work item initialization in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Creating a work item initializes your workspace and checks for pending items.</figcaption>
</figure>

To view pending changes:

```
gk work info
```

<figure>
  <img src="/wp-content/uploads/gk-cli-w-info.png" class="img-bordered img-responsive center" alt="Work info output in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Use <code>gk work info</code> to review changes across all repositories.</figcaption>
</figure>

## Committing Changes with AI

Use AI to generate commit messages and commit changes in parallel:

```
gk work commit --ai
```

This command:

* Analyzes staged changes using AI.
* Generates context-aware commit messages.
* Commits changes across all repositories in the work item.

<figure>
  <img src="/wp-content/uploads/gk-cli-w-commit.png" class="img-bordered img-responsive center" alt="AI-generated commit in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">AI-generated commit messages help standardize your commit history.</figcaption>
</figure>

## Creating a Pull Request with AI

Generate pull requests using:

```
gk work pr create --ai
```

This creates pull requests for **all** changes in the current work item with AI-generated messages, streamlining collaboration and review.

## Finalizing a Work Item

When your work is complete, end the work item with:

```
gk work end
```

This command cleans up your workspace and provides options to delete or retain local changes while removing temporary resources.

