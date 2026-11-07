# Device configuration review

## The concept

**Configuration review** (or configuration analysis) is examining the settings of
systems and network devices to find security weaknesses — misconfigurations,
weak or default credentials, unnecessary services, and deviations from good
practice. It's a quiet, high-value discipline: a great many serious findings come
not from exotic flaws but from how something was set up.

## Why it matters

Misconfiguration is one of the most common root causes of real-world compromise.
Reviewing a device's configuration directly — rather than only probing it from
outside — often reveals weaknesses that no external scan would surface, and does
so without any disruption. For infrastructure like routers, switches, and
firewalls, the configuration file *is* the security posture.

## Infrastructure devices and their configurations

Network devices (commonly Cisco in enterprise environments, but the principles
generalise) are driven by configuration files that define access control,
routing, and security settings. Reviewing them focuses on areas like:

- **Access control** — who can reach and manage the device, and how.
- **Authentication** — the strength and storage of credentials.
- **Enabled services and interfaces** — what's switched on that needn't be.
- **Logging and monitoring** — whether the device records what it should.
- **Routing and filtering rules** — ACLs and firewall policy.

## Credentials in configuration: a worked theme

Infrastructure devices illustrate password-storage principles vividly. On Cisco
devices, for example, there's an important difference between:

- A **plaintext** privileged-mode password stored readably in the configuration —
  weak, because anyone who can read the config reads the password.
- An **encrypted/hashed** equivalent (the "enable secret"), which stores a hashed
  form instead — much better, though the strength depends on the algorithm used.
- A setting that **encrypts the remaining plaintext passwords** in the config file
  (`service password-encryption`) — worth enabling, though note that some of these
  older encryption schemes are weak and easily reversed, so they're a thin layer,
  not real protection.

The lesson mirrors [password storage](../core-technical/hashing.md) generally:
**how a secret is stored matters enormously**, and a configuration review is where
you catch secrets stored badly. Treat a configuration file as sensitive — it often
contains, or protects, the keys to the device.

## Key review areas

- **Strong authentication, no defaults.** Default credentials on infrastructure
  are a perennial serious finding.
- **Secure management access.** Prefer encrypted management (e.g. SSH over Telnet);
  restrict where management access can come from.
- **Least functionality.** Disable unused ports, services, and interfaces to
  shrink the attack surface.
- **Centralised access control** (AAA) and **logging** so access is controlled and
  recorded.
- **Encryption of stored secrets**, understanding the limits of weak schemes.

## Managing configuration securely

Configuration review isn't a one-off; it's part of configuration *management*:

- **Back up** configurations so they can be restored.
- **Version-control** them to track changes and spot unauthorised ones.
- **Audit regularly** against a known-good baseline.
- **Restrict who can change them** (role-based access control).
- **Automate** enforcement for consistency across many devices.

## Tools

Specialised tools can audit device configurations against security baselines and
flag weaknesses automatically — useful for scale, but the understanding of *what*
a good configuration looks like is what makes their output meaningful.

!!! note "Check your understanding"
    - Why can a configuration review surface weaknesses that an external scan
      cannot?
    - What's the difference between storing a device password in plaintext versus
      a hashed form, and why does a weak encryption scheme give only thin
      protection?
    - Why should a device's configuration file itself be treated as sensitive?
