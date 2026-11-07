# Service enumeration

## The concept

**Enumeration** is the step after discovery: now that you know a service is
running, you draw out detail from it — names, shares, configurations, versions.
Many services are designed to share information to function, and when they're
misconfigured they share far more than intended.

## Why it matters

Enumeration is where a bare list of open ports becomes genuine understanding.
Some services, when loosely configured, will volunteer usernames, network
structure, file shares, and configuration detail to anyone who asks — turning a
"found a service" into a meaningful finding without any exploitation at all.

## Services that commonly leak information

A few services are perennial enumeration targets because of what they expose
when misconfigured:

### SMB / NetBIOS (file sharing on Windows networks)

Used for file and resource sharing. Misconfigurations — particularly **shares
that allow anonymous or guest access** — can expose files, and sometimes those
files contain exactly the sort of thing that shouldn't be on an open share
(configuration, backups, credentials). Enumeration here is about discovering
which shares exist and what access they permit.

> *Example:* An assessor finds a file share reachable without authentication and
> discovers it contains a backup archive with sensitive contents. No
> exploitation was needed — the access control simply wasn't there.

### SNMP (network management)

The Simple Network Management Protocol lets devices be monitored and managed.
When left with **default or weak community strings** (effectively passwords), it
can reveal detailed device and system configuration — a rich source of
information about the environment.

### LDAP / directory services

Directory services underpin authentication and organisation-wide information. If
they permit **anonymous queries** or are otherwise loosely configured, they can
reveal user and group information and structure.

### Others

Many services — mail, databases, remote-access, and more — have their own
enumeration characteristics. The recurring pattern is the same: *a service that
trusts too much, or was never locked down from its defaults, tells you more than
it should.*

## The underlying theme

Almost every enumeration finding traces back to one of two root causes:

1. **Defaults left in place** — default credentials, default community strings,
   default "allow" configurations.
2. **Missing access control** — anonymous or guest access where authentication
   should be required.

Recognising that pattern is more valuable than memorising any single service's
quirks.

## Remediation themes

- **Remove anonymous and guest access** from file shares and directory services;
  require authentication.
- **Change default credentials and community strings**, everywhere, as a matter
  of routine.
- **Apply least privilege.** Services and accounts should expose and access only
  what they genuinely need.
- **Disable services you don't need.** The safest service is the one that isn't
  running.
- **Keep sensitive files off shared locations**, and review share permissions
  regularly.

!!! note "Check your understanding"
    - What two root causes sit behind most enumeration findings?
    - Why can an anonymous file share be a serious finding even without any
      "exploitation"?
    - Why are default SNMP community strings a problem, and what's the fix?
