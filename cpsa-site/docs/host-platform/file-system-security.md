# File system security

## The concept

**File system security** is the protection of files and directories from
unauthorised access, modification, or deletion. It rests on two main mechanisms —
**permissions** (who can do what to which files) and **encryption** (making data
unreadable without a key) — and it's where the confidentiality and integrity of
data at rest are won or lost.

## Why it matters

Permissions are one of the most common sources of real findings. Overly
permissive files and directories enable information disclosure and
[privilege escalation](../exploitation-concepts/privilege-escalation.md); missing
encryption means a lost laptop or a copied disk exposes everything on it. This is
foundational host security.

## File systems and their security features

Different file systems offer different protections. A few worth recognising:

| File system | Platform | Security-relevant features |
|---|---|---|
| **NTFS** | Windows | Granular permissions (ACLs), encryption, journaling |
| **FAT32 / exFAT** | Cross-platform | Simple; **no permission model** |
| **ext4** | Linux | Permissions, ACLs, journaling |
| **APFS** | macOS | Encryption-capable, snapshots |
| **ZFS** | Linux/BSD | Integrity checking, snapshots, encryption |

The takeaway: the *file system itself* determines what protections are even
available. Storing sensitive data on one with no permission model (like FAT32 on a
USB stick) means there's nothing enforcing access control at all.

## Permissions

### Linux

Linux uses a compact owner / group / others model with read, write, and execute
rights, plus a few special bits:

| Right | Symbol | Meaning |
|---|---|---|
| Read | `r` | View file contents |
| Write | `w` | Modify the file |
| Execute | `x` | Run the file as a program |
| **SetUID** | `s` | Run the file with the **owner's** privileges, not the runner's |
| Sticky bit | `t` | In a shared directory, only owners can delete their files |

**SetUID** is especially security-relevant: a SetUID-root program runs with root
privileges regardless of who starts it, so a vulnerable or misconfigured one is a
classic escalation path. Assessors pay close attention to SetUID binaries, and
defenders should minimise and scrutinise them.

### Windows

Windows uses **ACL-based permissions** — Read, Write, Modify, Full Control, and
custom "special" permissions — assigned to users and groups. **Full Control** is
the one to watch: it includes the ability to change permissions themselves, so
handing it out loosely undermines the whole model.

## Encryption at rest

Permissions protect data while the system enforces them; **encryption** protects
it even when it doesn't (a stolen disk, a copied file). Common tools include
**BitLocker** (Windows), **LUKS** (Linux), **FileVault** (macOS), **VeraCrypt**
(cross-platform), and **GPG** for individual files. Full-disk encryption is the
baseline for portable devices.

## Common file system attacks (and defences)

| Attack (concept) | Root cause | Defence |
|---|---|---|
| **Privilege escalation** via weak permissions | Over-permissive files, risky SetUID binaries | Strict least-privilege permissions; audit SetUID |
| **Data exfiltration** | Sensitive files accessible and unmonitored | Access control, DLP, monitoring |
| **Log manipulation** | Writable logs let an intruder erase traces | Centralised, integrity-protected logging |
| **Ransomware** (impact on files) | Broad write access, no recovery | Backups, least privilege, endpoint protection |

## Defensive themes

- **Least privilege on files and directories.** Grant the minimum access needed;
  review permissions regularly.
- **Scrutinise special permissions** — SetUID/SetGID binaries on Linux, Full
  Control grants on Windows.
- **Encrypt data at rest**, especially on portable devices.
- **Protect logs** with centralised collection and integrity checks.
- **Back up** important data so destructive attacks are survivable.
- **Use a file system that supports access control** for anything sensitive.

!!! note "Check your understanding"
    - Why is storing sensitive data on a file system with no permission model
      (like FAT32) a problem?
    - What makes a SetUID-root binary a potential privilege-escalation path?
    - Permissions and encryption both protect data at rest — what does encryption
      protect against that permissions alone do not?
