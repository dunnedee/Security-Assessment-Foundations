# Wi-Fi & wireless security

## The concept

Wireless networks bring obvious convenience and one inescapable property: the
signal travels through the air, where anyone in range can receive it. That
changes the security model fundamentally. Where a wired network has some
physical access control, a wireless one is exposed to anyone nearby — so the
encryption and authentication protecting it have to do much more work.

## Why it matters

Wi-Fi is often an organisation's softest edge: a weakly secured wireless network
can offer a path onto the internal network without the attacker ever setting
foot inside. Understanding wireless security protocols and their weaknesses is
core infrastructure knowledge.

## Encryption protocols, oldest to newest

| Protocol | Standing | Notes |
|---|---|---|
| **WEP** | Obsolete / broken | Fundamentally flawed; trivially defeated. Should never be in use today. |
| **WPA** | Weak | An interim improvement over WEP, now also considered weak. |
| **WPA2** | Still common | Strong when configured well (AES-based); the long-time standard. Has known weaknesses such as the KRACK key-reinstallation issue, addressed by patching. |
| **WPA3** | Current best | Modern protections and stronger key establishment; the target to move toward. |

The practical lesson mirrors [cryptography](../core-technical/cryptography.md)
generally: **older protocols are broken, and a network is only as strong as the
weakest option it permits.** WEP in particular is a serious finding simply by
being present.

## Authentication models

How clients prove they're allowed to join:

- **Open** — no authentication or encryption. Fine for genuinely public access
  *only alongside other protections*, but traffic is exposed to anyone
  listening.
- **Pre-Shared Key (PSK)** — the "personal" model, a shared password for the
  network. Simple, but only as strong as the password; weak passphrases
  undermine it.
- **Enterprise (802.1X / RADIUS)** — each user authenticates individually
  against an authentication server. Stronger and more manageable (no shared
  secret, per-user control), and the right choice for organisations.

## Classes of wireless weakness

At a conceptual level, wireless attacks fall into recognisable families:

- **Eavesdropping** — because the signal is broadcast, unencrypted or
  weakly-encrypted traffic can be observed.
- **Rogue / "evil twin" access points** — a malicious access point impersonating
  a legitimate network, tricking clients into connecting to it.
- **Deauthentication / availability attacks** — disrupting wireless service, or
  forcing clients to reconnect (which can set up other attacks).
- **Authentication weaknesses** — attacks against the key-exchange or against
  weak pre-shared keys, and against convenience features like WPS that have known
  design flaws.

The tools used to assess these (packet captures, wireless analysers, and
purpose-built suites) are well known; the assessment point is to identify which
of these weaknesses a given deployment is exposed to, and the defensive point is
to close them.

## Defensive measures

- **Use WPA3, or well-configured WPA2 (AES)** at minimum. Eliminate WEP and WPA
  entirely.
- **Prefer Enterprise (802.1X) authentication** for organisational networks;
  where PSK is unavoidable, use a long, strong passphrase.
- **Disable WPS**, which has well-known weaknesses.
- **Separate networks.** Keep guest Wi-Fi isolated from internal systems; treat
  wireless as untrusted and segment accordingly.
- **Monitor for rogue access points** with wireless intrusion detection.
- **Keep firmware patched** — several wireless weaknesses are fixed by updates.
- **Use a VPN on untrusted/public Wi-Fi** to protect traffic end-to-end.

!!! note "Check your understanding"
    - Why does wireless change the security model compared with a wired network?
    - Why is the presence of WEP a serious finding on its own?
    - What advantages does Enterprise (802.1X) authentication have over a shared
      pre-shared key?
    - What is an "evil twin" access point, and what makes it effective?
