# Building a home lab

Everything in this resource is meant to be *tried*, not just read — but only in
a place where you can't do any harm. A home lab is that place: an isolated,
self-contained environment made of machines you own, where you can break things
freely.

!!! danger "This is the whole point"
    Practising against systems you don't own or have explicit written
    permission to test is a criminal offence in most jurisdictions, including
    under the UK's [Computer Misuse Act
    1990](../assessment-management/legal-compliance.md). A home lab removes any
    ambiguity: the targets are yours.

## The basic ingredients

You can build a capable lab on a single modern laptop:

- **A hypervisor** to run virtual machines — e.g. VirtualBox (free) or VMware
  Workstation Player. This lets you run multiple isolated systems on one
  physical computer.
- **An attacker VM** — a security-focused Linux distribution such as Kali Linux
  or Parrot OS, which bundle the common assessment tooling.
- **Deliberately vulnerable target VMs** — systems built *to be* broken into,
  for learning. Common choices include Metasploitable, the OWASP Broken Web
  Applications project, and the intentionally vulnerable apps described below.
- **An isolated virtual network** — so your lab traffic never touches your home
  network or the internet unless you choose.

## Keep it isolated

Configure your lab network as **host-only** or **internal** in your hypervisor.
That means:

- The vulnerable targets can't be reached from your home network or the wider
  internet.
- Nothing you do to them can leak out.
- You control exactly what talks to what.

This matters because deliberately vulnerable machines are, by definition,
insecure — you do not want them exposed.

## Safe, legal practice targets

Rather than hunting for things to attack, use environments built and licensed
for learning:

| Target | What you learn |
|---|---|
| **OWASP Juice Shop** | Modern web application vulnerabilities, hands-on |
| **Damn Vulnerable Web Application (DVWA)** | Classic web weakness classes at adjustable difficulty |
| **Metasploitable** | Network service and host weaknesses |
| **VulnHub** images | Full "boot-to-root" scenarios you download and run locally |
| **TryHackMe / HTB** | Hosted labs — no local setup, isolation handled for you |

## A sensible first setup

1. Install a hypervisor.
2. Create your attacker VM (Kali or Parrot).
3. Add one vulnerable target (OWASP Juice Shop or DVWA is a gentle start).
4. Put both on a host-only network.
5. Confirm the attacker VM can reach the target and that neither can reach the
   internet.
6. Snapshot both VMs while they're clean, so you can roll back after you've made
   a mess.

From there, add targets as your interests grow. The lab is never "finished" —
it grows with you.
