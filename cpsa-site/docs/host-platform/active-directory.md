# Active Directory

## The concept

**Active Directory (AD)** is Microsoft's directory service — the system that
manages users, computers, and resources across a Windows network. It provides
authentication (proving who you are), authorisation (deciding what you can do),
and central management of the whole environment. In most organisations running
Windows, AD *is* the identity backbone.

## Why it matters

Because AD controls identity and access across the entire environment, it's one
of the highest-value targets in any Windows network. Compromise of AD — and
especially of its most privileged accounts — can mean control of everything it
governs. Understanding how it's structured and secured is essential for anyone
assessing or defending Windows estates.

## How AD is organised

A few core ideas worth knowing:

- **Domains, trees, and forests.** A **domain** is a management boundary; multiple
  domains can form a **tree**, and one or more trees form a **forest** (the
  top-level security boundary).
- **Domain controllers (DCs).** The servers that run AD, authenticate users, and
  hold the directory. They are critical infrastructure — compromise of a DC is
  compromise of the domain.
- **The Global Catalog.** A distributed index that lets users and applications
  search for objects across the whole forest, and supports logon in multi-domain
  environments.
- **Group Policy.** The mechanism for pushing configuration and security settings
  to users and computers across the domain — powerful for enforcing security, and
  worth protecting because of that power.

## FSMO roles

AD distributes certain special, single-holder responsibilities called **FSMO
(Flexible Single Master Operations) roles**, to avoid conflicts in a distributed
system. You don't need deep operational knowledge, but recognise that they exist
and that they matter:

| Role | Scope | Responsibility (in brief) |
|---|---|---|
| Schema Master | Forest | Controls changes to the AD schema |
| Domain Naming Master | Forest | Manages adding/removing domains |
| RID Master | Domain | Allocates identifiers for new objects |
| PDC Emulator | Domain | Time sync, password handling, and more |
| Infrastructure Master | Domain | Maintains cross-domain object references |

The security point: these roles are powerful, so the accounts and systems that
hold or manage them need to be tightly controlled.

## Why AD is a target

AD concentrates immense value in one system of systems:

- It holds **credentials and the keys to authentication** for the whole
  environment.
- Its **privileged groups** (domain administrators and similar) are the crown
  jewels — control them and you control the domain.
- It's the natural pivot for [lateral movement](../exploitation-concepts/post-exploitation.md):
  an attacker who understands AD can use it to spread.

This is why AD security is a specialism in its own right, and why even
foundational assessors should understand its shape.

## Defensive themes

- **Least privilege for administration.** Tightly limit who holds privileged
  roles; separate everyday accounts from administrative ones; use dedicated admin
  workstations.
- **Strong authentication.** Enforce strong password policies and multi-factor
  authentication, especially for privileged accounts.
- **Protect domain controllers.** Patch them promptly, restrict access, and treat
  them as the most critical systems in the estate.
- **Use Group Policy to enforce security** consistently — and guard the ability to
  change it.
- **Audit and monitor.** Log authentication and directory changes; watch for the
  signs of credential abuse and privilege changes.
- **Back up AD** and know how to recover it — resilience matters as much as
  prevention.

!!! note "Check your understanding"
    - What three things does Active Directory provide for a Windows network?
    - Why is a domain controller such a critical system to protect?
    - Why is AD such an attractive target, and which later attack phase does
      controlling it most enable?
