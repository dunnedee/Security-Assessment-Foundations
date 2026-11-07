# DNS enumeration

## The concept

The **Domain Name System (DNS)** translates human-readable names
(`example.com`) into IP addresses and other records. Because DNS describes an
organisation's internet-facing infrastructure, it's a rich source of
information — both for legitimate assessment and, when misconfigured, for
attackers.

## Common DNS record types

A quick reference for the records you'll meet most:

| Record | Purpose |
|---|---|
| **A** / **AAAA** | Maps a name to an IPv4 / IPv6 address |
| **MX** | Identifies the mail servers for a domain |
| **NS** | Lists the authoritative name servers |
| **TXT** | Free-text records, often holding email-security policies (SPF, DKIM, DMARC) |
| **CNAME** | An alias pointing one name at another |
| **SOA** | Administrative information about the zone |

## What DNS enumeration reveals

By querying public DNS, an assessor can learn:

- **Subdomains**, which often map to distinct services (mail, VPN, admin
  portals, development environments). Each is a potential point of interest.
- **Mail infrastructure** via MX records.
- **Third-party services** an organisation uses, revealed by where its records
  point.
- **Email security posture**, from the presence (or absence) of SPF/DKIM/DMARC
  policies in TXT records.

Most of this is simply *public* — DNS is meant to answer these questions.

## The zone transfer misconfiguration

DNS has a legitimate mechanism — a **zone transfer (AXFR)** — for one name
server to replicate a full copy of a zone's records from another. It's meant to
be restricted to authorised secondary servers only.

When it's **misconfigured to allow anyone** to request it, a single query can
hand over the organisation's entire list of DNS records at once — every
subdomain and host the zone knows about. That turns a slow, piecemeal discovery
process into a complete map, and often exposes internal-sounding hosts
(`vpn.`, `admin.`, `dev.`) that were never meant to be advertised.

> *Example:* An assessor finds that a name server permits unrestricted zone
> transfers and retrieves the full set of records in one go — including
> subdomains pointing at administrative and remote-access services that broaden
> the attack surface.

This is a classic, well-known misconfiguration and a staple finding precisely
because it's both impactful and easy to fix.

## Remediation themes

- **Restrict zone transfers.** Allow AXFR only to specifically authorised
  secondary name servers, not to the world.
- **Mind what DNS advertises.** Don't rely on "security through obscurity," but
  do avoid needlessly publishing internal host names in public DNS; separate
  internal and external DNS where appropriate.
- **Set strong email-security records.** Proper SPF, DKIM, and DMARC policies in
  TXT records reduce email spoofing.
- **Review periodically.** DNS accumulates stale records; old entries can point
  at forgotten or decommissioned systems.

!!! note "Check your understanding"
    - What legitimate purpose does a zone transfer serve, and why is an
      unrestricted one a problem?
    - Which record type would tell you where an organisation receives email?
    - Why might the subdomains discovered via DNS be more interesting than the
      main domain itself?
