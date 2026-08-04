# freee (freee)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

freee K.K. (freee株式会社) is a Japanese cloud business-management SaaS company. Its core products are **freee Accounting** (会計freee) — cloud accounting and bookkeeping — and **freee HR & Payroll** (人事労務freee) — HR, attendance, and payroll — plus invoicing (freee請求書) and sales management (freee販売). freee publishes well-documented public REST APIs for both accounting and HR.

## Access model (honest summary)

- **This is freee the Japanese accounting company (freee.co.jp) — not the English word "free."**
- **Auth:** OAuth 2.0 **authorization code** grant. You register an app in the freee Developers console for a `client_id` / `client_secret`, send the user through the consent flow, then exchange the code for an access token (and refresh token). The access token is sent on every request as `Authorization: Bearer <access_token>`. Authorization endpoint `https://accounts.secure.freee.co.jp/public_api/authorize`, token endpoint `https://accounts.secure.freee.co.jp/public_api/token`, scopes `read` and `write`.
- **Base hosts:** Accounting under `https://api.freee.co.jp/api/1`; HR & Payroll under `https://api.freee.co.jp/hr/api/v1`.
- **Scoping:** most accounting and HR calls are scoped to a freee company (事業所) via a `company_id` parameter.
- **Region:** Japan. The product UI and most documentation are in Japanese; English developer material also exists. Field names in this entry are given in English with the Japanese term in parentheses.
- **Protocol:** request/response REST over HTTPS only. freee does **not** expose a documented public WebSocket API; change detection is done by polling with date-range filters.
- **Included with subscription:** API access is included with a paid freee plan — there is no separate metered API fee.

freee publishes machine-readable OpenAPI schemas at [github.com/freee/freee-api-schema](https://github.com/freee/freee-api-schema) and maintains official SDKs (PHP, Java, and others) at [github.com/freee](https://github.com/freee). The bundled `openapi/freee-openapi.yml` here is a curated, high-fidelity **subset** grounded in those schemas — the real accounting schema defines 91 paths and the HR schema 68 paths.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/freee/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/freee/refs/heads/main/apis.yml)

## Tags

- Accounting
- Bookkeeping
- HR
- Payroll
- Invoicing
- Finance
- SaaS
- Japan

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### freee Accounting Deals API

Create, list, get, update, and delete accounting deals / transactions (取引) — income and expense records with account-item detail lines, tax codes, partners, and settlement status — scoped to a freee company.

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Deals
- Transactions

#### Properties

- [Documentation](https://developer.freee.co.jp/)
- [API Reference](https://developer.freee.co.jp/reference/accounting/reference)
- [OpenAPI](openapi/freee-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/freee.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/freee.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### freee Accounting Account Items API

Manage a company's account items / chart of accounts (勘定科目) and related tax codes (税区分) that classify each line of a deal or journal.

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Account Items
- Chart of Accounts

### freee Accounting Partners API

Create, list, get, update, and delete trading partners / counterparties (取引先) — the customers and suppliers referenced by deals, invoices, and payments.

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Partners
- Counterparties

### freee Accounting Invoices and Quotations API

Read issued invoices (請求書) and quotations / estimates (見積書) for a company, including invoice number, issue date, partner, totals, and lifecycle status.

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Invoicing
- Quotations

### freee Accounting Wallet Transactions API

Manage wallet transactions / statement lines (明細) and the walletables (口座) they belong to — bank accounts, credit cards, and wallets — for bank reconciliation and cash-flow tracking.

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Wallet Transactions
- Bank Accounts

### freee Accounting Journals and Reports API

Request asynchronous journal (仕訳帳) exports (CSV / PDF / yayoi), manage manual journals (振替伝票), and read trial-balance reports such as the profit-and-loss trial balance (試算表).

- **Human URL:** [https://developer.freee.co.jp/reference/accounting/reference](https://developer.freee.co.jp/reference/accounting/reference)
- **Base URL:** `https://api.freee.co.jp/api/1`

#### Tags

- Accounting
- Journals
- Reports

### freee HR Employees API

Create, list, get, update, and delete employees (従業員) in freee人事労務, plus the authenticated HR user context and the companies (事業所) they can access.

- **Human URL:** [https://developer.freee.co.jp/reference/hr/reference](https://developer.freee.co.jp/reference/hr/reference)
- **Base URL:** `https://api.freee.co.jp/hr/api/v1`

#### Tags

- HR
- Employees
- Japan

### freee HR Payroll API

Read employee salary and bonus payroll statements (給与明細・賞与明細) by company and pay month for downstream payroll, accounting, and reporting workflows.

- **Human URL:** [https://developer.freee.co.jp/reference/hr/reference](https://developer.freee.co.jp/reference/hr/reference)
- **Base URL:** `https://api.freee.co.jp/hr/api/v1`

#### Tags

- HR
- Payroll
- Salary

### freee HR Attendance API

Register time-clock punches (打刻) and read or edit daily attendance work records (勤怠) for employees — clock in / out, breaks, and worked hours.

- **Human URL:** [https://developer.freee.co.jp/reference/hr/reference](https://developer.freee.co.jp/reference/hr/reference)
- **Base URL:** `https://api.freee.co.jp/hr/api/v1`

#### Tags

- HR
- Attendance
- Time Tracking

## Common Properties

- [Domain Security](security/freee-domain-security.yml)
- [Authentication](authentication/freee-authentication.yml)
- [GitHub Organization](https://github.com/freee)
- [LinkedIn](https://www.linkedin.com/company/freeekk)
- [Website](https://www.freee.co.jp/)
- [Documentation](https://developer.freee.co.jp/)
- [Plans](plans/freee-plans-pricing.yml)
- [Rate Limits](rate-limits/freee-rate-limits.yml)
- [Fin Ops](finops/freee-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
