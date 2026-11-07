# Scoping & rules of engagement

## The concept

**Scoping** defines what will be tested, how, and within what boundaries.
The **Rules of Engagement (RoE)** document captures those decisions formally.
Together they are the contract that makes a test safe, lawful, and useful — and
they're agreed *before* any testing starts.

## Why it matters

A test without a clear scope is dangerous in both directions: the tester might
touch systems they weren't authorised to (a legal problem), or waste the
engagement on the wrong targets (a value problem). Good scoping aligns the test
with what the client actually needs and protects everyone involved.

## Defining the scope

Scoping is fundamentally about drawing a clear line between what is **in scope**
and what is **out of scope**.

- **In scope:** the specific systems, applications, networks, IP ranges, URLs,
  or accounts that the tester is authorised to assess.
- **Out of scope:** everything else — often including production systems that
  can't tolerate disruption, third-party services the client doesn't own, or
  sensitive platforms excluded for business reasons.

> *Example:* A retailer authorises testing of its public e-commerce website but
> excludes its HR system entirely. The HR system is explicitly out of scope and
> must not be touched, even if a path to it is discovered.

Good scoping conversations also surface:

- The client's **objectives** — what outcome makes this test worthwhile?
- **Risk factors** — what's fragile, what's business-critical, what's sensitive.
- **Timelines and resources** — how long, how many testers, when.
- **Third-party authorisation** — if systems are hosted by a cloud or managed
  provider, that provider may also need to authorise the testing.

## Rules of Engagement (RoE)

The RoE document turns the agreed scope into explicit operating rules. It
typically specifies:

- **What's permitted** — e.g. whether social engineering or denial-of-service
  style testing is allowed (often it is explicitly *not*).
- **Timing** — the testing window, and whether certain activity must happen
  out of hours.
- **Escalation and contacts** — who to call if something breaks, and how
  quickly serious findings must be reported.
- **Handling of sensitive data** — what to do if the tester encounters personal
  or regulated data.
- **Constraints** — e.g. "no destructive actions," "report critical findings
  immediately rather than continuing."

> *Example:* A client doesn't want its production servers affected. The RoE
> states that no destructive testing will take place and that any critical
> finding must be reported before any demonstration of impact is attempted.

## The professional takeaway

Scoping and the RoE are where a lot of risk is quietly eliminated before it ever
materialises. Treat them as a core skill, not paperwork to rush through:

- Be precise. Ambiguity in scope is where accidents happen.
- Write it down and get it agreed by someone with authority.
- Revisit it if circumstances change mid-engagement — don't just improvise.

!!! note "Check your understanding"
    - Why is it sometimes necessary to get authorisation from a party *other*
      than your direct client?
    - Give two reasons a client might place a system out of scope.
    - What should the RoE say about what happens when a tester finds something
      critical on day one?
