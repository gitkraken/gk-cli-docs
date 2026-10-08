---
title: How to Script GitKraken CLI with JSON Output
description: Use GitKraken CLI in scripts, CI jobs, and AI agent workflows with JSON output, field filtering, structured errors, retry-aware exit codes, and named sessions.
product: "GitKraken CLI"
feature: "JSON Output and Scripting"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

GitKraken CLI can print machine-readable JSON, so you can use it in shell scripts, CI jobs, and AI agent workflows. For example, you can post your open pull requests to a team channel each morning, or let an agent read your assigned issues without parsing text tables.

This page explains how JSON output, errors, and exit codes work so your scripts can rely on them.

## Requirements

To script GitKraken CLI, you need the following:

- **GitKraken CLI 3.1.75 or later:** `--json` became a global flag in 3.1.75. To check your version, run `gk version`.
- **Account:** most commands that read from your providers need you to sign in with `gk auth login`.
- **A JSON tool (optional):** the examples on this page use [jq](https://jqlang.org/) to read JSON.

***

## How to Get JSON Output

Add `--json` to a command to print a single JSON document:

```
gk pr list --all --json
```

To turn on JSON output for every command in your terminal session or CI job, set the `GK_OUTPUT` environment variable to `json`.

In JSON mode, GitKraken CLI prints only the JSON document to standard output (stdout). Warnings, progress messages, and other human-readable text go to standard error (stderr). This means you can pipe the output straight into another tool:

```
gk issue list jira --json | jq .
```

GitKraken CLI doesn't print color codes in JSON mode, or when the output isn't going to a terminal.

> **Note:** As of GitKraken CLI 3.1.75, `--output json` is deprecated. Use `--json` instead.

***

## How to Keep Only the Fields You Need

List commands, such as `gk pr list`, `gk issue list`, and `gk ai skill list`, accept `--fields` to keep only the fields you name. This keeps the output small, which saves context when an AI agent reads it:

```
gk pr list github --json --fields id,title,state
```

The `--fields` flag works only with `--json`. GitKraken CLI drops an unknown field name with a warning. If every field name is unknown, the command fails and lists the valid field names.

***

## How to Handle Errors and Exit Codes

GitKraken CLI uses the following exit codes so your scripts know whether to retry:

| Exit code | Meaning | What to do |
| --- | --- | --- |
| `0` | Success | Continue. |
| `1` | Permanent failure, such as a sign-in, validation, or internal error | Fix the problem. Don't retry the same command. |
| `75` | Temporary failure, such as a network error or timeout | Retry the command. |

In JSON mode, an error prints a single JSON object to stderr, and stdout stays empty. The object includes an error `code`, a `message`, and a `retryable` value. The following error codes are the most useful in scripts:

- `auth_required`: your sign-in is missing or expired. Run `gk auth login`, then try again.
- `credits_exhausted`: your organization is out of GitKraken AI credits. The message explains how to add credits or who to contact.
- `invalid_request`: the command or its input is invalid. Fix the command before you run it again.

When GitKraken CLI runs another program for you, it exits with that program's exit code instead.

***

## How to Spot Deprecated Commands in Scripts

When you run a deprecated command, GitKraken CLI prints a warning to stderr. In JSON mode, it adds a top-level `deprecation` field to the JSON result instead. Check for this field in your scripts so you can update them before the command is removed.

***

## How to Preview Changes Before You Make Them

Some commands that change things accept `--dry-run`. With `--dry-run`, GitKraken CLI checks the command and shows what it would do without doing it. For example:

```
gk ai skill install claude-cli --dry-run
```

***

## How to Run Separate Sessions

By default, GitKraken CLI shares one sign-in and cache across your terminal sessions. To keep a separate sign-in and cache, for example for a CI job or a different GitKraken account, add `--session <NAME>` to each command:

```
gk auth login --session ci
gk pr list --all --json --session ci
```

To turn off telemetry in scripts and CI, see [GitKraken CLI Security and Data Storage Information](https://help.gitkraken.com/cli/CLI-Security/).

<style>
pre{position:relative;min-height:3.5em}
.copy-btn{position:absolute;top:8px;right:8px;padding:2px 8px;font-size:11px;font-family:sans-serif;background:rgba(128,128,128,.15);border:1px solid rgba(128,128,128,.25);border-radius:4px;cursor:pointer;color:#aaa;opacity:0;transition:opacity .15s,background .15s,color .15s;line-height:1.5;z-index:1}
pre:hover .copy-btn{opacity:1}
.copy-btn:hover{background:rgba(128,128,128,.3);color:#ddd}
.copy-btn.copied{color:#22c55e;border-color:rgba(34,197,94,.4)}
</style>
<script>(function(){function cp(t){if(navigator.clipboard&&window.isSecureContext)return navigator.clipboard.writeText(t);var x=document.createElement('textarea');x.value=t;x.style.cssText='position:fixed;opacity:0';document.body.appendChild(x);x.select();try{document.execCommand('copy')}catch(e){}document.body.removeChild(x);return Promise.resolve()}function init(){document.querySelectorAll('pre').forEach(function(p){if(p.querySelector('.copy-btn'))return;var b=document.createElement('button');b.className='copy-btn';b.setAttribute('aria-label','Copy code');b.textContent='Copy';p.appendChild(b);b.addEventListener('click',function(){var el=p.querySelector('code')||p;cp(el.innerText.replace(/\n$/,'')).then(function(){b.textContent='Copied!';b.classList.add('copied');setTimeout(function(){b.textContent='Copy';b.classList.remove('copied')},2000)})})})}document.readyState==='loading'?document.addEventListener('DOMContentLoaded',init):init()})()</script>
