---
title: How to Use AI Features in GitKraken CLI
description: Use GitKraken CLI to write commit messages, turn messy changes into clean commits, resolve merge conflicts, explain branches, and create pull requests with AI, using GitKraken AI or your own AI provider.
product: "GitKraken CLI"
feature: "AI Features"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

GitKraken CLI brings AI help to the parts of Git that slow you down. You can write a commit message from your staged changes, split a pile of unrelated edits into clean commits, resolve merge conflicts, and draft a pull request, all without leaving your terminal. Each AI command shows you the result before it changes anything, so you stay in control.

This page shows you how to use each AI feature, choose a model, and use your own AI provider. For every flag, see the [`gk ai` command reference](https://gitkraken.github.io/gk-cli/docs/gk_ai.html).

## Requirements

To use AI features, you need the following:

- **Account:** sign in with `gk auth login`. You need to sign in even when you use your own AI provider, because GitKraken CLI downloads its prompts from GitKraken.
- **Organization:** set an organization with `gk organization set <ORG_NAME>`. GitKraken AI requests run under your active organization.
- **Plan:** AI-powered features require a paid plan such as Pro, Advanced, Business, or Enterprise.
- **AI credits:** GitKraken AI uses your organization's GitKraken AI credits. Your own AI provider doesn't use GitKraken AI credits.
- **Repository:** run each command inside a Git repository, or point to one with `--path` or `--workdir`.

The following table summarizes the AI commands:

| Command | Use it to | Changes your repository |
| --- | --- | --- |
| `gk ai commit` | Write a commit message for your staged changes and commit | Yes, after you confirm |
| `gk ai compose` | Group your changes into a series of clean commits | Only when you apply a plan |
| `gk ai resolve` | Propose and stage resolutions for merge conflicts | Only when you apply a plan |
| `gk ai explain` | Explain what a branch or commit changes | No |
| `gk ai changelog` | Write a changelog between two commits or branches | No |
| `gk ai pr create` | Write a pull request title and description and open the pull request | Opens a pull request, after you confirm |

***

## How to Write a Commit Message with AI

Stage your changes with `git add`, then run:

```
gk ai commit
```

GitKraken CLI reads your staged changes, writes a commit message, and shows it to you. Confirm to create the commit. To add a longer description under the commit message, add `--add-description`.

<!-- Screenshot needed: terminal output of gk ai commit showing the generated commit message and the "Do you want to proceed?" prompt. -->

***

## How to Turn Messy Changes into Clean Commits with AI

When you've changed several unrelated things at once, such as a bug fix, a rename, and a new test, `gk ai compose` sorts the changes into a series of focused commits. It works at the hunk level, so it can split the edits in a single file across more than one commit.

Compose works in three steps: plan, review, and apply.

1. Create a plan and save it to a file. This step doesn't change your repository:
   ```
   gk ai compose plan --plan-file plan.json
   ```
   GitKraken CLI prints one line for each proposed commit, with its message and how many files and lines it covers.
2. If the plan isn't what you want, run step 1 again with guidance. For example, to group commits by type of change, such as fixes, features, and tests, add `--direction type`. To give your own instructions, add `--direction custom --instructions "keep the API rename separate"`.
3. Apply the plan you reviewed:
   ```
   gk ai compose apply-plan plan.json
   ```
   Applying a saved plan doesn't call AI again, so it doesn't use AI credits.

Each apply returns an undo ID. To reverse the commits, run:

```
gk ai compose undo <UNDO_ID>
```

To list the undo IDs in your repository, run `gk ai compose undo --list`.

By default, compose reads all your staged, unstaged, and new files and writes the commits to your current branch. You can also compose only staged changes, rework the commits already on a branch, or split a branch into a stack of smaller branches. For these options, see the [`gk ai compose` command reference](https://gitkraken.github.io/gk-cli/docs/gk_ai_compose.html).

> **Tip:** `gk ai compose apply` creates a plan and applies it in one step, without a chance to review. Use it only when you don't need to see the plan first.

<!-- Screenshot needed: terminal output of gk ai compose plan listing the proposed commits with their messages, file counts, and line counts. -->

***

## How to Resolve Merge Conflicts with AI

When a merge, rebase, or cherry-pick stops with conflicts, `gk ai resolve` proposes a resolution for each conflicted file and explains its reasoning. It uses the same engine as the Resolve app in the GitKraken MCP server.

Resolve works in three steps: plan, review, and apply.

1. Create a plan and save it to a file. This step doesn't change your repository:
   ```
   gk ai resolve plan --plan-file resolve-plan.json
   ```
2. Review each proposed resolution in the plan, including its confidence and reasoning. To improve the proposal for one file, refine it with instructions:
   ```
   gk ai resolve refine-plan resolve-plan.json --file src/example.ts --instructions "keep both validation checks" --plan-file resolve-plan-v2.json
   ```
3. Apply the reviewed plan. GitKraken CLI writes the resolved files and stages them:
   ```
   gk ai resolve apply-plan resolve-plan-v2.json
   ```

Resolve never commits, pushes, or finishes the merge or rebase for you. After you apply the plan, run `git status`, check the result, and continue the merge or rebase yourself.

If your files change after you create a plan, applying it fails instead of writing the wrong content. Create a new plan and try again.

> **Note:** As of GitKraken CLI 3.1.74, running `gk ai resolve` on its own shows help instead of resolving conflicts. Use `gk ai resolve plan` and `gk ai resolve apply-plan`. The `--path` flag is replaced by `--workdir`.

Saved plans can contain your source code. Delete them when you no longer need them. For more options, such as resolving only some files or falling back to "ours" or "theirs" when AI can't resolve a file, see the [`gk ai resolve` command reference](https://gitkraken.github.io/gk-cli/docs/gk_ai_resolve.html).

***

## How to Explain a Branch or Commit with AI

Before you review or merge a branch, get a summary of what it changes compared with its base branch:

```
gk ai explain branch
```

To explain a single commit, run `gk ai explain commit`. Neither command changes your repository.

***

## How to Write a Changelog with AI

To write a changelog for a release, run `gk ai changelog` with the two branches or commits you want to compare:

```
gk ai changelog --base <BASE_BRANCH_OR_COMMIT> --head <HEAD_BRANCH_OR_COMMIT>
```

***

## How to Create a Pull Request with AI

When your branch is ready, push it, then run:

```
gk ai pr create
```

GitKraken CLI compares your branch with its base branch, writes a pull request title and description, and shows them to you. Confirm to open the pull request on your Git provider.

***

## How to Choose an AI Model

Every AI command accepts `--model` to use a specific model for that one run. It doesn't change your saved settings:

```
gk ai commit --model <MODEL_ID>
```

To see the GitKraken AI models you can use, run:

```
gk ai models
```

The default model is marked with `*`. To change the model GitKraken AI uses for every command, run `gk ai provider set gitkraken --model <MODEL_ID>`.

***

## How to Use Your Own AI Provider

If your team already pays for an AI provider, you can use your own API key with GitKraken CLI. GitKraken CLI supports OpenAI, Anthropic, OpenRouter, and Ollama for local models.

1. Add your provider and choose a model:
   ```
   gk ai provider add anthropic --key <API_KEY> --model <MODEL_ID>
   ```
2. If GitKraken CLI doesn't make the new provider active automatically, it tells you. To make it active, run:
   ```
   gk ai provider use anthropic
   ```
3. Check which provider and model are active:
   ```
   gk ai provider show
   ```

To switch back to GitKraken AI without removing your provider, run `gk ai provider use gitkraken`.

When you use your own provider, your AI requests go to that provider and don't use GitKraken AI credits. `gk ai resolve` needs a model that supports tool calling.

***

## How to Check Your AI Credit Usage

To see how many GitKraken AI tokens you've used, run:

```
gk ai tokens
```

When your organization runs out of GitKraken AI credits, AI commands stop and show a message:

- **If you're an organization admin,** the message includes a link to add credits.
- **If you're an organization member,** ask an organization admin to add credits.

To keep working while you wait, you can switch to your own AI provider.

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
