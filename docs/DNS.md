# DNS Configuration

Both domains are registered and DNS-hosted at **GoDaddy** (account: Charles
Hammon, customer #8105293). Changes below were made on **2026-07-10** with the
owner's approval, via the GoDaddy DNS Management UI.

## What was changed (web records only)

### excelrealty.us

| Record | Before | After |
| --- | --- | --- |
| `A @` | "Parked" (GoDaddy parking) | `185.199.108.153` |
| `A @` | — (added) | `185.199.109.153` |
| `A @` | — (added) | `185.199.110.153` |
| `A @` | — (added) | `185.199.111.153` |
| `CNAME www` | `excelrealty.us.` | `charles403.github.io.` |

### shortcreekrealty.com

| Record | Before | After |
| --- | --- | --- |
| `A @` | "WebsiteBuilder Site" (GoDaddy Website Builder) | `185.199.108.153` |
| `A @` | — (added) | `185.199.109.153` |
| `A @` | — (added) | `185.199.110.153` |
| `A @` | — (added) | `185.199.111.153` |
| `CNAME www` | `shortcreekrealty.com.` | `charles403.github.io.` |

`185.199.108–111.153` are GitHub Pages' anycast IPs. The `www` hosts are the
primary domains on the two GitHub Pages sites; GitHub redirects each apex to
its `www`. The old GoDaddy Website Builder site for shortcreekrealty.com
("Launching Soon" page) is disconnected from the domain but still exists in
the GoDaddy account.

## What was NOT changed — preserve these

These records keep **Google Workspace email and domain verification** working
on both domains. Never delete or modify them when editing DNS:

| Record | Value (both domains) | Purpose |
| --- | --- | --- |
| `MX @` | `smtp.google.com.` (priority 1) | Google Workspace mail delivery |
| `TXT @` | `v=spf1 include:_spf.google.com ~all` | SPF (anti-spoofing) |
| `TXT google._domainkey` | `v=DKIM1; k=rsa; p=…` | DKIM email signing |
| `TXT _dmarc` | `v=DMARC1; p=quarantine; …` | DMARC policy |
| `TXT @` | `google-site-verification=…` | Google domain verification |
| `NS @` | `ns43/ns44` (.us) / `ns69/ns70` (.com) `.domaincontrol.com` | GoDaddy nameservers |
| `CNAME _domainconnect` | `_domainconnect.gd.domaincontrol.com.` | GoDaddy Domain Connect |
| `SOA @` | (GoDaddy default) | Zone authority |

## Rollback

To restore the previous websites: on shortcreekrealty.com, delete the four
`A @` records and re-connect the domain to the GoDaddy Website Builder site
(GoDaddy recreates its records), and set `CNAME www` back to
`shortcreekrealty.com.` On excelrealty.us, delete the four `A @` records,
restore GoDaddy parking ("Parked"), and set `CNAME www` back to
`excelrealty.us.` Email records need no changes in either direction.

## HTTPS

GitHub Pages provisions Let's Encrypt certificates for all four hostnames
automatically after DNS propagates, and "Enforce HTTPS" is enabled on both
Pages sites, so HTTP requests redirect to HTTPS.
