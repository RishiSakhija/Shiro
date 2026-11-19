# Security Policy

## Reporting a Vulnerability

**Do not open a public issue.**

Email: **security@shiro.example.com** (placeholder — replace before launch)

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

We will acknowledge within 48 hours and work on a fix.

## Supported Versions

| Version | Supported |
|---------|-----------|
| Pre-alpha (main branch) | ✅ Security fixes only |

## Security Practices

### Secrets Management
- **Never commit secrets** to Git (API keys, DB passwords, tokens)
- Use `.env.local` for local development (gitignored)
- Production secrets: Vercel/Render environment variables
- Rotate keys quarterly

### Database (Supabase)
- Row Level Security (RLS) enabled on **all tables**
- Service role key **only** in agent service (server-side)
- Anon key for frontend only (public read policies)
- Regular RLS policy audits

### Authentication
- Supabase Auth (email/phone OTP, magic links)
- Owner admin panel: strict RLS, owner-only policies
- Session timeout: 24 hours
- No password storage (OTP-based)

### Agent Service
- Runs with Supabase service role (server-only)
- Reads/writes via approved proposals only
- Audit Agent monitors all writes
- Telegram bot token: server env only, owner chat ID allowlist

### Dependencies
- `pnpm audit` / `pip-audit` in CI
- Dependabot alerts enabled
- Pin versions in `package.json` / `requirements.txt`

### Data Protection
- PII: phone, email, address — encrypted at rest (Supabase default)
- No credit card data stored (handled by payment gateway)
- Order data: retained 7 years (Indian law)
- Audit logs: immutable, append-only

### Incident Response
1. Detect (monitoring, audit alerts, user report)
2. Contain (revoke keys, disable affected feature)
3. Investigate (audit logs, DB forensics)
4. Fix + deploy
5. Notify affected users (if data exposed)
6. Post-mortem (blameless, documented)