# TARZO storefront security — v13

Security controls in this release:

- Public storefront stays public; customers still browse, join the Circle and open WhatsApp orders.
- Server-level Content Security Policy, HTTPS enforcement, clickjacking restrictions, MIME sniffing protection, restricted browser permissions, safe referrer policy and no caching of admin/API responses.
- Signup, newsletter, inquiry and owner-login POSTs require a same-origin browser request and JSON payloads with a server-enforced streamed body-size limit.
- Shared Cloudflare D1 request counters throttle repeated submissions by the edge-provided visitor IP. Limits are 8 owner-login attempts per 15 minutes, 12 Circle signups per hour, 20 newsletter requests per hour, and 10 legacy form inquiries per hour.
- D1 counters store only a rolling SHA-256 fingerprint, not the raw visitor IP. Old counters are removed opportunistically.
- Owner dashboard data endpoints require a signed, expiring HTTP-only, Secure, SameSite=Strict session cookie and the configured secret owner key. Keep `TARZO_ADMIN_KEY` in Sites secrets, never in source or browser code.
- Cross-origin WhatsApp redirects retain a fixed TARZO number. User-supplied message text is encoded by the URL API and limited to 1,900 characters.

## Account controls required outside website code

The current Sites project record reports **papanotify@gmail.com** as the owner; this release **does not transfer ownership**. Complete an authorized ownership transfer to **humzacrypto@gmail.com** using the Sites/ChatGPT account management UI if that is still your intended owner, and verify the new account is shown as owner before removing the old one. Do not share password, secret key, 2FA codes or source repository credentials.

Turn on strong two-factor authentication/passkeys for the owner account, periodically review editors and external viewers, and remove unknown access. A public Site permits viewing; it does not grant publishing rights. If available in account settings, disable public remix/forking and require explicit owner approval for connected automation or AI editing. Site code cannot revoke or override the hosting owner's administrative permissions.

Check Cloudflare/Sites WAF, bot management, rate-limit analytics and alerts from the hosting account. Those edge-level features complement these app limits, and require a hosting plan/control panel to configure. Keep source and database backups and review deployed version history.

No website is guaranteed impossible to attack. This release does not stop a legitimate owner/editor (or any authorized automation) from making changes; only hosting/account permissions and credential controls can govern that.
