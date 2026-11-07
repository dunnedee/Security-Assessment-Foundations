# Common web vulnerabilities

## The concept

Web applications take input from untrusted users and act on it — displaying it,
storing it, using it to build database queries, making decisions with it. A huge
proportion of web weaknesses come from a single root cause: **the application
trusts input it shouldn't**, and fails to separate *data* from *instructions*.
Learn that pattern and the specific vulnerabilities become recognisable
variations.

The **[OWASP Top 10](https://owasp.org/www-project-top-ten/)** is the
authoritative, regularly-updated catalogue of the most critical categories.
What follows is an orientation to the recurring ones, at a conceptual level.

## Injection (including SQL injection)

**Injection** happens when user-supplied input is treated as part of a command
or query rather than as mere data. **SQL injection** is the classic example: if
an application builds a database query by pasting user input straight into it, a
crafted input can change the *meaning* of the query rather than just its values.

- **Impact:** depending on the case, reading data that should be off-limits,
  bypassing authentication, or altering data.
- **Root cause:** mixing untrusted input with query structure.
- **Fix:** **parameterised queries / prepared statements**, which keep input
  strictly as data and never let it alter the query's structure. Input
  validation and least-privilege database accounts add defence in depth.

This resource deliberately doesn't provide injection strings or exploitation
walkthroughs — the conceptual point is what matters for understanding and
defending, and hands-on practice belongs in a [lab](../getting-started/home-lab.md)
against applications built for it (such as OWASP Juice Shop or DVWA).

## Cross-Site Scripting (XSS)

**XSS** occurs when an application includes untrusted input in a web page without
properly neutralising it, so that a victim's browser executes attacker-influenced
script in the context of the trusted site.

- **Impact:** running script in other users' browsers — e.g. stealing session
  information or performing actions as the victim.
- **Root cause:** untrusted input reflected or stored into page output without
  proper encoding.
- **Fix:** context-appropriate **output encoding**, input validation, and
  defences such as a Content Security Policy.

## Broken access control

When an application **fails to properly enforce what a user is allowed to do** —
letting users reach data or functions that should be restricted. This includes
things like being able to access another user's records by changing an
identifier, or reaching admin functionality as an ordinary user.

- **Root cause:** access decisions not consistently enforced on the server for
  every request.
- **Fix:** enforce authorisation **server-side**, on every request, denying by
  default.

## Other recurring classes

- **Local/Remote File Inclusion** — tricking an application into including files
  it shouldn't, through unvalidated input used in file paths.
- **Security misconfiguration** — default accounts, verbose errors, unnecessary
  features left enabled.
- **Cross-Site Request Forgery (CSRF)** — causing a logged-in user's browser to
  make an unwanted request; mitigated with anti-CSRF tokens and sensible cookie
  settings.
- **Sensitive data exposure** — failing to protect data in transit or at rest.

## The unifying lesson

Across nearly all of these, the defensive principles repeat:

- **Never trust input.** Validate it; treat it as data, never as instructions.
- **Separate data from code** (parameterised queries, output encoding).
- **Enforce access control on the server**, for every request, deny-by-default.
- **Minimise and harden.** Remove defaults, limit privileges, reduce what's
  exposed.
- **Defence in depth.** No single control should be the only thing standing
  between an application and compromise.

## Tools (for context)

Professionals assess web applications with tools such as **Burp Suite** (an
intercepting proxy for inspecting and manipulating web traffic) and automated
helpers. These are instruments for *finding and validating* the weakness classes
above; the understanding of cause and fix is what makes them useful.

!!! note "Check your understanding"
    - What single root cause underlies most injection and scripting
      vulnerabilities?
    - Why do parameterised queries defeat SQL injection where input filtering
      alone may not?
    - Why must access control be enforced on the server rather than hidden in the
      interface?
