# Aniis status

Public status page for [aniis.ai](https://aniis.ai), published at
**[status.aniis.ai](https://status.aniis.ai)**.

Built on [Upptime](https://upptime.js.org) — the checks run as GitHub Actions, the
history is committed to this repo, and the page is served from GitHub Pages.

## Why it lives here and not on our own infrastructure

A status page hosted on the infrastructure it monitors is useless at the one
moment it matters. This repo runs entirely on GitHub, which is a different
failure domain from our AWS account, our Render services and our DNS.

## ⚠️ This repository must stay public

Upptime checks every five minutes — roughly **8,600 workflow runs a month**.

- **Public repo:** GitHub Actions minutes are unlimited. The status page is free
  and cannot affect anything else.
- **Private repo:** those runs bill against the organisation's 2,000 free monthly
  minutes — the same budget that ran dry on 30 July 2026 and took CI down until
  the 1 August reset. Making this repo private would take out the status page and
  the main repo's CI together.

There is nothing sensitive here: the monitored URLs are public hostnames, and
`admin.aniis.ai` is deliberately **not** monitored.

## What is checked

| Site      | URL                                        | Note                                                            |
| --------- | ------------------------------------------ | --------------------------------------------------------------- |
| Aniis     | `https://aniis.ai`                         | Customer-facing web                                             |
| Aniis API | `https://aniis-api.onrender.com/v1/health` | Switches to `https://api.aniis.ai/v1/health` at the AWS cutover |

The API check points at Render's hostname for now because `api.aniis.ai` resolves
to the AWS ALB, whose ECS services are scaled to 0 and answer 503. Monitoring the
customer-facing hostname is the end state — it catches DNS and certificate
failures too, not just application failures.

## When something goes down

Upptime opens a GitHub issue in this repo and assigns it, then closes it when the
site recovers. Watch this repo to get those as notifications.

## Configuration

Everything lives in [`.upptimerc.yml`](.upptimerc.yml). Full options:
<https://upptime.js.org/docs/configuration>.
