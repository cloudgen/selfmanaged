# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.0.0 (current) | Yes |
| Older releases | No public support matrix yet — report issues against the current release when possible |

## Reporting a Vulnerability

Please **do not** open a public issue for security-sensitive reports when a private channel is available.

**Maintainer contact (email):** `cloudgen.wong@gmail.com`

- Source of contact: product **author-email** SSOT in [`LICENSE.md`](./LICENSE.md) (Copyright line).  
- Prefer email for vulnerability details, reproduction steps, and impact.  
- You should receive an acknowledgment when the report is received and actionable.  
- Do not include exploit weaponization guides in public channels.

For non-sensitive questions, product usage, or general bugs that are not security-sensitive, use normal project channels (for example public issues on the project repository when available).

## Security Design Principles (CIAO)

This project follows **[CIAO](https://github.com/cloudgen/ciao)** / **CIAO-Lite** defensive design. Security-relevant intent:

| Letter | Principle | Security application |
|--------|-----------|----------------------|
| **C** | **Caution** | Assume hostile input, hostile networks, and misconfiguration. Validate install paths, checksums, and privilege boundaries; fail closed on integrity mismatch when a digest is present. |
| **I** | **Intentional** | Privilege typing (Type 0 self-management), channel URL (`SCRIPT_URL`), and checksum modes are deliberate and documented—not accidental. Prefer clear “why” over silent magic. |
| **A** | **Anti-fragile** | Survive harsh environments (minimal containers, missing tools, non-interactive `curl \| sh`). Prefer automatic SHA-256 sidecar checks when available, least privilege for day-to-day use, and recoverable failure over brittle trust. |
| **O** | **Over-protect** | Defense in depth on critical paths (integrity verify before install/update, CIAO Protection Zones in the ship unit, loud failure). Do not “simplify away” safety for brevity. |

Full principles: [CIAO Defensive Programming](https://github.com/cloudgen/ciao) · agent contract: [CIAO-Lite](https://github.com/cloudgen/ciao-lite).

This section describes **design posture**. It is **not** a claim of third-party certification (ISO, OWASP “compliant”, etc.).

## Scope notes

- Preferred language for reports: English.  
- Out of scope: social engineering of third parties, physical attacks, spam.  
- Online install integrity: automatic `${SCRIPT_URL}.sha256` (SHA-256) when present; optional strict `CHECKSUM` pin — see [`README.md`](./README.md).  
- Related product docs: [`README.md`](./README.md), [`LICENSE.md`](./LICENSE.md), [`CHANGELOG.md`](./CHANGELOG.md).
