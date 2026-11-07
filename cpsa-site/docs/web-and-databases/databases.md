# Database security

## The concept

Databases hold the data that makes applications worth attacking — credentials,
personal information, financial records, intellectual property. Database security
is about protecting that data through access control, configuration, and sound
integration with the applications that use it.

## Why it matters

A database is often the ultimate target: the application is frequently just the
route to it. And databases are regularly exposed through a combination of
application weaknesses (like [injection](web-vulnerabilities.md)) and the
database's own misconfiguration. Understanding both sides is essential.

## Where database risk comes from

### Through the application

The most common route is the application layer. If an application builds queries
unsafely, **SQL injection** can let input reach the database in ways that read or
alter data it shouldn't. The fix lives largely in the application
(parameterised queries), but the database can limit the blast radius — see least
privilege below.

### Through direct exposure and configuration

Databases also suffer from problems of their own:

- **Default or weak credentials** on database accounts.
- **Excessive privileges** — application accounts granted far more access than
  they need, so any compromise is maximally damaging.
- **Network exposure** — a database reachable from places it never should be
  (e.g. directly from the internet).
- **Unencrypted data** — sensitive data stored or transmitted without
  encryption.
- **Missing patches** — unaddressed known vulnerabilities in the database
  software.

## Defensive principles

- **Least privilege.** Application accounts should have only the access they
  genuinely need — read where only reading is required, no administrative rights
  for routine work. This dramatically limits what any single compromise can do.
- **Strong authentication.** No default credentials; strong, well-managed
  passwords for database accounts.
- **Network segmentation.** Databases should be reachable only from the systems
  that must reach them, never exposed broadly.
- **Encrypt sensitive data**, both at rest and in transit.
- **Patch and maintain** the database software like any other critical system.
- **Secure the application layer**, since that's the most common route in — above
  all, parameterised queries to prevent injection.
- **Protect credentials at rest.** Where the database stores user passwords, they
  should be hashed with a purpose-built algorithm (see
  [Hashing & password storage](../core-technical/hashing.md)) — so that even if
  the data is exposed, the passwords aren't readily usable.

## The layered view

Database security is a good illustration of **defence in depth**: a well-secured
database limits the damage even when the application above it fails, and a
well-built application protects the database from most attacks in the first
place. Neither alone is enough; together they're resilient.

!!! note "Check your understanding"
    - Why is the principle of least privilege so powerful for limiting the impact
      of a database compromise?
    - What's the most common route through which databases are attacked, and
      where does the fix for it mainly live?
    - If a database is breached, what storage decision determines whether the
      user passwords inside are readily usable?
