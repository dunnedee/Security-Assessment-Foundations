# Web reconnaissance

## The concept

Web servers reveal a lot about how they're built and configured — sometimes
deliberately, often inadvertently. Web reconnaissance is about reading those
signals to understand the application and its hosting, as a precursor to deeper
assessment.

## HTTP headers

Every web response carries **headers** — metadata about the response and the
server. They can reveal:

- **Server and technology hints** — software and sometimes version information,
  frameworks, and platforms in use.
- **Security posture** — the presence or absence of protective headers (for
  content security, transport security, framing protection, and so on) tells you
  how carefully the application was hardened.

For an assessor, headers are a quick, non-intrusive read on how mature a
deployment is. Missing security headers aren't a breach in themselves, but they
indicate gaps worth examining.

## Virtual hosts

A single server, on a single IP address, commonly hosts **many** websites. It
decides which site to serve based on the **Host header** the browser sends —
this is **virtual hosting**.

This matters for reconnaissance because:

- One IP address can front multiple distinct applications.
- Some of those virtual hosts may be intended for internal or administrative
  use, and may behave differently — or reveal more — than the public site.

Understanding virtual hosting explains why "one server" can actually mean many
applications with different security characteristics, and why enumerating which
names a server responds to is part of building an accurate picture.

## The Host header as a trust problem

Because the application often *trusts* the Host header to decide what to serve
or how to build links, a server that doesn't validate it properly can behave in
unintended ways when that header is manipulated. Conceptually this is an example
of a recurring theme: **trusting client-supplied input**. The defensive answer
is the same as it always is — validate it.

> *Example (conceptual):* If a server will serve an administrative virtual host
> to any request that simply claims that host name, then access control is
> resting on something the client fully controls — which is no access control at
> all.

## Other web recon signals

- **Error messages** that reveal software versions, file paths, or stack
  details.
- **Default or sample content** left in place, indicating an incomplete
  hardening process.
- **Robots files and sitemaps**, which sometimes point to areas the owner would
  rather weren't indexed (and therefore sometimes to interesting paths).
- **Response differences** that distinguish real resources from missing ones.

## Remediation themes

- **Minimise information disclosure.** Suppress unnecessary version banners and
  detailed error messages in production.
- **Set security headers.** Adopt the recommended protective response headers for
  your platform.
- **Validate the Host header** and don't let it drive security decisions or
  access control.
- **Separate and protect internal/admin interfaces** rather than relying on them
  being unadvertised.
- **Remove default and sample content** before going live.

!!! note "Check your understanding"
    - What can HTTP response headers tell an assessor about an application's
      maturity?
    - Why can a single IP address host many applications with different security
      characteristics?
    - The Host header is supplied by the client. Why does trusting it for access
      decisions break down?
