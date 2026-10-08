---
title: How to Manage Work Items in GitKraken CLI
description: Start, review, commit, open pull requests for, and clean up a work item across multiple repositories with the deprecated gk work commands in GitKraken CLI.
product: "GitKraken CLI"
feature: "Work Items"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

> **Deprecated:** As of GitKraken CLI 3.1.76, the `gk work` and `gk workspace` commands are deprecated and will be removed in a future release. They still work, but each command prints a deprecation warning. There's no direct replacement. For single-repository work, use standard Git commands with the [GitKraken CLI AI features](https://help.gitkraken.com/cli/GK-CLI-ai-features/), such as `gk ai commit` and `gk ai pr create`.

A work item is a task, such as a bug fix or feature, that spans more than one repository in your GitKraken workspace. With `gk work`, you can start the task, review changes, commit, open pull requests, and clean up in every repository at once, instead of repeating each step in each repository.

## Requirements

To use work items, you need the following:

- **Workspace:** an active GitKraken workspace that contains the repositories you're working in.
- **Plan:** you can use work items on any plan. AI-assisted actions require a paid plan.
- **Account:** sign in with `gk auth login` to use GitKraken cloud features.
- **Organization:** set an organization with `gk organization set <ORG_NAME>` to generate commits and pull requests with AI.
- **Scope:** every `gk work` command runs in every repository in the active workspace.

The following table summarizes the work item commands:

| Command | Use it to | Needs AI or sign-in | Result |
| --- | --- | --- | --- |
| `gk work start <name>` | Start a task across multiple repositories | No | Creates the work item across the workspace |
| `gk work info` | Review pending changes before you commit or open pull requests | No | Shows the work item's state in each repository |
| `gk work commit --ai` | Commit in each repository with AI-generated messages | Yes, and a paid plan | Commits staged changes in each affected repository |
| `gk work pr create --ai` | Open pull requests for the work item | Yes, and a paid plan | Creates pull requests for every repository with changes |
| `gk work end` | Finish the work item and clean up | No | Closes the work item and offers cleanup options |

For every option, see the [`gk work` command reference](https://gitkraken.github.io/gk-cli/docs/gk_work.html).

***

## When to Use GitKraken CLI Work Items Instead of Standard Git Commands

Use `gk work` when one issue, bug fix, or feature spans multiple repositories in the same workspace. If your work stays in one repository and you don't need matching commits, pull requests, or cleanup across repositories, use standard Git commands instead.

***

## How to Start a GitKraken CLI Work Item Quickly

Follow these steps for the shortest path through a multi-repository task. The next section explains each command in detail.

1. Start a new work item:
   ```
   gk work start <name>
   ```
2. Review pending changes in every repository in the workspace:
   ```
   gk work info
   ```
3. Stage your changes with `git add`, then commit with an AI-generated message:
   ```
   gk work commit --ai
   ```
4. Create pull requests for every repository in the work item:
   ```
   gk work pr create --ai
   ```
5. Finish and clean up the work item:
   ```
   gk work end
   ```

Every `gk work` command runs in parallel in every repository in the active workspace. To generate commit messages and pull requests with AI, you need to be signed in, have an organization set, and have a paid plan.

***

## How to Run a GitKraken CLI Work Item from Start to Finish

To create a task that spans every repository in the active workspace, run `gk work start`:

```
gk work start <name>
```

The `<name>` is the title of your work item. GitKraken CLI sets up each repository in your workspace and checks for **pending commits, pull requests, or open work items**.

<figure>
  <img src="/wp-content/uploads/gk-cli-work.png" class="help-center-img img-bordered" alt="Terminal output of gk work start setting up each repository in the workspace and checking for pending items." />
  <figcaption style="text-align: center; color: #888">Starting a work item sets up your workspace and checks for pending items.</figcaption>
</figure>

Before you commit or open pull requests, review the state of the work item with `gk work info`:

```
gk work info
```

<figure>
  <img src="/wp-content/uploads/gk-cli-w-info.png" class="help-center-img img-bordered" alt="Terminal output of gk work info listing the changes in each repository of the work item." />
  <figcaption style="text-align: center; color: #888">Use <code>gk work info</code> to review changes in every repository.</figcaption>
</figure>

### How to Commit Work Item Changes with AI

To generate commit messages and commit your staged changes in each repository of the work item, run:

```
gk work commit --ai
```

This command does the following:

* Analyzes your staged changes with AI.
* Writes a commit message that fits each change.
* Commits the changes in each repository in the work item.

To choose the AI model for one run, add `--model <MODEL_ID>`. To learn more about models, see [How to Use AI Features in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-ai-features/).

<figure>
  <img src="/wp-content/uploads/gk-cli-w-commit.png" class="help-center-img img-bordered" alt="Terminal output of gk work commit --ai showing AI-generated commit messages for each repository." />
  <figcaption style="text-align: center; color: #888">AI-generated commit messages help keep your commit history consistent.</figcaption>
</figure>

### How to Create Pull Requests for a Work Item with AI

To open pull requests for every repository in the active work item, run:

```
gk work pr create --ai
```

GitKraken CLI creates a pull request with an AI-generated title and description for each repository that has changes in the work item. Run this command after you review the work item and commit your changes.

### How to End and Clean Up a Work Item

When the task is complete, close the work item and clean up its temporary resources:

```
gk work end
```

GitKraken CLI asks whether to delete or keep your local changes, then removes the work item's temporary resources.

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
