# Metadata & exposed data

## The concept

**Metadata** is "data about data" — information embedded inside files that isn't
part of their visible content. Documents, spreadsheets, PDFs, and images routinely
carry hidden details: who created them, what software and version produced them,
timestamps, and sometimes more. Organisations publish these files publicly
without realising what's travelling along inside them.

## What metadata can expose

Published files can quietly reveal:

- **Usernames and email addresses** of the people who authored them — which maps
  internal naming conventions and identifies real accounts.
- **Software and versions** used internally, which hints at what else might be
  running.
- **Internal paths and system names** embedded by the authoring software.
- **Location data**, in the case of some images with embedded GPS coordinates.

Individually these seem harmless. Collectively they help an outsider understand
an organisation's internal naming, technology, and people — the groundwork for
targeted attacks.

> *Example:* A document published on a company's website carries, in its
> metadata, the author's internal username. That single detail reveals the
> organisation's account-naming convention, which narrows down valid usernames
> across the estate.

## Search engines as a discovery tool

Search engines index far more than home pages. Using advanced search operators
(sometimes called "dorking"), it's possible to narrow results to, for example,
particular file types on a particular site, or pages containing particular
terms. Defenders should assume that **anything reachable and indexable will be
found** — so the control is to not expose it, not to hope no one looks.

This technique surfaces things like:

- Documents that were published without being intended for a wide audience.
- Exposed directory listings or backup files left on a web server.
- Login portals and administrative interfaces that were never meant to be easy
  to find.

## Why it matters

Metadata and inadvertently-exposed files are a reminder that an organisation's
attack surface includes **everything it has ever published**, not just its
current website. The information leaks are usually accidental and entirely
preventable — which is exactly why they make such reliable findings.

## Remediation themes

- **Strip metadata before publishing.** Use the "inspect document" / "remove
  personal information" features in office software, or an automated cleaning
  step in the publishing pipeline.
- **Standardise what gets published.** Have a process for what goes public and
  review it.
- **Avoid leaking internal naming** in public-facing content.
- **Prevent accidental exposure.** Disable directory listings, keep backups off
  web-accessible paths, and don't rely on obscurity for anything sensitive.
- **Search for your own exposure.** Periodically look for your organisation's
  files and sensitive paths the way an outsider would, and remediate what you
  find.

!!! note "Check your understanding"
    - Name three things that file metadata can reveal about an organisation.
    - Why is knowing one internal username potentially valuable to an attacker?
    - If a sensitive file is reachable but unlinked, why is "no one will find it"
      a poor control?
