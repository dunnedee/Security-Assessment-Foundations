# Routing & network architecture

## The concept

**Routing** is how data finds its way across networks — the process of selecting
paths so a packet gets from source to destination, possibly across many
intermediate networks. Understanding routing, the layered model beneath it, and
how networks are structured gives you the map on which all other security
thinking sits.

## The OSI model

The **OSI (Open Systems Interconnection) model** is a seven-layer framework for
reasoning about network communication. Each layer has a job, and being able to
place a protocol or a problem at the right layer is genuinely useful.

| Layer | Function | Examples |
|---|---|---|
| 7 Application | User-facing services, data formatting | HTTP, FTP, DNS |
| 6 Presentation | Encryption, compression, encoding | TLS, MIME |
| 5 Session | Establishing/maintaining/ending connections | RPC, NetBIOS |
| 4 Transport | End-to-end delivery, flow control | TCP, UDP |
| 3 Network | Addressing and routing | IP, ICMP, ARP* |
| 2 Data Link | Local addressing, error detection | Ethernet, PPP |
| 1 Physical | Raw transmission | Cabling, Wi-Fi radio |

*ARP is sometimes placed between layers 2 and 3; models are a guide, not gospel.

The practical value: a weakness at the data-link layer (local segment trust) is a
fundamentally different problem from one at the application layer, even if both
end in compromise. Thinking in layers keeps that clear.

## Routing protocols

Routing protocols decide how traffic is forwarded. You don't need to configure
them to understand them conceptually:

| Protocol | Type | In brief |
|---|---|---|
| **RIP** | Distance vector | Simple, uses hop count; limited scale |
| **OSPF** | Link-state | Efficient path selection; common internally |
| **EIGRP** | Hybrid (Cisco) | Balances speed and efficiency |
| **BGP** | Path vector | The routing protocol *between* networks on the internet |
| **IS-IS** | Link-state | Large-scale, common with ISPs |

**BGP** deserves special mention: it's what routes traffic between the large
networks (autonomous systems) that make up the internet, and it historically
trusts routing announcements more than is comfortable — which is why BGP security
is an ongoing concern.

## Static vs dynamic routing

- **Static routing** — routes configured manually. Predictable and simple, good
  for small or fixed networks.
- **Dynamic routing** — routing protocols adjust paths automatically as
  conditions change. Scales far better, at the cost of complexity and of trusting
  the protocol's exchanges.

## Network architectures (a quick map)

- **Client–server vs peer-to-peer** — centralised services versus direct
  device-to-device communication.
- **LAN / WAN** — local versus geographically distributed networks.
- **Segmentation** — dividing a network into zones so that compromise in one
  doesn't mean access to all. This is one of the most important *defensive*
  architectural ideas in this entire resource.

## How routing is attacked (and defended)

Routing and local addressing rely on trust, which is where the weaknesses are:

| Attack (concept) | What it does | Defence |
|---|---|---|
| **Route manipulation** (e.g. route poisoning) | Injects false routing information to misdirect traffic | Authenticated routing protocols; validation |
| **BGP hijacking** | Announces routes to reroute others' traffic | Route origin validation (e.g. RPKI), filtering |
| **ARP spoofing** | Falsifies local address mappings to intercept traffic on a segment | Dynamic ARP inspection, segmentation, encryption |
| **Man-in-the-middle** | Intercepts/alters traffic in transit | Encryption and certificate validation end-to-end |

The recurring theme: **routing trusts information that can be forged**, so the
defences are authentication, validation, segmentation, and end-to-end encryption
so that intercepted traffic is useless.

## Remediation / defensive themes

- **Segment networks** so a foothold can't reach everything — the single most
  valuable architectural control.
- **Authenticate routing** where the protocol supports it; validate routes.
- **Encrypt end-to-end** so interception doesn't equal disclosure.
- **Use ACLs and firewalls** to constrain traffic to what's needed.
- **Patch and monitor** network devices like the critical systems they are.

!!! note "Check your understanding"
    - Why is being able to place a problem at the right OSI layer useful?
    - What makes BGP's trust model a security concern, and what helps?
    - Why is network segmentation such a powerful defensive idea — which later
      attack phase does it most directly limit?
