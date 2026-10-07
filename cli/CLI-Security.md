---
title: GitKraken CLI Security and Data Storage Information
description: Review what GitKraken CLI cloud-connected features store, how data is encrypted in transit and at rest, what stays on your computer, and how to turn off telemetry.
product: "GitKraken CLI"
feature: "Security Information"
content_type: "security"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-10"
taxonomy:
    category: cli
---

<kbd>Last updated: October 2026</kbd>

This page explains what data GitKraken CLI cloud services store, how GitKraken encrypts that data in transit and at rest, and where GitKraken hosts it. It also covers what GitKraken CLI keeps only on your computer and how to turn off telemetry. Use this page if you're a developer, admin, or security reviewer evaluating GitKraken CLI.

## Requirements and scope

This page covers the following:

- **Product scope:** GitKraken CLI features that connect to GitKraken cloud services, plus data GitKraken CLI stores on your computer.
- **Out of scope:** local Git commands that don't use GitKraken cloud features.
- **Audience:** developers, admins, and security reviewers.
- **Security focus:** the data collected, encryption in transit, storage location, and encryption at rest.

## What GitKraken CLI cloud services store

The following table lists each GitKraken cloud service, the data it stores, and how GitKraken protects that data. All services encrypt data in transit with Transport Layer Security (TLS) and encrypt data at rest with the Advanced Encryption Standard (AES) using 256-bit keys.

| Service | Data collected | Security in transit | Storage location | Security at rest |
| --- | --- | --- | --- | --- |
| Workspaces and Insights | Repository metadata, issues, and pull requests | Encrypted with TLS | MongoDB Atlas | Encrypted with AES-256 |
| Teams and users | Repository-relative file paths, number of lines changed, name of the checked-out branch, and first commit SHA of the repository | Encrypted with TLS | MongoDB Atlas | Encrypted with AES-256 |
| Subscriptions | Billing metadata such as last four digits, name, payment type, ZIP code, country, and card type | Encrypted with TLS | MongoDB Atlas | Encrypted with AES-256 |
| Launchpad | Metadata for issues, pull requests, and URLs | Encrypted with TLS | Postgres (Amazon RDS) | Encrypted with AES-256 |
| Cloud Patches | Patch metadata, such as repository, provider, and base branch, plus patch content | Encrypted with TLS | Metadata in Postgres, content in Amazon S3 | Encrypted with AES-256 (Amazon S3 server-side encryption, SSE-S3) |

## What GitKraken CLI keeps on your computer

Some GitKraken CLI data never leaves your computer:

- **AI agent session data:** when you install AI hooks for an agent such as Claude Code, GitKraken CLI saves each agent session in a local cache on your computer. It passes session updates only to GitKraken apps, such as GitKraken Desktop, GitLens, and Kepler, running on the same computer. Session data can include your prompts, the tools the agent uses and their arguments, and the files the agent changes. GitKraken CLI removes ended sessions from the cache after 30 days.
- **Saved AI plans:** when you save a plan from `gk ai compose` or `gk ai resolve` to a file, the file can contain source code. On macOS and Linux, GitKraken CLI creates it so only your user account can read it. Delete these files when you no longer need them.

## Where AI requests go

By default, GitKraken CLI sends AI requests to GitKraken AI. If you add your own provider with `gk ai provider add`, such as OpenAI, Anthropic, OpenRouter, or a local Ollama model, GitKraken CLI sends your AI requests to that provider with your API key. GitKraken CLI still downloads its prompt templates from GitKraken, so you need to stay signed in. To learn more, see [How to Use AI Features in GitKraken CLI](https://help.gitkraken.com/cli/GK-CLI-ai-features/).

## How to Turn Off GitKraken CLI Telemetry

GitKraken CLI sends usage telemetry and error reports to GitKraken to help improve the product. You can turn this off in any of the following ways:

- To turn off telemetry for one command, add the `--no-telemetry` flag:
  ```
  gk pr list github --no-telemetry
  ```
- To turn off telemetry for every command, set the `GK_CLI_NO_TELEMETRY` environment variable to `1` or `true`.
- To use the OpenTelemetry standard setting, set the `OTEL_SDK_DISABLED` environment variable to `true`.
