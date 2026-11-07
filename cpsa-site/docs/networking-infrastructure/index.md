# Networking & infrastructure

Once you know an organisation exists and roughly how it's shaped, the next step
is mapping the network and understanding the services running on it. This
section covers how networks are discovered and enumerated, and the particular
case of wireless.

- **[Network mapping & discovery](network-mapping.md)** — finding live hosts and
  open services, and the trade-off between thoroughness and stealth.
- **[Service enumeration](service-enumeration.md)** — drawing information out of
  the services you find.
- **[Fingerprinting & service identification](fingerprinting.md)** — identifying
  operating systems, services, and applications from how they respond.
- **[Routing & network architecture](network-routing.md)** — how traffic moves,
  the OSI model, and where routing is attacked.
- **[Wi-Fi & wireless security](wifi-security.md)** — the protocols, their
  weaknesses, and how wireless is secured.
- **[VoIP & SIP security](voip-security.md)** — securing voice-over-IP and its
  signalling.

!!! info "Discovery is where the map gets drawn"
    This is the phase where an abstract target becomes a concrete list of
    systems and services. The defensive mirror is **asset management**: most
    organisations are surprised by what a thorough discovery turns up, because
    they'd lost track of it.
