# VoIP & SIP security

## The concept

**Voice over IP (VoIP)** carries phone calls over data networks instead of
traditional telephone lines. Because the voice is now just network traffic, it
inherits all the security concerns of network traffic — plus some of its own.
Understanding VoIP means understanding its signalling (how calls are set up) and
its media (the voice itself), because they're secured differently.

## Why it matters

VoIP is everywhere in modern organisations, and it's frequently overlooked in
security programmes — treated as "the phone system" rather than as the networked
application it actually is. That gap is exactly why it's worth assessing: calls
can be intercepted, services disrupted, and VoIP accounts abused for fraud.

## How VoIP works: signalling and media

VoIP splits into two jobs, each with its own protocols:

- **Signalling** sets up, modifies, and tears down calls. The dominant protocol is
  **SIP (Session Initiation Protocol)**. Older environments may use **H.323**;
  Cisco environments historically used **SCCP ("Skinny")**.
- **Media** carries the actual voice (and video). This is **RTP (Real-time
  Transport Protocol)**, with **SRTP** as its encrypted form.

| Protocol | Role | Typical port(s) |
|---|---|---|
| SIP | Call signalling | 5060 (UDP/TCP), 5061 (TLS) |
| RTP | Voice/video media | Dynamic UDP range |
| SRTP | Encrypted media | As RTP, encrypted |
| H.323 | Legacy signalling | 1720 (TCP) |

The key insight: **SIP over TLS** protects the call setup, and **SRTP** protects
the voice itself. You need both — encrypting one without the other leaves a gap.

## SIP in a little more detail

SIP is worth knowing because it's the most common signalling protocol. It
involves components such as **user agents** (the endpoints), **proxy servers**
(routing SIP messages), and **registrar servers** (which authenticate users and
track where they are). It uses readable message types — `INVITE` to start a call,
`BYE` to end one, `REGISTER` to sign an endpoint in, and so on.

Because SIP is often text-based and, if unencrypted, readable on the network, it's
exposed to interception and manipulation unless protected.

## VoIP security threats

The recurring risks, at a conceptual level:

| Threat | What it means |
|---|---|
| **Eavesdropping** | Intercepting unencrypted signalling or media to listen to calls |
| **Call hijacking / redirection** | Diverting calls to an attacker-controlled endpoint |
| **Denial of service / SIP flooding** | Overwhelming VoIP services so calls fail |
| **Caller ID spoofing** | Falsifying the caller identity, enabling fraud and "vishing" |
| **Toll fraud** | Abusing a compromised VoIP account to place costly calls |

Several of these trace back to the same roots seen elsewhere: **unencrypted
traffic** (eavesdropping), **weak authentication** (fraud, hijacking), and
**exposed services** (DoS). VoIP is a good illustration that the same principles
apply to every networked application.

## Remediation / defensive themes

- **Encrypt both layers.** SIP over **TLS** for signalling and **SRTP** for media.
- **Authenticate strongly.** Robust authentication for endpoints; don't rely on
  defaults or weak credentials.
- **Restrict and segment.** Limit who can reach VoIP servers (ACLs), and keep
  voice infrastructure segmented from the rest of the network.
- **Patch and monitor.** Treat VoIP servers and endpoints as the critical,
  patchable systems they are; watch for anomalies and SIP abuse.
- **Reduce the surface.** Disable unused VoIP features and services.
- **Train people.** Voice phishing (vishing) and caller-ID spoofing target users,
  so awareness is part of the defence.

!!! note "Check your understanding"
    - Why do you need to secure *both* SIP and RTP, rather than just one?
    - Which familiar root causes underlie VoIP eavesdropping and toll fraud?
    - Why is VoIP so often overlooked in security programmes, and why is that a
      mistake?
