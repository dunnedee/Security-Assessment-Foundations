# Core technical skills

Everything an assessor does rests on a solid grasp of how systems communicate
and how data is protected. This section covers the technical foundations:

- **[Network protocols](network-protocols.md)** — how data moves, and where the
  design choices create risk.
- **[Cryptography fundamentals](cryptography.md)** — how confidentiality and
  integrity are achieved, and how weak choices undermine them.
- **[Hashing & password storage](hashing.md)** — how secrets are stored, and why
  some approaches hold up far better than others.

!!! tip "Don't skip the fundamentals"
    It's tempting to rush to the "interesting" offensive topics, but almost
    every weakness later in this resource is really a fundamentals problem in
    disguise — a protocol trusting something it shouldn't, or a weak
    cryptographic choice. Time spent here pays off everywhere else.
