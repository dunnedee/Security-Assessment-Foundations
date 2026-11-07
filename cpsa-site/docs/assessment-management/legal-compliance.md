# Legal & compliance (UK)

## The concept

Security testing involves doing things to computer systems that, without
permission, would be criminal. The *only* thing separating authorised testing
from illegal hacking is **explicit permission** and staying within its bounds.
Knowing the legal landscape isn't optional background — it's the foundation the
whole profession stands on.

!!! danger "The line is permission"
    Running even a simple scan against a system you don't own or have written
    authorisation to test can be a criminal offence. "I was only looking" is not
    a defence. Get authorisation in writing, and stay inside its scope.

## Why it matters

A tester who strays outside authorisation exposes themselves to prosecution,
exposes their employer to liability, and destroys client trust. Compliance
knowledge also shapes *what* clients need from you — many engagements exist
specifically to satisfy a regulatory or contractual requirement.

## Key UK laws

### Computer Misuse Act 1990 (CMA)

The central piece of UK legislation. In broad terms it creates offences around:

- **Unauthorised access** to computer material.
- **Unauthorised access with intent** to commit or facilitate further offences.
- **Unauthorised acts** intended to impair the operation of a computer (e.g.
  causing a denial of service).
- Making, supplying, or obtaining tools for use in the above.

The recurring word is **unauthorised**. Written authorisation that clearly
covers your activity is what makes the same technical action lawful.

### Data Protection Act 2018 / UK GDPR

Governs how personal data is handled. Relevant to testing because:

- An engagement may expose you to personal data (in a database, a file share, a
  document). You must handle it lawfully and protect its confidentiality.
- The way you store evidence, screenshots, and findings must itself respect data
  protection principles.
- Clients often test *because* they have obligations to protect personal data.

### The wider picture

Other legislation can come into play depending on the engagement — for example,
laws around interception of communications, or sector-specific rules. The
practical takeaway: know enough to recognise when something needs legal input,
and don't guess.

## Standards and regulations you'll meet

These aren't laws, but they drive a huge amount of testing work:

| Framework | What it is | Where it applies |
|---|---|---|
| **PCI DSS** | Payment Card Industry Data Security Standard | Any organisation handling payment card data |
| **ISO/IEC 27001** | International standard for information security management | Organisations formalising their security programme |
| **NIS Regulations** | Security of network & information systems | Operators of essential services (energy, transport, health, etc.) and certain digital service providers |
| **Cyber Essentials** | UK government-backed baseline scheme | Organisations demonstrating basic cyber hygiene, often for public-sector contracts |

## The professional takeaway

- **Authorisation first, always.** Written, specific, and agreed by someone with
  the authority to grant it.
- **Stay in scope.** Authorisation covers what it says it covers — no more.
- **Handle data responsibly.** Treat anything you encounter as if it were your
  own most sensitive information.
- **Know your limits.** When something has legal or regulatory weight you're
  unsure about, escalate it rather than improvise.

!!! note "Check your understanding"
    - What single word in the Computer Misuse Act most determines whether an
      action is lawful?
    - Why might two engagements that are technically identical be lawful in one
      case and criminal in the other?
    - A client asks you to "just quickly check" a system that isn't in the
      signed scope. What's the right response, and why?
