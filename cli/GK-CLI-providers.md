---
title: How to Connect Providers in GitKraken CLI
description: Connect GitHub, GitLab, Bitbucket, Azure DevOps, Jira, Linear, Trello, and self-hosted instances to GitKraken CLI, sync integrations from your GitKraken account, and manage more than one account per provider.
product: "GitKraken CLI"
feature: "Providers and Integrations"
content_type: "how-to"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
os_support: [Windows, macOS, Linux]
integrations: [github, github-enterprise, gitlab, gitlab-self-managed, bitbucket, bitbucket-data-center, azure-devops, jira, jira-data-center, linear, trello]
llms_include: true
tags: [providers, integrations, sync, personal-access-token, self-hosted, multiple-accounts]
taxonomy:
    category: cli
custom_fields:
    nav_category: "gk-cli-providers"
    nav_label: "How to Connect Providers in GitKraken CLI"
    nav_order: 50
    nav_parent: ""
    page_type: "content"
---

<kbd>Last updated: October 2026</kbd>

GitKraken CLI uses your provider connections to list pull requests and issues, open pull requests, and give AI coding agents access to your work. If you already connected GitHub, Jira, or other integrations in GitKraken Desktop, GitLens, or gitkraken.dev, you can reuse them in the CLI with one command.

This page shows you how to sync, add, and manage provider connections, including self-hosted instances and more than one account per provider. For every flag, see the [`gk provider` command reference](https://gitkraken.github.io/gk-cli/docs/gk_provider.html).

## Requirements

To connect providers, you need the following:

- **Account:** sign in with `gk auth login`.
- **Organization:** set your organization with `gk organization set <ORG_NAME>` before you sync.
- **Multiple accounts:** connecting more than one account to the same provider requires a paid plan.

The following table lists the providers GitKraken CLI supports and the name to use in commands:

| Provider | Name in commands | Use for |
| --- | --- | --- |
| GitHub | `github` | Pull requests and issues |
| GitHub Enterprise | `github_enterprise` | Pull requests and issues |
| GitLab | `gitlab` | Pull requests and issues |
| GitLab Self-Managed | `gitlab_self_hosted` | Pull requests and issues |
| Bitbucket | `bitbucket` | Pull requests |
| Bitbucket Server and Data Center | `bitbucket_server` | Pull requests |
| Azure DevOps | `azure` | Pull requests and issues |
| Jira | `jira` | Issues |
| Jira Server and Data Center | `jira_server` | Issues |
| Linear | `linear` | Issues |
| Trello | `trello` | Issues |

***

## How to Sync Integrations from Your GitKraken Account

If you connected integrations in GitKraken Desktop, GitLens, or gitkraken.dev, sync them to GitKraken CLI:

```
gk provider list --sync
```

GitKraken CLI lists each connected provider. Run this command again any time you connect a new integration in another GitKraken product.

<!-- Screenshot needed: terminal output of gk provider list --sync showing connected providers such as GitHub and Jira. -->

***

## How to Add a Provider

To connect a cloud provider such as GitHub, GitLab, Bitbucket, Azure DevOps, Jira, Linear, or Trello, run `gk provider add` with the provider name:

```
gk provider add github
```

GitKraken CLI opens your browser so you can sign in to the provider and approve access.

### How to Add a Provider with a Personal Access Token

You can connect with a personal access token instead of signing in through your browser. For example:

```
gk provider add github -t <TOKEN>
```

Some providers need more details with a token:

- **Jira:** add `--email <EMAIL>` and `--jira-organization <JIRA_ORGANIZATION>`.
- **Bitbucket:** add `--email <EMAIL>`. Your token needs the `read:pullrequest:bitbucket` and `write:pullrequest:bitbucket` scopes.
- **Trello:** add `--key <API_KEY>`. A Trello token connection stays on the computer where you add it. To sync Trello across your computers, connect without a token instead.
- **Azure DevOps:** tokens aren't supported. Connect through your browser instead.

GitKraken CLI checks your token with the provider before it saves it. To skip this check, add `--no-verify`.

### How to Add a Self-Hosted Provider

To connect GitHub Enterprise, GitLab Self-Managed, Bitbucket Server and Data Center, or Jira Server and Data Center, use a personal access token and your instance URL:

```
gk provider add gitlab_self_hosted -t <TOKEN> --url <INSTANCE_URL>
```

***

## How to Connect More Than One Account to a Provider

If you work with more than one account on the same provider, such as a personal and a work GitHub account, you can connect both. To add another account without replacing the current one, add `--additional`:

```
gk provider add github --additional
```

This feature requires a paid plan.

When you have more than one connection, GitKraken CLI uses the primary connection by default. To manage your connections:

1. List your connections and their IDs:
   ```
   gk provider list
   ```
2. Set the connection you want to use by default:
   ```
   gk provider primary github <TOKEN_ID>
   ```

To use a different connection for one command, add `--connection <TOKEN_ID>` to `gk pr list` or `gk issue list`.

***

## How to Find Organizations, Projects, and Repositories

Some commands need the name of an organization, project, or repository on your provider. To look these up, use the following commands:

- `gk provider orgs` lists your organizations or workspaces.
- `gk provider projects` lists projects, such as Azure DevOps projects.
- `gk provider repos` lists repositories.

For the options each command needs, see the [`gk provider` command reference](https://gitkraken.github.io/gk-cli/docs/gk_provider.html).

***

## How to Remove a Provider

To remove a provider and all its connections, run:

```
gk provider remove github
```

To remove one connection only, add `--connection <TOKEN_ID>`. To skip the confirmation prompt, add `--force`.

> **Note:** As of GitKraken CLI 3.1.74, `--yes` is deprecated. Use `--force` instead.
