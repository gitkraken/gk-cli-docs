---
title: How to Manage Work Items in GitKraken CLI
description: Start, review, commit, create pull requests for, and clean up a GitKraken CLI Work Item across multiple repositories in one workspace.
product: "GitKraken CLI"
feature: "Work Items"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-03"
taxonomy:
    category: cli
---

<kbd>Last updated: March 2026</kbd> 

## How to Manage Work Items with GitKraken CLI

GitKraken CLI Work Items let developers and agents start, review, commit, create pull requests for, and clean up a task across every repository in the active workspace. Use this workflow when one issue affects multiple repositories; AI-generated commits and pull requests require authentication, a configured organization, and a paid plan.

## Requirements

- Workspace: an active GitKraken workspace with the target repositories
- Plan support: Work Items can be used on all plans, but AI-assisted actions require a paid plan
- Authentication: `gk auth login` is required for GitKraken cloud features
- Organization: `gk organization set <ORG_NAME>` is required for AI-generated commits and pull requests
- Scope: `gk work` commands run across every repository in the active workspace

| Command | Use when | Requires AI or auth | Output |
| --- | --- | --- | --- |
| `gk work start <name>` | Start a coordinated task across multiple repositories | No | Initializes the work item across the workspace |
| `gk work info` | Review pending changes before committing or opening pull requests | No | Shows work item state across repositories |
| `gk work commit --ai` | Create commits across repositories with AI-generated messages | Yes, plus a paid plan | Commits staged changes in all affected repositories |
| `gk work pr create --ai` | Open pull requests for the current work item | Yes, plus a paid plan | Creates pull requests for all changes in scope |
| `gk work end` | Finish the work item and clean up temporary resources | No | Closes the work item and offers cleanup options |

***

## How to Start a GitKraken CLI Work Item Quickly

Use this Quick Start when you want the shortest path through a multi-repository task. The detailed command-by-command walkthrough appears later on this page.

1. Start a new work item:
   ```
   gk work start <name>
   ```
2. Review pending changes across all repositories in the workspace:
   ```
   gk work info
   ```
3. Stage your changes, then commit with an AI-generated message:
   ```
   gk work commit --ai
   ```
4. Create pull requests for all repositories in the work item:
   ```
   gk work pr create --ai
   ```
5. Finalize and clean up the work item:
   ```
   gk work end
   ```

All `gk work` commands execute in parallel across every repository in the active workspace. An authenticated GitKraken account with a configured organization and paid plan is required to use AI-generated commit messages and pull requests.

***

## When to Use GitKraken CLI Work Items Instead of Standard Git Commands

Use `gk work` when one issue, bug fix, or feature spans multiple repositories in the same workspace. Use standard Git commands instead when the work stays in a single repository and you do not need synchronized commits, pull requests, or cleanup.

***

## How to Run a GitKraken CLI Work Item from Start to Finish

Start with `gk work start` when you want GitKraken CLI to initialize a shared task across every repository in the active workspace:

```
gk work start <name>
```

The `<name>` assigns a title to your work item. This initializes all repositories in your workspace and checks for any **pending commits, pull requests, or open work items.**

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-work.png" class="img-bordered img-responsive center" alt="Work item initialization in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Creating a work item initializes your workspace and checks for pending items.</figcaption>
</figure>

Review the workspace state with `gk work info` before committing or opening pull requests across the full work item:

```
gk work info
```

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-w-info.png" class="img-bordered img-responsive center" alt="Work info output in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Use <code>gk work info</code> to review changes across all repositories.</figcaption>
</figure>

### How to Commit Work Item Changes with AI

Use `gk work commit --ai` when you want GitKraken CLI to generate commit messages and commit staged changes across every repository in the work item:

```
gk work commit --ai
```

This command:

* Analyzes staged changes using AI.
* Generates context-aware commit messages.
* Commits changes across all repositories in the work item.

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-w-commit.png" class="img-bordered img-responsive center" alt="AI-generated commit in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">AI-generated commit messages help standardize your commit history.</figcaption>
</figure>

### How to Create Pull Requests for a Work Item with AI

Use `gk work pr create --ai` when you want GitKraken CLI to open pull requests for every repository included in the active work item:

```
gk work pr create --ai
```

This creates pull requests for **all** changes in the current work item with AI-generated messages. Use this command after you have reviewed the workspace state and committed the repositories that belong in the shared task.

### How to End and Clean Up a Work Item

Use `gk work end` when the shared task is complete and you want GitKraken CLI to close the work item and clean up temporary resources:

```
gk work end
```

This command cleans up your workspace and provides options to delete or retain local changes while removing temporary resources.

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
