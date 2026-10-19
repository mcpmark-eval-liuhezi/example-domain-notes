# Reserved Example Domains, Public Resolvers & TLD Registries — Onboarding Reference

Single reference page for the two questions every new hire asks in week one:

1. Who actually controls **example.com / example.org / example.net**, and where does their registration data come from?
2. Whose networks do the public resolvers **1.1.1.1** and **8.8.8.8** live on?

All data below was pulled live from WHOIS registry records on **2026-10-19 (UTC)**. Registrars, statuses and nameservers are reproduced exactly as the records show them today.

## Quick answers

- The three reserved example domains are held under **IANA's** registrar of record (Registrar IANA ID **376** — listed as `RESERVED-Internet Assigned Numbers Authority` for .com/.net and `ICANN` for .org) and are locked against deletion, transfer and update. They are reserved for use in documentation and testing (RFC 2606) and are not available for ordinary registration.
- Their authoritative DNS is outsourced to **Cloudflare**, a commercial DNS operator — the same company that runs the 1.1.1.1 public resolver.
- **1.1.1.1** → Cloudflare, **AS13335** (`CLOUDFLARENET`), network **1.1.1.0/24** (`APNIC-LABS`).
- **8.8.8.8** → Google LLC, **AS15169** (`GOOGLE`), network **8.8.8.0/24** (`GOGL`).

---

## The reserved domains

### example.com

Registration record served by `whois.verisign-grs.com` (the Verisign .com registry).

| Field | Value as recorded |
|---|---|
| Registrar | RESERVED-Internet Assigned Numbers Authority |
| Registrar IANA ID | 376 |
| Registrar WHOIS server | whois.iana.org |
| Registrar URL | http://res-dom.iana.org |
| Domain statuses | clientDeleteProhibited · clientTransferProhibited · clientUpdateProhibited |
| Name servers | ELLIOTT.NS.CLOUDFLARE.COM · HERA.NS.CLOUDFLARE.COM |
| DNSSEC | signedDelegation — DS 2371 13 2 C988EC423E3880EB8DD8A46FE06CA230EE23F35B578D64E78B29C3E1C83D245A |
| Created / Updated / Expires | 1995-08-14 / 2026-08-14 / 2027-08-13 |
| Registry Domain ID | 2336799_DOMAIN_COM-VRSN |

> **Nameserver operator call-out:** the authoritative nameservers for example.com end in `NS.CLOUDFLARE.COM` — they belong to **Cloudflare, Inc.**, a commercial DNS operator, not to the .com registry (Verisign) and not to IANA. IANA holds the registration; the domain's DNS is served from Cloudflare's nameserver platform.

### example.org

Registration record served by `whois.pir.org` (the Public Interest Registry .org registry).

| Field | Value as recorded |
|---|---|
| Registrar | ICANN |
| Registrar IANA ID | 376 |
| Domain statuses | serverDeleteProhibited · serverTransferProhibited · serverUpdateProhibited |
| Name servers | katelyn.ns.cloudflare.com · mitch.ns.cloudflare.com |
| DNSSEC | signedDelegation |
| Created / Updated / Expires | 1995-08-31 / 2026-10-14 / 2027-08-30 |

The record also notes: *"This domain is protected by the Registry Lock service."*

> Note the lock-level difference: .org carries **server\*** locks (imposed at the registry level via Registry Lock), while .com and .net carry **client\*** locks (imposed at the registrar level). example.org also runs on Cloudflare nameservers.

### example.net

Registration record served by `whois.verisign-grs.com` (the Verisign .net registry).

| Field | Value as recorded |
|---|---|
| Registrar | RESERVED-Internet Assigned Numbers Authority |
| Registrar IANA ID | 376 |
| Registrar WHOIS server | whois.iana.org |
| Registrar URL | http://res-dom.iana.org |
| Domain statuses | clientDeleteProhibited · clientTransferProhibited · clientUpdateProhibited |
| Name servers | BETTY.NS.CLOUDFLARE.COM · HUGH.NS.CLOUDFLARE.COM |
| DNSSEC | signedDelegation — DS 2371 13 2 6EBDD24B59EBB0A642D07F2D8EF3CB65AAF1124FA5507FB2F2101D53B45FE666 |
| Created / Updated / Expires | 1995-08-31 / 2026-08-31 / 2027-08-30 |
| Registry Domain ID | 2328120_DOMAIN_NET-VRSN |

