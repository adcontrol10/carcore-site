# CarCore domain plan — inspected October 3, 2026

## User's revised routing

- carcore.us: PUBLIC sales website, GitHub Pages in adcontrol10/carcore-site.
- carcore.pro: PRIVATE customer portal, behind real login. Do not redirect it to .us or expose its content through Pages.
- renew.carcore.pro or carcore.pro/renew: pending user's choice, service and payment/renewal integration.
- download.carcore.pro or carcore.pro/download: pending user's choice, authenticated download service. Do not upload installers to this public repository.
- mail.carcore.pro: HTTP redirect to https://mail.zoho.com. Current website Email login links go directly to Zoho while this alias is unconfigured.

## Current services: preserve

Both domains currently use IONOS nameservers ns1028.ui-dns.com, ns1046.ui-dns.de, ns1020.ui-dns.biz, ns1090.ui-dns.org. Root A currently 74.208.236.141 and root AAAA should be reviewed before changes. Both HTTP sites show the IONOS default-page redirect. Current MX: priority 10 mx00.ionos.com and mx01.ionos.com. SPF: v=spf1 include:_spf-us.ionos.com ~all. These email records were NOT changed. A Zoho login shortcut does not migrate email hosting; Zoho domain verification, MX, SPF and DKIM setup is a separate task if requested.

Other existing GitHub sites n2sny-site, shorts2go-site, and silvestro.us-site are unrelated and must remain unchanged.

## carcore.us GitHub Pages launch

1. Enable Pages on the new repository only, main branch, root directory. Verify successful build and preview.
2. Set the Pages custom domain to carcore.us BEFORE changing DNS; GitHub will create its CNAME file. Do not set this prematurely while the preview is needed.
3. In IONOS DNS for carcore.us only, replace the old root A with all four GitHub Pages A records:
   - @ → 185.199.108.153
   - @ → 185.199.109.153
   - @ → 185.199.110.153
   - @ → 185.199.111.153
4. Remove old conflicting root AAAA; either use no AAAA or all four GitHub IPv6 addresses: 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153.
5. Add www CNAME → adcontrol10.github.io (not a repository path), removing only conflicting www web records. GitHub can redirect www.carcore.us to the root.
6. Preserve all MX, TXT, DKIM, verification and unrelated records. Leave carcore.pro's root untouched until its authenticated host is ready.
7. Wait for DNS and certificate provisioning, then enable Enforce HTTPS. Verify root, www redirect, mobile layout and contact CTA.

Official GitHub instructions: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Zoho mail shortcut

Use IONOS subdomain forwarding to configure mail.carcore.pro → https://mail.zoho.com if supported with HTTPS. Prefer an HTTP 302/307 redirect for this service shortcut, not frame forwarding. A DNS CNAME alone does not implement an HTTP redirect to Zoho and may fail TLS or host routing. Preserve root domain, MX and TXT. Confirm HTTPS works at the alias before replacing direct Zoho links.

## Portal deployment prerequisites

GitHub Pages is static and cannot enforce server-side login. Keep the public site and protected portal separate. Required inputs: existing identity service or selected backend host, customer account/enrollment policy, approved installer source, download entitlement rules, renewal process/payment provider, and existing support mailbox. The desktop program's local login/license checking is not web authentication. No license signing/check secrets may be bundled into public web code.
