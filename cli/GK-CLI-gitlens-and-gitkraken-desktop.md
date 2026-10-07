---
title: How GitKraken CLI Works with GitLens and GitKraken Desktop
description: Learn how GitLens and GitKraken Desktop use GitKraken CLI behind the scenes to run the GitKraken MCP server and show live AI agent sessions, and how to check or turn off each connection.
product: "GitKraken CLI"
feature: "GitLens and GitKraken Desktop Integration"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

If you use GitLens or GitKraken Desktop, GitKraken CLI (`gk`) may already be working for you. GitLens uses it to give your AI assistant GitKraken tools. GitKraken Desktop, GitLens, and [Kepler ADE by GitKraken](https://help.gitkraken.com/kepler/kepler-getting-started/) use it to show what your AI coding agents are doing. This page explains what you see in each product, what `gk` does behind the scenes, and how to check or turn off each connection.

GitLens runs in VS Code, Cursor, Windsurf, Trae, and Kiro. Everything on this page about GitLens applies to all of these editors.

## Requirements

The connections on this page depend on the following:

- **GitLens:** the GitLens tools that an AI assistant can call need GitLens 17.10.0 or later.
- **Account:** most GitKraken MCP tools need you to be signed in to your GitKraken account.
- **Same computer:** GitKraken CLI connects to GitKraken Desktop, GitLens, and Kepler only when they run on the same computer.

***

## What GitKraken CLI Does in Each Product

The following table summarizes what you see in each product and what GitKraken CLI does behind the scenes:

| What you see | Where | What GitKraken CLI does |
| --- | --- | --- |
| A GitKraken MCP server in your editor's AI chat | GitLens | Runs the GitKraken MCP server (`gk mcp`), which gives your AI assistant Git, pull request, and issue tools |
| Your AI assistant opens Launchpad, starts work on an issue, or starts a pull request review in GitLens | GitLens | Finds the GitLens window for your repository and asks it to open that view |
| Live status for your AI agent sessions, such as the current tool and prompt | GitKraken Desktop, GitLens, and Kepler | Receives events from AI agent hooks and passes them to the app |
| Approve or deny an agent's tool request from the app, when the app supports it | GitKraken Desktop, GitLens, and Kepler | Holds the agent's request until you decide in the app, then returns your decision to the agent |

***

## How GitLens Uses GitKraken CLI for the GitKraken MCP Server

The GitKraken MCP server lets AI assistants such as GitHub Copilot, Cursor, and Claude work with your repositories, pull requests, and issues through GitKraken. For example, you can ask your assistant "What issues are assigned to me?" and it uses your connected GitHub, Jira, or other integrations to answer.

GitLens installs the GitKraken MCP server for you:

- **VS Code:** if your version of VS Code supports it, GitLens installs the server automatically.
- **Cursor, Windsurf, Trae, and Kiro:** open the Command Palette, run **GitLens: Install MCP Server**, and follow the prompts.

Behind the scenes, GitLens installs GitKraken CLI and runs `gk mcp install` for your editor. That command adds a **GitKraken** entry to your editor's MCP settings. When your AI assistant starts the server, it runs `gk mcp`.

When an MCP tool needs you to sign in or connect an integration, it opens GitLens so you can finish in your editor.

<!-- Screenshot needed: VS Code with GitLens, the Copilot Chat panel in Agent mode, showing the GitKraken MCP server tools enabled and a response to "What issues are assigned to me?" -->

To learn more about the GitKraken MCP server and its tools, see the [GitKraken MCP documentation](https://help.gitkraken.com/mcp/mcp-getting-started/). To install the server in other AI tools, see [How to Use GitKraken CLI with AI Coding Agents](https://help.gitkraken.com/cli/gk-cli-mcp/).

### How Your AI Assistant Works with an Open GitLens Window

When GitLens is open, the GitKraken MCP server can hand work to it. Your AI assistant can do the following:

- Show your Launchpad list of pull requests and issues.
- Start work on an issue in GitLens.
- Start a review of a pull request in GitLens.

GitKraken CLI finds the GitLens window that has your repository open and sends the request to it over a local connection.

***

## How GitKraken Desktop, GitLens, and Kepler Show Your AI Agent Sessions

GitKraken Desktop, GitLens, and Kepler can show live status for AI coding agents, such as Claude Code, Cursor, Codex, and GitHub Copilot CLI. Kepler, GitKraken's agentic development environment (ADE), uses these updates to show your agent sessions as they run. You can see the following details for each session:

- Whether the agent is working, idle, or waiting for you.
- The prompt you gave the agent and the tool it's using.
- Subagents and the files the agent changed.

When the app supports it, you can also approve or deny an agent's permission request from the app.

<!-- Screenshot needed: GitKraken Desktop (or GitLens) showing a live AI agent session with its status, current tool, and prompt. -->

GitKraken CLI makes this work with hooks. A hook is a small command that an AI agent runs when something happens, such as a session starting, a prompt being submitted, or a tool being used. GitKraken CLI installs a hook in the agent's settings. For Claude Code, it installs a `gitkraken-hooks` plugin. Each time the hook runs, `gk` does the following:

1. Saves the session update in a local cache on your computer.
2. Sends the update to GitKraken Desktop, GitLens, or Kepler running on the same computer.
3. For a permission request that the app handles, waits for your decision in the app and passes it back to the agent.

Hooks are available for Claude Code, OpenCode, Cursor, Codex, GitHub Copilot CLI, Antigravity, Pi, Augment, and Grok Build.

### What Data AI Agent Hooks Use

Hook data stays on your computer. GitKraken CLI sends it only to GitKraken apps running on the same computer and doesn't upload it to GitKraken.

Depending on the event, a session update can include the following:

- The prompt you gave the agent.
- The tool the agent is using and its arguments.
- The files the agent changed and the folders it worked in.
- The agent's model and session state.

Because session data can include prompts and file paths, treat it as sensitive. GitKraken CLI removes ended sessions from its local cache after 30 days.

***

## How to Check and Turn Off GitKraken CLI Connections

To see every AI agent GitKraken CLI knows about, whether the agent is on your computer, and whether the GitKraken MCP server and hooks are installed for it, run:

```
gk agents list
```

To stop sending an agent's events to GitKraken Desktop, GitLens, and Kepler, uninstall its hooks. Live session status for that agent stops working until you install the hooks again. For example, for Claude Code:

```
gk ai hook uninstall claude-code
```

To remove the GitKraken MCP server from an AI tool, run `gk mcp uninstall` with the tool's name. For example, for Cursor:

```
gk mcp uninstall cursor
```

To find the names to use, run `gk mcp install --list`. For every option, see the [`gk mcp uninstall` command reference](https://gitkraken.github.io/gk-cli/docs/gk_mcp_uninstall.html).

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