> example.net's nameservers also belong to Cloudflare — all three reserved domains delegate DNS to the same commercial operator.

---

## The public resolvers

### 1.1.1.1

- **Operator:** Cloudflare, Inc. (AS record registered to Cloudflare, Inc., 101 Townsend Street, San Francisco, CA — ARIN)
- **AS number:** AS13335 — ASName `CLOUDFLARENET`
- **Network:** 1.1.1.0/24 — netname `APNIC-LABS`, held by APNIC Research and Development (ORG-ARAD1-AP), status ASSIGNED PORTABLE
- **Record sources:** IP record from APNIC whois; AS record from ARIN whois

The APNIC inetnum record describes the block as the *"APNIC and Cloudflare DNS Resolver project"*, a *"Research prefix for APNIC Labs"*, and states it is *"Routed globally by AS13335/Cloudflare"* — i.e. the address space is an APNIC research allocation, announced by Cloudflare's AS13335, and the resolver service is run by Cloudflare.

### 8.8.8.8

- **Operator:** Google LLC (AS record registered to Google LLC, 1600 Amphitheatre Parkway, Mountain View, CA — ARIN)
- **AS number:** AS15169 — ASName `GOOGLE`
- **Network:** 8.8.8.0/24 — NetName `GOGL`, a Direct Allocation to Google LLC (NetHandle NET-8-8-8-0-2, parent NET8)
- **Record sources:** IP record from ARIN whois; AS record from ARIN whois

### The Cloudflare connection (explicit)

The company behind example.com's nameservers — **Cloudflare, Inc.** (`ELLIOTT.NS.CLOUDFLARE.COM` / `HERA.NS.CLOUDFLARE.COM`) — **is the same company that operates the 1.1.1.1 public resolver**, which is served out of Cloudflare's **AS13335 (CLOUDFLARENET)**. In fact, all three reserved example domains use Cloudflare nameservers.

So on our standard laptop setup: the authoritative DNS for the example domains you see all over our docs, and one of the two recursive resolvers your machine queries, are run by the same firm — **Cloudflare**. The other resolver, 8.8.8.8, is run by **Google** on AS15169.

---

## TLD registries

Registry records for the three top-level domains, drawn from the **IANA root database** (`source: IANA`, IANA WHOIS server) — each record also identifies the registry's own whois server where domain-level data is served:

| TLD | Registry operator | Record source | Status |
|---|---|---|---|
| **.com** | VeriSign Global Registry Services — 12061 Bluemont Way, Reston VA 20190, USA | IANA root database; registry whois `whois.verisign-grs.com` | ACTIVE |
| **.org** | Public Interest Registry (PIR) — 11911 Freedom Drive, 10th Floor, Suite 1000, Reston VA 20190, USA | IANA root database; registry whois `whois.publicinterestregistry.org` | ACTIVE |
| **.net** | VeriSign Global Registry Services — 12061 Bluemont Way, Reston VA 20190, USA | IANA root database; registry whois `whois.verisign-grs.com` | ACTIVE |

- **Verisign** operates both the .com and .net registries — which is why example.com and example.net records both come from `whois.verisign-grs.com`.
- The .org registry is operated by **Public Interest Registry (PIR)**; its IANA record lists **Identity Digital Limited** as the technical contact (DNS Infrastructure Group).
- All three TLD records show `created: 1985-01-01` (delegation date) and status ACTIVE.

---

## Where to re-check this data

- **Domain records:** the TLD registries' whois servers — `whois.verisign-grs.com` (.com/.net) and `whois.pir.org` (.org).
- **Resolver IP records:** APNIC whois (1.1.1.1) and ARIN whois (8.8.8.8).
- **AS records:** ARIN whois (AS13335, AS15169).
- **TLD registry records:** the IANA root database (IANA WHOIS server).

*Reference generated from live registry lookups on 2026-10-19 (UTC). Records change — re-pull before quoting in a ticket.*
