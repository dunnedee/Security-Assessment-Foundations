# Hashing & password storage

## The concept

A **hash function** turns input of any size into a fixed-size fingerprint. Good
cryptographic hashes are *one-way* (you can't reverse them to recover the input)
and *collision-resistant* (it's infeasible to find two inputs with the same
output). Hashing is how systems can store and verify passwords without keeping
the actual password — and how they detect whether data has changed.

## Why it matters

Password storage is one of the most consequential design decisions a system
makes. If credentials are stored well, a database breach is survivable; if
they're stored badly, a breach hands attackers usable passwords. Understanding
the difference is core knowledge for both assessing and building systems.

## Hashing vs encryption

A common beginner confusion, worth nailing down:

- **Encryption** is two-way — data is protected but can be recovered with the
  key.
- **Hashing** is one-way — there's no "key" to turn the fingerprint back into
  the original.

Passwords should be **hashed**, not encrypted: the system never needs to recover
the original password, only to check whether a submitted one matches.

## Why not all hashing is equal

Not every hash function is suitable for passwords.

- **General-purpose hashes** (like the SHA family) are designed to be *fast* —
  which is exactly what you *don't* want for passwords, because speed helps
  anyone trying large numbers of guesses.
- **Older algorithms** such as MD5 are considered broken for security use and
  shouldn't protect anything that matters.
- **Password-hashing algorithms** (such as **bcrypt**, **scrypt**, and
  **Argon2**) are deliberately *slow* and resource-intensive, and are built for
  exactly this job. That deliberate cost is a feature.

On many systems you can recognise the scheme from a prefix on the stored value —
for example different prefixes distinguish MD5-based, SHA-256-based, SHA-512-based,
and bcrypt hashes. Windows environments historically used NTLM hashes, which
have their own well-known weaknesses.

## Salting (and why it's essential)

A **salt** is a unique random value added to each password before hashing.
Without salts:

- Identical passwords produce identical hashes, so patterns leak.
- Precomputed lookup tables (so-called rainbow tables) can reverse common hashes
  quickly.

A unique salt per password defeats precomputation and ensures two users with the
same password still get different stored hashes. Modern password-hashing
algorithms handle salting for you.

## How weak password storage shows up in an assessment

Conceptually, an assessor looks at *how* credentials and other secrets are
stored and asks:

- Are passwords stored in plaintext, or reversibly encrypted, when they should
  be hashed? (A serious finding.)
- Is a fast or obsolete algorithm used where a slow password-hashing algorithm
  should be?
- Are salts used, and are they unique?
- Are weak or default passwords in use, which undermine even good hashing?

The *tools* that attackers use to test the strength of recovered hashes (such as
password-cracking utilities) exist and are widely known; the assessment point is
simply that **weak storage dramatically lowers the cost of turning a breach into
usable credentials**, and strong storage raises it enormously.

## Remediation themes

- **Hash passwords with a purpose-built, slow algorithm** — bcrypt, scrypt, or
  Argon2.
- **Always salt**, uniquely per credential (modern algorithms do this).
- **Retire broken algorithms** like MD5 for any security purpose.
- **Enforce strong password policies** and support multi-factor authentication,
  so a single recovered or guessed password isn't game over.
- **Never store plaintext or reversibly-encrypted passwords.**

!!! note "Check your understanding"
    - Why should passwords be hashed rather than encrypted?
    - Why is a *fast* hash function a poor choice for storing passwords?
    - What problem does salting solve that a strong algorithm alone does not?
    - How does multi-factor authentication limit the damage even if a password
      hash is recovered and cracked?
