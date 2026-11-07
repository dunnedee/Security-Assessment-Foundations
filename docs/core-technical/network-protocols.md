# Network protocols

## The concept

Networks are built on agreed rules — protocols — that let systems communicate.
Understanding these protocols deeply matters because many weaknesses come not
from "bugs" but from protocols trusting something they shouldn't, or from
services being exposed where they shouldn't be.

## IPv4 and IPv6

The Internet Protocol handles addressing and routing.

| | IPv4 | IPv6 |
|---|---|---|
| **Address size** | 32-bit (e.g. `192.168.1.1`) | 128-bit (e.g. `2001:db8::ff00:42:8329`) |
| **Address space** | ~4.3 billion — effectively exhausted | Vast |
| **Notable features** | Ubiquitous, well understood | Larger space, modern design, IPsec support defined in the standard |

From a security standpoint, IPv6 is worth special attention for one practical
reason: it's often **present but unmanaged**. Hosts may have IPv6 enabled and
reachable while the organisation's monitoring and controls were built only for
IPv4 — creating blind spots. The lesson is that an address family you're not
watching is an address family someone else might use.

## TCP and UDP

Both sit at the transport layer, but they behave very differently:

- **TCP (Transmission Control Protocol)** is *connection-oriented*. It
  establishes a session (the "three-way handshake"), guarantees ordered
  delivery, and retransmits lost data. Used where reliability matters — web,
  email, file transfer.
- **UDP (User Datagram Protocol)** is *connectionless*. It just sends
  datagrams, with no handshake and no delivery guarantee. Faster and lighter,
  used where speed beats reliability — DNS, many streaming and voice protocols,
  SNMP.

Why this matters for assessment:

- TCP's handshake is what lets a tester determine whether a port is open,
  closed, or filtered.
- UDP's connectionless, source-trusting nature is what makes certain services
  prone to **spoofing and amplification** abuse — because a server may reply to
  a request without verifying who really sent it.

## The OSI model (a quick orientation)

The OSI model is a seven-layer mental model for how communication is structured.
You don't need to memorise it mechanically, but you should be able to reason
about *which layer* a given issue lives at:

| Layer | Example concern |
|---|---|
| 7 Application | Web app logic, HTTP |
| 6 Presentation | Encoding, encryption formatting |
| 5 Session | Session setup/teardown |
| 4 Transport | TCP/UDP, ports, flow control |
| 3 Network | IP addressing, routing |
| 2 Data Link | MAC addressing, local segment |
| 1 Physical | Cabling, radio |

Thinking in layers helps you place a problem: a weakness in how a local network
segment trusts address information is a very different thing from a flaw in web
application logic, even if both end in "an attacker got in."

## Common ports and services

Recognising common services by their default port is basic fluency. A
non-exhaustive starter set:

| Port | Service |
|---|---|
| 22 | SSH |
| 25 | SMTP (email) |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 139 / 445 | SMB / NetBIOS |
| 3389 | RDP |
| 161 | SNMP |

Defaults are only conventions — services can run anywhere — but knowing them
speeds up understanding what a system is offering.

## How protocol weakness shows up in an assessment

At a conceptual level, an assessor is interested in:

- **What's exposed** — which services are reachable, and should they be?
- **What's trusted** — does a protocol accept information (like a source
  address) without verifying it?
- **What's unencrypted** — is sensitive data moving in the clear where it could
  be observed?

## Remediation themes

- **Reduce exposure.** Only expose services that need to be reachable, and only
  to those who need them. Segment networks.
- **Don't rely on spoofable trust.** Where a protocol trusts source information,
  add controls that don't (authentication, filtering).
- **Encrypt sensitive traffic.** Protect confidentiality and integrity in
  transit.
- **Manage what you have — all of it.** Including IPv6 and services you forgot
  were enabled.

!!! note "Check your understanding"
    - Why does UDP's design make certain services more prone to spoofing and
      amplification abuse than TCP-based ones?
    - Give an example of a weakness that lives at the network layer versus one
      at the application layer.
    - Why is "IPv6 is enabled but unmonitored" a security problem even if no one
      is deliberately using it?
