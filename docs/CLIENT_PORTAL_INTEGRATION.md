# Client Portal Integration Plan

This document records the recommended groundwork for adding a future M45 client portal to the Webflow website.

Status:

- Planning only.
- No live Webflow navigation or code changes have been made for the portal yet.

## Short Answer

Yes, a client portal is feasible.

Recommended architecture:

- Keep `www.m45capital.com` as the public Webflow marketing site.
- Build the portal as a separate secure application.
- Attach it to the brand through a subdomain such as:
  - `portal.m45capital.com`
  - `app.m45capital.com`
  - `clients.m45capital.com`
- Add a restrained `Client Portal` entry to the Webflow header only when the portal is ready for controlled access.

Do not build sensitive client-account functionality purely inside Webflow custom code.

## Why The Portal Should Be A Separate Secure App

The public Webflow site is excellent for:

- Marketing pages
- Public research pages
- Newsroom updates
- Public PDF hosting
- Brand and contact flows

A client portal likely needs:

- Authentication
- MFA
- Authorization by client, household, advisor, and administrator
- Secure document access
- Audit logs
- Session management
- Private client data storage
- Administrative tooling
- Compliance review
- Incident response processes

Those are application responsibilities, not marketing-site responsibilities.

## Current Webflow Reality

As of 2026-07-07:

- Webflow User Accounts is being sunset. Webflow says User Accounts will no longer be available on January 29, 2026 and cannot be enabled on new sites after January 31, 2025.
- Webflow custom code has character and lifecycle limits. It is useful for site behaviour, but it is not the right security boundary for client data.
- Webflow Cloud can deploy full-stack apps such as Next.js and Astro alongside Webflow sites, which may be useful if M45 wants to keep hosting under the Webflow platform.

References:

- Webflow User Accounts sunset: `https://help.webflow.com/hc/en-us/articles/36046006227731-User-Accounts-sunset`
- Webflow User Accounts overview: `https://help.webflow.com/hc/en-us/articles/33961356432147-Webflow-User-Accounts-overview`
- Webflow Cloud docs: `https://developers.webflow.com/webflow-cloud/intro`
- Webflow custom code docs: `https://help.webflow.com/hc/en-us/articles/33961357265299-Custom-code-in-head-and-body-tags`

## Recommended Architecture

### Option A: Separate Portal App On A Subdomain

Recommended default.

Example:

```text
www.m45capital.com              Public Webflow site
portal.m45capital.com           Secure client portal app
```

Benefits:

- Clear security boundary.
- Webflow site stays simple and stable.
- Portal can use a proper backend, auth provider, database, file store, and audit logging.
- Easier compliance review.
- Easier to take the portal down or restrict access without affecting the public website.

### Option B: Webflow Cloud App

Potentially viable if the portal is built with a supported full-stack framework and the team wants Webflow-hosted app deployment.

Use only after confirming:

- Framework support.
- Runtime limits.
- Data storage model.
- Environment variable handling.
- Logging and audit requirements.
- Access-control needs.
- Security review comfort.

### Option C: Webflow + Third-Party Membership Tool

Potentially useful for low-risk gated content.

Not recommended for a true financial client portal containing sensitive client information unless compliance and security requirements are carefully reviewed.

### Option D: Webflow Native User Accounts

Not recommended.

Reason:

- Webflow User Accounts is being sunset.

## What Should Not Live In Webflow

Do not put these in Webflow CMS, Webflow forms, public assets, or front-end custom code:

- Client names tied to portfolios or confidential documents.
- Account statements.
- Portfolio holdings.
- Subscription or redemption documents.
- KYC/AML documents.
- Identification documents.
- Private investor communications.
- Access tokens or API keys.
- Client-specific permissions.
- Any secret used by the portal backend.

## Groundwork To Put In Place Now

### 1. Reserve The Portal URL

Pick the future URL convention now.

Recommended:

```text
portal.m45capital.com
```

Reasons:

- Clear to clients.
- Easy to separate from the public site.
- Easy to protect with its own app, DNS, TLS, WAF, logging, and auth settings.

Do not add it to the public nav until there is a real secure destination.

### 2. Define The Portal App Contract

The portal-building chat should define:

- Framework: e.g. Next.js
- Hosting: e.g. Vercel, AWS, Azure, Cloudflare, or Webflow Cloud
- Auth provider: e.g. OIDC-compatible provider
- MFA policy
- User roles
- Database
- File storage
- Audit log storage
- Admin console route
- Client route
- Session lifetime
- Password/passwordless policy
- Support and lockout process

