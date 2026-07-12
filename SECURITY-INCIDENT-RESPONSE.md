# Synorai EcoCharge — Security Incident Response Policy

_Effective: July 11, 2026 · Owner: Synorai Inc. (owner-operator)_

## Scope

Covers any suspected or confirmed security incident affecting the Synorai
EcoCharge application, its database, its hosting (Render), or the credentials
that control them (Shopify Partner account, GitHub, Render).

Data inventory context: the application stores merchant configuration and
order-level remittance records (destination province/country code, order
number, fee amounts). It stores **no customer names, addresses, emails, or
phone numbers**, which materially limits the impact of any breach.

## Detection

- Hosting and application logs are reviewed when anomalies are reported
  (failed webhooks, unexpected admin actions, provider alerts).
- Provider notifications (Render, GitHub, Shopify) are delivered to the
  owner's monitored email.

## Response steps

1. **Contain** — revoke or rotate affected credentials immediately:
   Shopify API secret (Partner Dashboard), GitHub keys/tokens, Render
   deploy keys and database credentials. Suspend the affected service if
   necessary.
2. **Assess** — determine what data was exposed, for which stores, and over
   what window, using application and provider logs.
3. **Notify** — affected merchants are notified promptly (target: within 72
   hours of confirmation) via the app's support email, with a plain-language
   description of what happened, what data was involved, and what is being
   done. Shopify is informed through partner support channels.
4. **Remediate** — patch the vulnerability, redeploy, and verify.
5. **Record** — write a dated post-incident summary (cause, impact, fix,
   prevention) and retain it in this repository.

## Prevention measures in force

- All access in transit over TLS; database and backups encrypted at rest.
- Two-factor authentication on Shopify Partner, GitHub, and hosting accounts.
- Least-privilege data design: no customer PII stored by design.
- Automatic data deletion on app uninstall and `shop/redact`.
- Code changes ship via version-controlled pull requests.

## Contact

support@synorai.ai
