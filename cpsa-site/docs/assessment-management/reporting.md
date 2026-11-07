# Reporting & documentation

## The concept

The report is the **product**. Everything the tester finds only becomes
valuable when it's recorded accurately and communicated clearly enough for the
client to act on. Documentation runs throughout the engagement; the report is
its polished output.

## Why it matters

A client doesn't buy "a test" — they buy the understanding and the fixes a test
produces. Two testers can find identical issues; the one who explains them
clearly, rates them sensibly, and gives actionable remediation delivers far more
value. Reporting is also an accountability record of what was done and when.

## Record-keeping during the engagement

Keep thorough, contemporaneous notes as you work:

- What you did, when, and against what.
- What you found, with enough evidence to reproduce and verify it.
- Anything unexpected — instability, out-of-scope discoveries, access to
  sensitive data.

This protects you (it evidences that you stayed in scope and acted
professionally) and makes the final report far easier to write accurately.

## Types of report

- **Interim / real-time updates.** For anything serious enough that the client
  shouldn't wait — a critical weakness is flagged during the test, not held back
  for the final document.
- **The final report.** The comprehensive record of the engagement: scope,
  approach, findings, risk ratings, and recommendations.

## Anatomy of a good finding

Each finding should stand on its own and answer three questions — *what's wrong,
how bad is it, and what do we do?* A typical structure:

- **Title** — concise and specific.
- **Risk rating** — e.g. Critical / High / Medium / Low / Informational, applied
  consistently.
- **Description** — what the weakness is, in clear language.
- **Impact** — what it means for *this* business if exploited.
- **Evidence** — enough to let the client verify and reproduce it.
- **Remediation** — clear, actionable steps to fix it.

> *Example finding (abbreviated):*
>
> **Title:** User input incorporated directly into a database query on the login
> form
> **Risk:** High
> **Impact:** Could allow an attacker to bypass authentication or access data
> they shouldn't.
> **Remediation:** Use parameterised queries / prepared statements so user input
> is never interpreted as part of the query.

## Writing for two audiences

A report usually has to serve both:

- **Executive / management** — a concise summary in business terms: overall
  posture, the handful of things that matter most, and what they imply. Little
  or no jargon.
- **Technical teams** — the detail they need to understand, reproduce, and fix
  each issue.

A good report lets each reader find what they need without wading through what
they don't.

## Best practices

- **Be clear and concise.** Plain language beats cleverness.
- **Rate consistently.** Use a defined scale and apply it the same way every
  time, considering both likelihood and impact.
- **Make remediation actionable.** "Fix the SQL injection" is weak; naming the
  concrete change is strong.
- **Prioritise.** Help the client see what to do first.
- **Be accurate and fair.** Don't inflate severity, and don't bury the serious
  under the trivial.

## The professional takeaway

Good reporting is where technical skill becomes business value. It's also, for
many newcomers, the most under-practised skill — and therefore one of the
fastest ways to stand out.

!!! note "Check your understanding"
    - Why should a critical finding sometimes be reported *during* the test
      rather than saved for the final report?
    - What are the essential components of a well-written finding?
    - How does writing for management differ from writing for a technical team,
      and why must a report do both?
