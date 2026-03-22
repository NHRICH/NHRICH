# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| `main`  | ✅ Active support |
| Older branches | ❌ No longer maintained |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

If you discover a security vulnerability in any project maintained in this repository, please disclose it responsibly:

1. **Email:** Send a detailed report to **security@nahom.tech**  
   *(Replace with your actual security contact if different.)*
2. **Subject line:** `[SECURITY] <short description>`
3. **Include in your report:**
   - A description of the vulnerability and its potential impact
   - Steps to reproduce or a proof-of-concept
   - Affected components or versions
   - Any suggested mitigations (optional)

## Response Timeline

| Stage | Target time |
|-------|-------------|
| Initial acknowledgement | Within **48 hours** |
| Severity assessment | Within **5 business days** |
| Patch / mitigation | Within **30 days** for critical issues |
| Public disclosure | After patch is released and users have had time to update |

## Scope

The following are **in scope** for vulnerability reports:

- Authentication and authorisation bypass
- Injection vulnerabilities (SQL, command, template, etc.)
- Sensitive data exposure
- Cross-Site Scripting (XSS) / Cross-Site Request Forgery (CSRF)
- Insecure direct object references (IDOR)
- Broken access control
- Misconfigured infrastructure (if exploitable)

The following are **out of scope**:

- Denial-of-service attacks requiring significant resources
- Social engineering attacks on contributors
- Vulnerabilities in third-party services outside our control
- Issues already reported or publicly known

## Security Best Practices for Contributors

- Never commit secrets, API keys, or credentials — use environment variables.
- Keep dependencies up-to-date; run `pip audit` / `npm audit` regularly.
- Follow the principle of least privilege for all service accounts and roles.
- Use parameterised queries; never interpolate user input into SQL.
- Validate and sanitise all user-supplied data on the server side.

## Acknowledgements

We are grateful to security researchers who responsibly disclose vulnerabilities. Confirmed valid reports may be acknowledged in release notes (with your permission).
