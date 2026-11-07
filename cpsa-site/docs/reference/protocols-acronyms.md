# Protocols & acronyms

A reference for the networking and security protocols and acronyms that come up
constantly. Understanding what each does — and which have secure alternatives —
is foundational fluency.

## Common protocols

| Protocol | Full name | Purpose |
|---|---|---|
| HTTP | Hypertext Transfer Protocol | Web communication (unencrypted) |
| HTTPS | HTTP Secure | Web communication encrypted with TLS |
| FTP | File Transfer Protocol | File transfer (unencrypted) |
| SFTP | SSH File Transfer Protocol | File transfer over SSH (encrypted) |
| SSH | Secure Shell | Encrypted remote access and transfer |
| Telnet | — | Remote access (**unencrypted**, legacy) |
| SMTP | Simple Mail Transfer Protocol | Sending email |
| POP3 | Post Office Protocol v3 | Retrieving email (downloads it) |
| IMAP | Internet Message Access Protocol | Retrieving email (keeps it on server) |
| DNS | Domain Name System | Resolving names to IP addresses |
| DHCP | Dynamic Host Configuration Protocol | Assigning IP addresses automatically |
| SNMP | Simple Network Management Protocol | Managing/monitoring network devices |
| LDAP | Lightweight Directory Access Protocol | Directory access and authentication |
| TLS | Transport Layer Security | Encrypting communications (modern) |
| SSL | Secure Sockets Layer | Encryption (legacy, superseded by TLS) |
| IPsec | Internet Protocol Security | Securing IP traffic, VPNs |
| NTP | Network Time Protocol | Clock synchronisation |

## Secure vs insecure pairings

This is the single most useful table to internalise — the insecure protocol and
the secure one that should replace it.

| Insecure | Secure | What changes |
|---|---|---|
| **HTTP** | **HTTPS** | TLS encryption of web traffic |
| **FTP** | **SFTP** / FTPS | Encrypted file transfer |
| **Telnet** | **SSH** | Encrypted remote access |
| **LDAP** | **LDAPS** | Encrypted directory access |
| **SNMPv1/v2** | **SNMPv3** | Authentication and encryption |
| **POP3/IMAP** (plain) | **POP3S/IMAPS** | TLS-protected email retrieval |

> **Rule of thumb:** if a protocol has a secure variant, prefer it — and treat the
> presence of the insecure one as a finding worth noting.

## Selected acronyms

| Acronym | Full form | Note |
|---|---|---|
| TKIP | Temporal Key Integrity Protocol | Legacy Wi-Fi (WPA); weak |
| IKE | Internet Key Exchange | Key management for IPsec VPNs |
| SOAP | Simple Object Access Protocol | Structured web-service messaging |
| WSDL | Web Services Description Language | Describes web services |
| XML | Extensible Markup Language | Structured data format |
| AJAX | Asynchronous JavaScript and XML | Interactive web technique |
| ISAPI | Internet Server API | Microsoft web-server extension interface |
| AAA | Authentication, Authorisation, Accounting | Access-control framework |
| ACL | Access Control List | Rules governing access |
| MFA | Multi-Factor Authentication | Multiple proofs of identity |

!!! info "Why the secure/insecure framing matters"
    Much of foundational network security is recognising when something is using a
    weak, unencrypted, or legacy protocol where a secure option exists. That
    recognition — and knowing the replacement — is exactly the judgement these
    tables are meant to build.
