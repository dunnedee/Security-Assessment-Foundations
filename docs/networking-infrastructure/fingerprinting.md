# Fingerprinting & service identification

## The concept

**Fingerprinting** is identifying *what* something is — the operating system,
the service, the application and version — by examining how it responds. Systems
reveal themselves through subtle differences in how they implement protocols and
how they answer requests. Accurate identification is what turns "a port is open"
into "this is an old version of a specific service," which is the knowledge that
drives everything downstream.

## Why it matters

You can't assess, prioritise, or remediate what you can't identify. Fingerprinting
tells an assessor what they're dealing with; it tells a defender exactly how much
their systems are advertising to anyone who looks. Much of what fingerprinting
relies on is **unnecessary disclosure** that can be reduced.

## OS fingerprinting

Determining the operating system of a target. Two broad approaches:

- **Active fingerprinting** sends crafted requests and analyses the responses.
  Different operating systems answer certain unusual requests in characteristic
  ways, which reveals them. It's effective but involves direct interaction.
- **Passive fingerprinting** observes existing traffic without sending anything,
  inferring the OS from the characteristics of packets it already sees. Quieter,
  but limited to what's observable.

One classic signal is the **default TTL (Time To Live)** value in packets, which
commonly differs by OS family:

| Operating system | Typical default TTL |
|---|---|
| Windows | 128 |
| Linux / modern macOS | 64 |
| Some Unix (e.g. Solaris) | 255 |

TTL alone is only a hint (it decrements across hops and can be changed), but
combined with other signals it contributes to an identification.

## Service and application fingerprinting

Beyond the OS, assessors identify the specific services and applications running:

- **Banner grabbing** — many services announce themselves (and sometimes their
  version) in their responses. Reading that banner identifies the service.
- **Response analysis** — how a service replies to particular requests
  distinguishes products and versions even when no banner is offered.
- **Web technology identification** — web apps reveal frameworks, languages, and
  components through headers, cookies, and page characteristics.
- **TLS/SSL inspection** — the certificates and supported cryptographic options
  of an encrypted service reveal information about it.

Why it matters: a specific service *and version* can be checked against public
vulnerability databases (CVE, and similar). Knowing you have "an outdated version
of X" is the step that identifies a real, known weakness.

## Traceroute and path analysis

**Traceroute** (also `tracert` on Windows) maps the route packets take to a
destination. It works by sending packets with increasing TTL values; each router
along the way decrements the TTL and, when it hits zero, reports back — revealing
each hop in turn.

It's used to understand network latency, detect filtering, troubleshoot
connectivity, and map external infrastructure. For a defender, it's a reminder
that the *path* to your services is itself observable.

## A note on filtering evasion

Firewalls and intrusion-detection systems try to detect and block fingerprinting
and scanning. Various techniques exist to make that activity harder to detect or
attribute — packet fragmentation, decoy traffic, relaying through intermediaries,
irregular timing. As with [scanning](../vulnerability-assessment/scanning.md), the
point to take from this is **defensive**:

- Monitoring should be robust enough to detect reconnaissance even when it isn't
  done in the most obvious way.
- Controls should never depend on an attacker announcing themselves clearly.
- Reducing what your systems disclose in the first place is the most durable
  defence.

## Remediation / defensive themes

- **Minimise information disclosure.** Suppress or genericise service banners and
  version strings where you can; don't volunteer the exact software and version.
- **Keep software current.** Fingerprinting only matters because old versions map
  to known vulnerabilities — patching breaks that chain.
- **Harden and monitor.** Detect reconnaissance; don't rely on it being obvious.
- **Reduce the surface.** Fewer exposed services means fewer things to fingerprint.

!!! note "Check your understanding"
    - What's the difference between active and passive OS fingerprinting?
    - Why is identifying a service's *version* so much more useful than just
      knowing the service exists?
    - How does traceroute use TTL to map a network path?
    - Why is "reduce what systems disclose" a more durable defence than trying to
      block every fingerprinting technique?
