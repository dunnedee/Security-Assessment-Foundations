# The engagement lifecycle

## The concept

A penetration test isn't a single event — it's a structured engagement that
moves through distinct phases. Understanding the lifecycle helps you see where
the actual "hacking" fits (it's a surprisingly small slice) and why the work
around it determines whether the engagement is useful and professional.

## Why it matters

Penetration testing exists so that an organisation can find and fix weaknesses
**before** a genuine attacker exploits them. It gives a real-world, evidenced
view of security posture, and it supports compliance obligations under
frameworks and regulations such as ISO 27001, PCI DSS, and the UK GDPR.

That value only materialises if the engagement is run properly end to end. A
brilliant finding delivered late, unclearly, or without a fix is of little use.

## The phases

### 1. Pre-engagement

Everything that happens before testing begins:

- Understanding the client's objectives — what are they actually worried about?
- Defining and agreeing the [scope](scoping.md).
- Agreeing the [rules of engagement](scoping.md#rules-of-engagement-roe).
- Securing **written authorisation** — the legal basis for the whole test.
- Planning timelines, resources, and points of contact.

> *Example:* A financial services company asks for a test of its external
> infrastructure but explicitly excludes its payment-processing platform from
> scope. That exclusion is agreed and documented before anything starts.

### 2. Testing

The active phase, which itself has a natural internal flow:

- **Information gathering / reconnaissance** — building a picture of the target.
- **Enumeration** — identifying live systems, services, and potential entry
  points.
- **Analysis and validation** — determining which weaknesses are real and what
  they'd mean.
- **Controlled demonstration of impact** — where in scope, showing the
  real-world consequence of a weakness, within agreed limits.

Throughout, the tester keeps careful [records](reporting.md) of what was done
and what was found.

### 3. Post-engagement

Turning the work into lasting value:

- **Reporting** — documenting findings, risk ratings, and clear remediation
  advice.
- **Debrief** — walking the client through the results, for both technical and
  non-technical audiences.
- **Remediation support** — helping the client understand and implement fixes,
  and often re-testing afterwards to confirm the fix worked.

> *Example:* After identifying a weakness in a web application's handling of
> user input, the tester explains the underlying cause and the remediation — in
> this case, adopting parameterised queries — and later re-tests to confirm it's
> resolved.

## Types of assessment

How much the tester is told up front shapes the engagement:

| Type | Knowledge given | Simulates | Typical use |
|---|---|---|---|
| **Black box** | None | An external attacker with no inside knowledge | Realistic external perspective |
| **White box** | Full (architecture, source, credentials) | An insider or a thorough review | Deep, efficient internal review |
| **Grey box** | Partial (e.g. a standard user login) | A user or a partially-informed attacker | Common for application testing |

There's no "best" option — each trades realism against thoroughness and
efficiency. Grey box, for instance, often gives the best coverage per day of
effort because the tester doesn't spend time rediscovering what the client could
simply have told them.

## Project closure

A test should end with a structured handover: findings presented, risks
explained in business terms, and actionable recommendations delivered. The
client should come away knowing *what's wrong, how bad it is, and what to do
about it*.

!!! note "Check your understanding"
    - Why might an organisation choose a grey box test over a black box one,
      even though black box is "more realistic"?
    - Which phase of the lifecycle do you think most newcomers underestimate,
      and why?
    - What's the single most important thing that must exist before the testing
      phase can begin?
