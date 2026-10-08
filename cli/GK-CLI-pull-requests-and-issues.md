---
title: How to Track Pull Requests and Issues in GitKraken CLI
description: List your pull requests and issues from GitHub, GitLab, Bitbucket, Azure DevOps, Jira, Linear, and Trello in your terminal with GitKraken CLI, then view, filter, and assign them.
product: "GitKraken CLI"
feature: "Pull Requests and Issues"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

With GitKraken CLI, you can check the pull requests waiting on you and the issues assigned to you without opening a browser. One command can show work from every provider you've connected, such as your GitHub pull requests and your Jira tickets together. If you use Launchpad in GitLens or GitKraken Desktop, this gives you a similar view in your terminal.

This page shows you how to list, filter, view, and assign pull requests and issues. For every flag, see the [`gk pr`](https://gitkraken.github.io/gk-cli/docs/gk_pr.html) and [`gk issue`](https://gitkraken.github.io/gk-cli/docs/gk_issue.html) command references.

## Requirements

To list pull requests and issues, you need the following:

- **Account:** sign in with `gk auth login`.
- **Connected providers:** connect at least one Git provider or issue tracker. To learn how, see [How to Connect Providers in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-providers/).

The following table lists the providers each command supports:

| Command | Supported providers |
| --- | --- |
| `gk pr list` | GitHub, GitHub Enterprise, GitLab, GitLab Self-Managed, Bitbucket, Bitbucket Server and Data Center, Azure DevOps |
| `gk issue list`, `gk issue show`, `gk issue assign` | GitHub, GitHub Enterprise, GitLab, GitLab Self-Managed, Jira, Jira Server and Data Center, Azure DevOps, Linear, Trello |

***

## How to See Your Pull Requests

To list the open pull requests you authored or are assigned to on one provider, run `gk pr list` with the provider name:

```
gk pr list github
```

To see pull requests from every Git provider you've connected, run:

```
gk pr list --all
```

<!-- Screenshot needed: terminal output of gk pr list --all showing open pull requests from more than one provider. -->

Use the following options to change what you see:

- **To include pull requests waiting for your review,** add `--reviewer`.
- **To see closed and merged pull requests,** add `--closed`.
- **To see every pull request in one repository,** add `--org <ORG> --repo <REPO> --all-involvement`. For Azure DevOps, also add `--project <PROJECT>`.
- **To get the latest data,** add `--sync`. GitKraken CLI caches results for a short time, so `--sync` skips the cache.

For Bitbucket and Azure DevOps, GitKraken CLI first looks for the repository in your current folder. Outside a matching repository, it lists your pull requests across your Bitbucket workspaces or Azure DevOps organizations.

To create a pull request from your current branch with an AI-written title and description, see [How to Use AI Features in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-ai-features/).

***

## How to See Your Issues

To list the open issues assigned to you on one provider, run `gk issue list` with the provider name:

```
gk issue list jira
```

To see issues from every issue tracker you've connected, run:

```
gk issue list --all
```

Use the following options to filter the list:

- **To see issues assigned to anyone,** add `--all-assignees`.
- **To see issues with no assignee,** add `--unassigned`.
- **To see issues assigned to a teammate,** add `--assigned-to <USER>`.
- **To see closed issues,** add `--closed`.
- **To filter Jira issues,** add `--project <PROJECT_KEY>` and `--issue-type <TYPE>`, such as `Bug`.
- **To filter GitHub issues,** add `--org <ORG>` and `--repo <REPO>`.

For example, to list unassigned bugs in a Jira project, run:

```
gk issue list jira --unassigned --project <PROJECT_KEY> --issue-type Bug
```

***

## How to View an Issue

To see the details of one issue, including closed or unassigned issues, run `gk issue show` with the provider and the issue ID. For Jira, Linear, and Trello, the ID or key is enough:

```
gk issue show jira <ISSUE_KEY> --with-comments
```

For GitHub and GitLab, add the organization and repository. For Azure DevOps, add the organization and project:

```
gk issue show github <ISSUE_NUMBER> --organization-name <ORG> --repo-name <REPO>
```

The `--with-comments` flag adds the issue's comments.

***

## How to Assign an Issue

To assign an issue to someone, run `gk issue assign` with the provider and the issue ID. For GitHub and GitLab, use the person's username. For Jira and Azure DevOps, use their email:

```
gk issue assign github -i <ISSUE_NUMBER> -n <USERNAME> -o <ORG> -r <REPO>
```

***

## How to Work with More Than One Account

If you connected more than one account for the same provider, GitKraken CLI uses your primary connection by default. To list pull requests or issues for a different connection, add `--connection <TOKEN_ID>`. To find connection IDs, run `gk provider list`. To learn more, see [How to Connect Providers in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-providers/).

To use these lists in scripts, add `--json`. To learn more, see [How to Script GitKraken CLI with JSON Output](https://help.gitkraken.com/cli/GK-CLI-json-output/).

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
