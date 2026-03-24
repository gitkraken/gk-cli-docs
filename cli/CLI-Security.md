---

title: GitKraken CLI Security and Data Storage Information
description: Review what GitKraken CLI cloud-connected features store, how data is encrypted in transit and at rest, and which services send data to GitKraken-hosted systems.
product: "GitKraken CLI"
feature: "Security Information"
content_type: "security"
audience: "all"
plan_required: "all"
status: "GA"
last_verified: "2026-03"
taxonomy:
    category: cli

---

<kbd>Last updated: March 2026</kbd>

GitKraken CLI security information describes what GitKraken CLI cloud services store, how service data is encrypted in transit and at rest, and where that data is hosted. This page is for developers, admins, and security reviewers evaluating GitKraken CLI features such as Workspaces, Launchpad, Subscriptions, and Cloud Patches.

## Requirements and scope

- Product scope: GitKraken CLI cloud-connected features only
- Local-only workflows: local Git commands that do not use GitKraken cloud features are outside the scope of this page
- Audience: developers, admins, and security reviewers
- Security focus: data collected, transport encryption, storage location, and encryption at rest

## What GitKraken CLI cloud services store

| Service | Data collected | Security in transit | Storage location | Security at rest |
| --- | --- | --- | --- | --- |
| Workspaces/Insights | Repository metadata, issues, and pull requests | Encrypted with TLS | MongoDB Atlas | Encrypted at rest (AES-256) |
| Teams & Users | Repo-relative file paths, number of lines changed, name of branch currently checked out, first commit SHA of the repository | Encrypted with TLS | MongoDB Atlas | Encrypted at rest (AES-256) |
| Subscriptions | Billing metadata such as last four digits, name, payment type, ZIP code, country, and card type | Encrypted with TLS | MongoDB Atlas | Encrypted at rest (AES-256) |
| Launchpad | Metadata for issues, pull requests, and URLs | Encrypted with TLS | Postgres (RDS) | Encrypted at rest (AES-256) |
| Cloud Patches | Patch metadata such as repository, provider, and base branch, plus patch content | Encrypted with TLS | Patch metadata is stored in Postgres, and patch content is stored in AWS S3 | SSE-S3 with AES-256 |