### 3. Define Roles Early

Minimum suggested roles:

- `client`
- `advisor`
- `operations`
- `admin`
- `super_admin`

Consider relationship structures:

- Client belongs to one or more households/entities.
- Advisor can view assigned clients only.
- Operations can manage documents and onboarding status.
- Admin can manage users and permissions.

### 4. Define Security Baseline

Minimum expectations:

- MFA for all client and admin accounts.
- Strong session handling.
- Role-based access control.
- Server-side authorization checks on every private route and file download.
- Audit logs for login, logout, failed login, document view, document download, upload, permission change, and admin impersonation if used.
- Encryption in transit and at rest.
- Secrets stored only in the app hosting secret manager.
- No secrets in Webflow.
- No private client documents on public Webflow CDN.
- Backups and restore tests.
- Incident response playbook.

For Singapore financial-services context, review MAS technology risk expectations with the appropriate compliance/legal/security reviewers.

References:

- MAS Technology Risk Management Guidelines: `https://www.mas.gov.sg/regulation/guidelines/technology-risk-management-guidelines`
- MAS Cyber Security requirements overview: `https://www.mas.gov.sg/regulation/cyber-security`
- MAS Notice on Cyber Hygiene example: `https://www.mas.gov.sg/regulation/notices/notice-fsm-n06`

This repo is not legal or compliance advice. Treat these links as prompts for proper review.

### 5. Define Brand And UX Contract

The portal should feel like M45, but it should not inherit the public website layout blindly.

Keep:

- M45 logo treatment
- Quiet editorial typography
- Deep navy/off-white palette
- Restrained interactions
- Clear spacing
- Premium institutional feel

Change for portal usability:

- Use denser layouts for dashboards.
- Prefer clear tables, lists, filters, and upload states.
- Use explicit security and session states.
- Avoid heavy page-load animation inside logged-in workflows.
- Make document actions obvious and accessible.

### 6. Define Webflow Handoff Points

When ready, the Webflow site should add:

- Desktop utility link: `Client Portal`
- Mobile menu link: `Client Portal`
- Optional footer link
- Optional no-index public portal landing page if needed

The link should point to the portal app subdomain, not to a Webflow member page.

Recommended target behaviour:

- Same tab for normal client portal entry.
- Use a clear external-app URL, e.g. `https://portal.m45capital.com`.

### 7. Keep Public And Private Research Separate

Public Research & Insights can remain on Webflow.

Private client-only documents should live in the portal:

- Not Webflow CMS.
- Not public Webflow CDN.
- Not direct unauthenticated PDF links.

If a whitepaper is public, it can stay in Research & Insights.

If a document is client-specific or confidential, it belongs in the portal.

## Future Webflow Change Checklist

When the portal is ready:

1. Confirm the production portal URL.
2. Confirm the portal has authentication, MFA, logging, and access controls.
3. Add `Client Portal` to desktop nav or utility nav.
4. Add `Client Portal` to mobile menu.
5. Add footer link only if desired.
6. Confirm it does not disturb the existing nav spacing:
   - `Our Investment Philosophy`
   - `What We Do`
   - `Our Leadership`
   - `Newsroom`
   - `Research & Insights`
   - `Client Portal` if approved
   - `Get In Touch`
7. Test desktop and mobile.
8. Update `docs/SITE_ARCHITECTURE.md`, `docs/QA_CHECKLIST.md`, and `CHANGELOG.md`.
9. Publish staging and production.

## Suggested Prompt For The Portal-Building Codex Chat

Use this in the other Codex chat building the portal:

```text
This portal will eventually connect to the public M45 Webflow site.
The Webflow repo is C:\Users\gordo\Documents\Codex\2026-07-01\are\work\m45-webflow-custom-code.
Read docs/CLIENT_PORTAL_INTEGRATION.md before choosing routes or branding.
Assume the public site remains on www.m45capital.com and the portal should live on a separate subdomain, preferably portal.m45capital.com.
Do not rely on Webflow User Accounts.
Do not store private client documents or secrets in Webflow.
Design for MFA, server-side authorization, audit logs, and private file access from the start.
```

## Open Decisions

- Final portal URL.
- Hosting provider.
- Authentication provider.
- Whether clients will see portfolio data, documents only, onboarding flows, or all three.
- Whether advisors and operations users need internal admin workflows.
- Whether documents require watermarks, expiry links, or download restrictions.
- Whether the portal should support e-signature workflows.
- Who owns compliance/security sign-off.

