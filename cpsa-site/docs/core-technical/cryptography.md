# Cryptography fundamentals

## The concept

Cryptography provides **confidentiality** (keeping data secret),
**integrity** (detecting tampering), and **authentication** (proving identity).
You don't need to be a mathematician, but you do need to understand what each
tool is *for* and how weak choices or misconfigurations undermine the protection
they're meant to provide.

## Symmetric vs asymmetric encryption

### Symmetric encryption

A **single shared key** both encrypts and decrypts. It's fast and well suited to
bulk data.

- Examples: **AES** (modern, strong), DES/3DES (legacy, weak/retired).
- The challenge: both parties need the same key, so **key distribution** is the
  hard part — how do you share the key securely in the first place?

### Asymmetric encryption

A **key pair**: a public key that can be shared freely, and a private key kept
secret. Data encrypted with one can be decrypted only with the other.

- Examples: **RSA**, **ECC** (elliptic curve), Diffie–Hellman (key agreement).
- It's computationally heavier than symmetric, so it's often used to securely
  establish a shared symmetric key, which then does the bulk work.

### How they work together

In practice, secure protocols combine both: asymmetric cryptography solves the
key-distribution problem by safely agreeing a symmetric session key, and the
fast symmetric cipher encrypts the actual traffic. This is, in essence, what
happens when you establish an HTTPS connection.

## Integrity and authentication

Encryption alone doesn't prove data wasn't altered, or who sent it. Other
primitives cover that:

- **Hashing** produces a fixed-size fingerprint of data; any change to the input
  changes the output. (See [Hashing & password storage](hashing.md).)
- **Message authentication codes (MACs)** and **digital signatures** combine
  hashing with a key to prove both integrity *and* origin.
- **Certificates** bind a public key to an identity, vouched for by a trusted
  authority — the basis of trust on the web.

## Transport security: TLS / SSL

**TLS** (the modern successor to the obsolete **SSL**) secures data in transit —
most visibly as the "S" in HTTPS. It negotiates which cryptographic algorithms
both sides will use, authenticates the server (via its certificate), and
establishes an encrypted channel.

The negotiation step is where a lot of real-world weakness lives: if a system
still permits old, broken protocol versions or weak ciphers, the overall
security drops to the weakest option it will accept.

## How cryptographic weakness shows up in an assessment

Assessors rarely "break" strong, correctly-used cryptography — they find it used
badly. Common themes, conceptually:

- **Obsolete algorithms** still in use (e.g. legacy ciphers long known to be
  weak).
- **Weak configurations** — a service that still accepts outdated protocol
  versions or weak cipher suites, allowing a connection to settle on something
  far weaker than the best available.
- **Unencrypted sensitive data**, in transit or at rest.
- **Poor key and certificate management** — expired, self-signed where it
  shouldn't be, or improperly protected keys.
- **Known implementation flaws** — named issues like Heartbleed, POODLE, or
  BEAST, which stem from specific protocol or library weaknesses rather than the
  underlying maths.

## Remediation themes

- **Use current, well-regarded algorithms** and retire deprecated ones.
- **Configure strongly** — disable obsolete protocol versions and weak ciphers
  so a connection can't be negotiated down to something weak.
- **Encrypt sensitive data** both in transit and at rest.
- **Manage keys and certificates properly** — protect private keys, rotate and
  renew, and use trusted authorities.
- **Keep libraries patched** — many famous cryptographic failures were fixed by
  a simple update.

## Quick reference

### Algorithms at a glance

| Algorithm | Type | Standing |
|---|---|---|
| **AES** | Symmetric | Strong, the modern standard |
| DES | Symmetric | Obsolete (key too short) |
| 3DES | Symmetric | Legacy; superseded by AES |
| RC4 | Symmetric (stream) | Broken; avoid (was used in WEP) |
| **RSA** | Asymmetric | Widely used; needs large keys |
| **ECC** | Asymmetric | Efficient; strong at smaller key sizes |
| Diffie–Hellman | Asymmetric (key exchange) | Establishes shared keys securely |
| MD5 | Hash | Broken (collisions); not for security |
| SHA-1 | Hash | Deprecated |
| **SHA-256 / SHA-512** | Hash | Current general-purpose hashes |
| **bcrypt / scrypt / Argon2** | Password hash | Purpose-built, deliberately slow |

### Cryptographic protocols

| Protocol | Secures |
|---|---|
| TLS (SSL is its obsolete predecessor) | Web and other traffic in transit |
| IPsec | VPNs and IP-layer traffic |
| SSH | Encrypted remote administration |
| S/MIME, PGP | Email and files |
| Kerberos | Authentication within networks |

### Attacks and defences

| Attack | Idea | Defence |
|---|---|---|
| Brute force | Try all keys | Strong algorithms, long keys |
| Man-in-the-middle | Intercept/alter in transit | TLS with proper authentication |
| Collision | Two inputs, same hash | Use SHA-256/512, not MD5/SHA-1 |
| Downgrade | Force a weaker option | Disable weak protocols/ciphers |
| Side-channel | Infer keys from behaviour | Vetted implementations, hardening |

!!! note "Check your understanding"
    - Why is asymmetric encryption often used to set up a symmetric key rather
      than to encrypt all the data itself?
    - If a server supports both a strong modern cipher and an old weak one, what
      determines the actual security of a given connection?
    - Why is "the maths is sound" not the same as "the system is secure"?
    - Which hash families are broken or deprecated, and what should be used
      instead — for general hashing, and specifically for passwords?
