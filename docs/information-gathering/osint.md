# OSINT & reconnaissance

## The concept

**Reconnaissance** is the first phase of understanding a target: gathering
information before any deeper assessment. **OSINT** — Open Source Intelligence —
is the part of that drawn from publicly available sources. The striking thing
for newcomers is how much can be learned without touching the target's systems
at all.

## Passive vs active reconnaissance

The key distinction:

- **Passive reconnaissance** gathers information **without directly interacting**
  with the target's systems. You're reading what's already public: company
  records, websites, public filings, employee profiles on professional networks,
  public breach-notification data. The target has no way to notice.
- **Active reconnaissance** involves **direct interaction** — probing systems,
  identifying services, fingerprinting what's running. It yields more, but it
  touches the target and can be detected, and it requires authorisation.

A tester typically starts passive (quiet, no authorisation footprint beyond the
engagement) and moves to active within the agreed scope.

## What open sources reveal

OSINT about an organisation can surface a surprising amount:

- **People** — names, roles, and contact patterns from professional networking
  sites, which reveal org structure and who does what.
- **Technology** — job adverts, public documents, and support forum posts often
  reveal what software and systems a company runs.
- **Exposed credentials** — public breach-notification services (such as the
  well-known "have I been pwned" style databases) indicate when an email address
  has appeared in a known data breach.
- **Infrastructure** — public records about domains and addresses (see
  [DNS enumeration](dns-enumeration.md)).

## Why it matters

Reconnaissance feeds everything that follows. From a defender's point of view,
it's a reminder that **your attack surface includes what your people and your
public footprint reveal**, not just your servers. An organisation can have
perfectly patched systems and still be exposed because its public information
makes targeting its people easy.

One of the most important realities here: information gathered passively about
people is frequently the *starting point* for social-engineering and
credential-focused attacks. That's why the defensive response is partly
technical and partly human.

!!! warning "Legal and ethical note"
    Even "just looking" has limits. Active reconnaissance requires authorisation
    — probing systems you don't own can be an offence (see
    [Legal & compliance](../assessment-management/legal-compliance.md)). And
    OSINT involving people must respect privacy and data-protection obligations.

## Remediation themes

Reducing what reconnaissance can find:

- **Manage your public footprint.** Be deliberate about what's published — in
  documents, job adverts, and on public profiles — about your technology and
  structure.
- **Monitor breach exposure.** Track whether corporate credentials appear in
  known breaches, and respond (forced resets, awareness).
- **Train people.** Since recon so often feeds attacks on people, awareness of
  phishing and social engineering is a core control.
- **Enforce multi-factor authentication.** It blunts the value of leaked or
  guessed credentials.

!!! note "Check your understanding"
    - What's the defining difference between passive and active reconnaissance,
      and why does it matter for authorisation?
    - Name three things OSINT can reveal about an organisation without touching
      its systems.
    - Why is reducing a company's public information footprint a security
      control, not just a privacy one?
