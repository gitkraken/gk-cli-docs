---
title: How to Use GitKraken CLI with AI Coding Agents
description: Give Claude Code, Cursor, GitHub Copilot, Codex, and other AI coding agents GitKraken tools with GitKraken CLI by installing the GitKraken MCP server and GitKraken agent skills.
product: "GitKraken CLI"
feature: "AI Coding Agents and MCP"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

AI coding agents work better when they can see your pull requests and issues and use Git safely. GitKraken CLI gives agents such as Claude Code, Cursor, GitHub Copilot, and Codex access to GitKraken in two ways:

- **The GitKraken MCP server** gives your agent tools for Git, pull requests, and issues across your connected providers. For example, you can ask your agent "What issues are assigned to me?" or "Create a pull request for this branch."
- **GitKraken agent skills** teach your agent how to use GitKraken CLI, including its AI commit composer and AI conflict resolution.

This page shows you how to install both, check what's installed, and remove them. If you use GitLens in VS Code, Cursor, Windsurf, Trae, or Kiro, GitLens can install the GitKraken MCP server for you. To learn more, see [How GitKraken CLI Works with GitLens and GitKraken Desktop](https://help.gitkraken.com/cli/GK-CLI-gitlens-and-gitkraken-desktop/).

## Requirements

To give your agent GitKraken tools, you need the following:

- **GitKraken CLI:** install `gk` by following [How to Install and Set Up GitKraken CLI](https://help.gitkraken.com/cli/cli-home/).
- **Account:** sign in with `gk auth login`. Most GitKraken MCP tools need you to be signed in.
- **Connected providers:** connect the Git providers and issue trackers you want your agent to use. To learn how, see [How to Connect Providers in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-providers/).

The following table lists the AI tools GitKraken CLI supports and the name to use in commands:

| AI tool | MCP server name | Agent skills name |
| --- | --- | --- |
| Claude Code | `claude-cli` | `claude-cli` |
| Claude Desktop | `claude` | Not supported |
| Cursor | `cursor` | `cursor` |
| VS Code | `vscode` | Not supported |
| VS Code Insiders | `vscode-insiders` | Not supported |
| GitHub Copilot CLI | `copilot` | `copilot` |
| JetBrains Copilot | `jetbrains-copilot` | Not supported |
| Codex | `codex` | `codex` |
| Windsurf | `windsurf` | Not supported |
| Trae | `trae` | Not supported |
| Kiro | `kiro` | Not supported |
| Zed | `zed` | Not supported |
| OpenCode | `opencode` | `opencode` |
| Antigravity | `antigravity` | `antigravity` |
| Antigravity CLI | `antigravity-cli` | `antigravity-cli` |
| Augment | Not supported | `augment` |
| Grok Build | Not supported | `grok` |
| Pi | Not supported | `pi` |

***

## How to Install the GitKraken MCP Server

To install the GitKraken MCP server in an AI tool, run `gk mcp install` with the tool's name. For example, for Claude Code:

```
gk mcp install claude-cli
```

GitKraken CLI adds a **GitKraken** entry to the tool's MCP settings. The next time your agent starts, it can use GitKraken tools.

You can also install the server in more than one tool at once:

- **To install in several tools,** list their names, for example `gk mcp install cursor claude-cli`.
- **To install in every AI tool on your computer,** run `gk mcp install --all`.
- **To see which tools GitKraken CLI supports and finds on your computer,** run `gk mcp install --list`.

If the GitKraken entry is already up to date, GitKraken CLI leaves it alone. If the entry is out of date, for example because `gk` moved, GitKraken CLI repairs it.

<!-- Screenshot needed: Claude Code (or Cursor) showing the GitKraken MCP server connected and its tools listed, after running gk mcp install. -->

### How to Limit Your Agent to Read-Only Tools

If you want your agent to read your repositories, pull requests, and issues without making changes, install the server in read-only mode:

```
gk mcp install claude-cli --readonly
```

In read-only mode, the server doesn't offer tools that commit, push, create pull requests, or create issues. To turn read-only mode off later, run the install again with `--readonly=false`.

To learn about every GitKraken MCP tool and how to use it, see the [GitKraken MCP documentation](https://help.gitkraken.com/mcp/mcp-getting-started/).

***

## How to Install GitKraken Agent Skills

Agent skills are instructions that your AI agent loads when a task needs them. GitKraken CLI includes the following skills:

- **gitkraken-cli:** helps your agent sign in, connect providers, list pull requests and issues, and write commit messages, changelogs, and pull request descriptions with `gk`.
- **gitkraken-commit-composer:** helps your agent turn mixed changes into clean commits with `gk ai compose`.
- **gitkraken-resolve:** helps your agent resolve merge conflicts with `gk ai resolve`.

To install all three skills for an AI tool, run `gk ai skill install` with the tool's name. For example, for Claude Code:

```
gk ai skill install claude-cli
```

To install only one skill, add `--skill <SKILL_NAME>`. To install skills in every AI tool on your computer, add `--all`.

By default, GitKraken CLI installs skills for your user account, so they work in every project. To add the skills to the current repository instead, so you can commit them and share them with your teammates, add `--scope project`.

When you update GitKraken CLI, update your installed skills to match:

```
gk ai skill update --all
```

To check whether your skills are current, run `gk ai skill check <TOOL_NAME>`. GitKraken CLI never overwrites a skill file you edited unless you add `--force`.

***

## How to Check What's Installed

To see every AI agent GitKraken CLI knows about, run:

```
gk agents list
```

For each agent, the list shows whether it's on your computer, whether the GitKraken MCP server is installed, and whether GitKraken AI hooks are installed. To see only skills, run `gk ai skill list`.

***

## How to Remove the GitKraken MCP Server and Skills

To remove the GitKraken MCP server from an AI tool, run:

```
gk mcp uninstall claude-cli
```

To remove it from every AI tool, run `gk mcp uninstall --all`.

To remove GitKraken agent skills, run:

```
gk ai skill uninstall claude-cli
```

> **Note:** As of GitKraken CLI 3.1.75, you can no longer install the GitKraken MCP server in Gemini CLI. To remove an earlier install, run `gk mcp uninstall gemini`.

For every option, see the [`gk mcp`](https://gitkraken.github.io/gk-cli/docs/gk_mcp.html) and [`gk ai skill`](https://gitkraken.github.io/gk-cli/docs/gk_ai_skill.html) command references.

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
