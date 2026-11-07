# Network mapping & discovery

## The concept

Network mapping (or discovery) is the process of identifying which hosts are
live on a network and which services they expose. It's the step that turns "an
IP range" into "a concrete inventory of systems to understand." Enumeration is
the natural companion: once you know what's there, you draw out detail.

## Why it matters

You can't assess — or defend — what you don't know exists. For an assessor,
discovery defines the real attack surface. For a defender, it's exactly the
asset-management exercise that so often reveals forgotten servers, shadow IT, and
services that were supposed to have been decommissioned.

## Host discovery

Before looking at services, you establish which hosts are actually alive. There
are several approaches, and which works depends on the environment:

- **ICMP ("ping")** is the simplest, but it's frequently blocked by firewalls,
  so its absence doesn't mean a host is down.
- **ARP-based discovery** is reliable on a local network segment, because ARP is
  fundamental to how that segment functions.
- **TCP/UDP probing** infers that a host is alive from how it responds (or
  doesn't) to traffic on particular ports — useful when ICMP is filtered.

A key practical lesson: **"no ping reply" is not "no host."** Firewalls routinely
drop ICMP, so testers use alternative techniques rather than assuming a silent
host is absent. A common approach when ping is blocked is to skip host-discovery
pinging altogether and probe ports directly.

## Port and service scanning

Once live hosts are known, scanning identifies **open ports** and the
**services** behind them. The general tool of the trade here is a network scanner
such as **Nmap**, which can:

- Identify open, closed, and filtered ports.
- Detect the **service and version** behind a port.
- Attempt **operating-system fingerprinting**.
- Run scripted checks for specific conditions.

Different scan styles trade **thoroughness, speed, and stealth** against each
other. A fast, aggressive, all-ports scan with version and OS detection is
thorough but noisy and demanding on the target; lighter, slower, or more
targeted scans are quieter and gentler. Choosing appropriately is part of
[risk management](../assessment-management/risk-management.md) — an aggressive
scan against fragile equipment can cause disruption.

!!! note "On evasion techniques"
    Scanners support techniques intended to make scanning harder for monitoring
    to detect or attribute. Conceptually, these exist because defensive systems
    (firewalls and intrusion-detection systems) watch for scanning, and testers
    sometimes need to understand how detectable their activity is. The
    *defensive* takeaway is what matters here: good monitoring should detect
    reconnaissance, and controls shouldn't rely on an attacker scanning in the
    most obvious way.

## Passive mapping

Not all discovery is active. On a network segment you're authorised to be on,
observing existing traffic can reveal which hosts are communicating without
sending probes to them directly. This is quieter and lower-impact, though it
reveals only what happens to be talking.

## Remediation / defensive themes

- **Know your estate.** Maintain accurate asset inventories; discovery shouldn't
  be able to find things you didn't know you had.
- **Reduce exposure.** Close or filter unnecessary ports and services; segment
  networks so a foothold doesn't see everything.
- **Monitor for reconnaissance.** Scanning should generate signal your defenders
  actually see and act on.
- **Don't depend on ICMP filtering as security.** Blocking ping slows casual
  discovery but doesn't hide a host from a capable assessor.

!!! note "Check your understanding"
    - Why is "the host didn't answer a ping" an unreliable conclusion that a host
      is offline?
    - What three properties are traded off when choosing how to scan, and when
      would you favour stealth over thoroughness?
    - Why is network discovery really an asset-management problem from the
      defender's side?
