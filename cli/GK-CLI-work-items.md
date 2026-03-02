---
title: Work Items
description: Learn how to take action on multiple repos at once with Work Items.
taxonomy:
    category: cli
---

<kbd>Last updated: March 2026</kbd> 

## Managing Work Items with GitKraken CLI

The `gk work` command suite provides a unified workflow for managing a work item throughout its lifecycle—from task initiation to cleanup. This command streamlines development tasks, enhancements, and bug fixes by automating actions like branch creation, committing changes, pull request creation, and workspace cleanup.

With the power of AI, `gk work` also enables automatic generation of commit messages and pull requests without leaving the terminal.

***

## Quick Start

To manage a work item across multiple repositories using GitKraken CLI:

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

All `gk work` commands execute in parallel across every repository in the active workspace. An authenticated GitKraken account with a configured organization is required to use AI-generated commit messages and pull requests.

## Boost Efficiency with Parallel Execution

Execute commands across multiple repositories in parallel to complete tasks faster and more efficiently.

***

## Example Workflow

To create a work item, use:

```
gk work start <name>
```

The `<name>` assigns a title to your work item. This initializes all repositories in your workspace and checks for any **pending commits, pull requests, or open work items.**

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-work.png" class="img-bordered img-responsive center" alt="Work item initialization in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Creating a work item initializes your workspace and checks for pending items.</figcaption>
</figure>

To view pending changes:

```
gk work info
```

<figure style="text-align: center">
  <img src="/wp-content/uploads/gk-cli-w-info.png" class="img-bordered img-responsive center" alt="Work info output in GitKraken CLI">
  <figcaption style="color:#888; text-align:center">Use <code>gk work info</code> to review changes across all repositories.</figcaption>
</figure>

### Committing Changes with AI

Use AI to generate commit messages and commit changes in parallel:

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

### Creating a Pull Request with AI

Generate pull requests using:

```
gk work pr create --ai
```

This creates pull requests for **all** changes in the current work item with AI-generated messages, streamlining collaboration and review.

### Finalizing a Work Item

When your work is complete, end the work item with:

```
gk work end
```

This command cleans up your workspace and provides options to delete or retain local changes while removing temporary resources.

<style>
pre{position:relative}
.copy-btn{position:absolute;top:8px;right:8px;display:flex;align-items:center;justify-content:center;width:28px;height:28px;padding:0;background:rgba(128,128,128,.12);border:1px solid rgba(128,128,128,.2);border-radius:4px;cursor:pointer;color:#999;opacity:0;transition:opacity .15s,background .15s,color .15s}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.25);color:#555}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.3)}
</style>
<script>(function(){var C='<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path></svg>',K='<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>';function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.innerHTML=C;p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.innerHTML=K;b.classList.add('copied');setTimeout(function(){b.innerHTML=C;b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
