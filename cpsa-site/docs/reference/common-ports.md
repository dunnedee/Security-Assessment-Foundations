# Common ports

Ports identify which service network traffic is destined for. Recognising the
common ones is basic fluency — it lets you read a scan result at a glance and
reason about what a system is exposing. Defaults are conventions, not rules
(services can run anywhere), but knowing them speeds up everything.

## Ports worth knowing

| Port | Service | Notes |
|---|---|---|
| 21 | FTP | File transfer (unencrypted) |
| 22 | SSH / SFTP | Encrypted remote access and transfer |
| 23 | Telnet | Remote access (**unencrypted**, legacy) |
| 25 | SMTP | Sending email |
| 53 | DNS | Name resolution (TCP and UDP) |
| 67/68 | DHCP | Automatic IP assignment |
| 80 | HTTP | Web (unencrypted) |
| 110 | POP3 | Email retrieval |
| 123 | NTP | Time synchronisation |
| 135 | RPC | Windows remote procedure call |
| 137–139 | NetBIOS | Legacy Windows networking (SMBv1 era) |
| 143 | IMAP | Email retrieval |
| 161/162 | SNMP | Device management/monitoring |
| 389 | LDAP | Directory access |
| 443 | HTTPS | Web (TLS-encrypted) |
| 445 | SMB | Windows file/printer sharing |
| 514 | Syslog | System logging |
| 636 | LDAPS | LDAP over TLS |
| 993 | IMAPS | IMAP over TLS |
| 995 | POP3S | POP3 over TLS |
| 1433 | MS SQL Server | Microsoft database |
| 1521 | Oracle TNS | Oracle database listener |
| 3306 | MySQL | Database |
| 3389 | RDP | Windows Remote Desktop |
| 5432 | PostgreSQL | Database |
| 5900 | VNC | Remote desktop control |

## Port ranges

| Range | Category | Meaning |
|---|---|---|
| 0–1023 | Well-known | Standard services, assigned by IANA |
| 1024–49151 | Registered | Assigned to specific applications |
| 49152–65535 | Dynamic / private | Temporary, client-side connections |

## Ports and security

A few principles tie ports back to defence:

- **Every open port is attack surface.** The safest service is one that isn't
  running and whose port is closed.
- **Close or filter what you don't need.** Firewalls and host configuration should
  expose only the services that must be reachable, and only to those who need them.
- **Watch the legacy/unencrypted ones.** Seeing Telnet (23), FTP (21), or SMBv1
  (139) is worth a second look — prefer the encrypted equivalents.
- **Databases should rarely face the world.** Ports like 1433, 3306, 5432, 1521
  being broadly reachable is a common and serious exposure.
- **Audit regularly.** Know what you have open; discovery shouldn't surprise you.

!!! note "A quick self-test"
    Cover the right-hand columns and see if you can name the service for 22, 53,
    80, 443, 445, and 3389 — and for each, say whether it's encrypted and what you'd
    check if you found it open.
