# Risk management

## The concept

Testing a live system carries its own risks — the act of assessing something can
disturb it. Risk management is about anticipating those risks, reducing them,
and keeping the client informed, so the engagement itself doesn't cause the harm
it was meant to help prevent.

## Why it matters

A test that knocks a production service offline, corrupts data, or triggers a
full incident response has failed — regardless of what it found. Managing risk
well is what lets a client trust you anywhere near their important systems, and
it's a mark of a mature tester.

## Common risks introduced by testing

- **Service disruption / downtime.** Aggressive activity — heavy scanning, high
  request volumes — can overwhelm fragile devices or services and cause an
  outage.
- **Data loss or corruption.** Interacting with a live database or application in
  certain ways can, in the worst case, damage or delete data.
- **False alarms.** The client's own security monitoring may detect the testing
  and treat it as a genuine attack, pulling in an incident response team
  unnecessarily.
- **Exposure of sensitive data.** Testing can surface personal or regulated data
  that must then be handled with care.

## Mitigation strategies

Good testers plan these in before they start:

- **Prefer non-production environments** where feasible. A staging or test
  environment that mirrors production lets you work without risking the live
  service.
- **Control intensity.** Pace and tune activity to what the target can bear;
  avoid blunt, high-volume approaches against fragile systems.
- **Coordinate monitoring.** Let the client's security team know the testing
  window and source addresses so genuine alerts aren't confused with the test
  (while being careful this doesn't invalidate the test's purpose).
- **Agree stop conditions.** Define up front what causes testing to pause — e.g.
  signs of instability — and who to contact.
- **Keep communication open.** Stakeholders should never be surprised. Flag
  risks before they materialise, and serious findings as they arise.

> *Example:* Rather than demonstrate a data-affecting weakness directly against a
> live database, a tester reproduces it in a controlled environment, or confirms
> it in a non-destructive way and reports it — preserving the client's data while
> still evidencing the risk.

## Communicating risk to clients

Risk management isn't only technical — it's about expectation-setting:

- Explain, in plain terms, what could go wrong and how likely it is.
- Agree how much risk the client is willing to accept, and reflect that in the
  [RoE](scoping.md#rules-of-engagement-roe).
- During the test, keep the relevant people informed in a way they understand —
  technical detail for the technical team, business impact for management.

## Putting numbers on risk

So far this page has treated risk qualitatively, which is how it's usually
communicated. But it helps to know the standard ways risk is *quantified*, because
you'll meet them in frameworks and reports.

The core idea is that risk combines **how likely** something is with **how bad** it
would be:

| Model | Formula | In plain terms |
|---|---|---|
| Basic risk | Risk = Likelihood × Impact | The fundamental shape of every risk model |
| Information security risk | Risk = Threat × Vulnerability × Impact | A threat only matters if a vulnerability exists for it to exploit |
| Single Loss Expectancy | SLE = Asset Value × Exposure Factor | The cost of **one** occurrence |
| Annualised Loss Expectancy | ALE = SLE × ARO | Expected yearly cost (ARO = annual rate of occurrence) |

These feed **quantitative** risk assessment (assigning monetary/numeric values),
as opposed to **qualitative** assessment (High/Medium/Low judgement). Most
real-world work blends both — numbers where they're available, judgement where
they aren't.

The components these formulas combine are worth naming precisely:

- **Threat** — something that could cause harm (malware, an insider, an attacker).
- **Vulnerability** — a weakness a threat could exploit (unpatched software, weak
  passwords).
- **Likelihood** — the probability a threat successfully exploits a vulnerability.
- **Impact** — the damage if it does (financial, data, reputational).
- **Mitigation** — the controls that reduce likelihood or impact.

A threat with no matching vulnerability, or a vulnerability no threat can reach, is
low risk — which is exactly why assessment focuses on where threats and
vulnerabilities *meet*.

## Risk management frameworks

You don't manage risk from scratch — established frameworks provide the structure:

| Framework | Focus |
|---|---|
| **NIST RMF / CSF** | Structured US-originated risk management and security controls |
| **ISO 27001 / 27005** | International standard for security management (27001) and risk (27005) |
| **CIS Critical Security Controls** | A prioritised, practical set of defensive controls |
| **FAIR** | A model for quantitative risk analysis |
| **MITRE ATT&CK** | A catalogue of real-world attacker tactics and techniques, useful for threat modelling |

These give a common language and a repeatable process, which matters when risk has
to be communicated, compared, and defended over time.

## The professional takeaway

The best testers are the ones clients trust with their crown jewels, precisely
because those testers so visibly manage the risk of the work. Caution and
clear communication are not timidity — they're professionalism.

!!! note "Check your understanding"
    - Name three distinct risks that the act of testing can introduce, and a
      mitigation for each.
    - Why might you choose to *report* a data-affecting weakness rather than
      fully demonstrate it against a live system?
    - How does good risk communication differ for a technical team versus
      senior management?
