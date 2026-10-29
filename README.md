# Authentik

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Authentik is an open source identity provider from Authentik Security Inc., a public benefit company, exposing a 1,193-operation REST API at /api/v3 on every self-hosted instance. The published OpenAPI covers users, groups, applications, tokens, RBAC, flows, stages, policies, property mappings, outposts, events, blueprints, endpoint devices, privileged access management and agent accounts. authentik speaks OAuth2/OIDC (OpenID Certified), SAML 2.0, SCIM 2.0, LDAP, RADIUS, Kerberos, Proxy and the OpenID Shared Signals Framework, and ships first-party API clients for TypeScript, Python, Go and Rust plus a Terraform provider and the `ak` CLI.

**Areas:** Authentication · Authorization · Identity Provider · LDAP · Open Source · OpenID Connect · SAML · SCIM · Self-Hosted · Identity Federation

## Authentik on APIs.io

Everything profiled for Authentik is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/authentik/](https://apis.io/providers/authentik/)** — or go straight to one of the APIs or properties below.

### APIs (27)

- [Authentik Core API](https://apis.io/apis/authentik/authentik-core-api/) — Users, groups, applications, tokens, brands, application entitlements and authenticated sessions — the identity records and the objects users see.
- [Authentik Crypto API](https://apis.io/apis/authentik/authentik-crypto-api/) — Certificate-key pairs used to sign SAML assertions and OIDC ID tokens, and to validate webhook receivers.
- [Authentik Events API](https://apis.io/apis/authentik/authentik-events-api/) — Audit events, notification rules and notification transports — including the webhook and Slack transports that push authentik events to external receivers.
- [Authentik Flows API](https://apis.io/apis/authentik/authentik-flows-api/) — Flow instances, flow bindings and the flow executor that drives authentication, enrollment, recovery and unenrollment.
- [Authentik Policies API](https://apis.io/apis/authentik/authentik-policies-api/) — Policies and policy bindings — expression, event matcher, GeoIP, password, password expiry, reputation and unique-password types.
- [Authentik Providers API](https://apis.io/apis/authentik/authentik-providers-api/) — Protocol providers: OAuth2/OIDC, SAML, SCIM, LDAP, RADIUS, Proxy, RAC, WS-Fed, Google Workspace, Microsoft Entra and the Shared Signals Framework backchannel.
- [Authentik RBAC API](https://apis.io/apis/authentik/authentik-rbac-api/) — Role-based access control — roles, global and object-level permissions, and initial permission sets.
- [Authentik Schema API](https://apis.io/apis/authentik/authentik-schema-api/) — The self-describing OpenAPI schema endpoint every authentik instance serves.
- [Authentik Sources API](https://apis.io/apis/authentik/authentik-sources-api/) — External identity sources — LDAP, OAuth, SAML, SCIM, Kerberos, Plex and Telegram — plus their user and group connections.
- [Authentik Stages API](https://apis.io/apis/authentik/authentik-stages-api/) — Flow stages: identification, password, consent, prompt, email, captcha, mTLS, redirect, user write/login/logout/delete, account lockdown and every…
- [Authentik Admin API](https://apis.io/apis/authentik/authentik-admin-api/) — Instance administration — installed apps, models, version, system information, workers and the file storage backend.
- [Authentik Agents API](https://apis.io/apis/authentik/authentik-agents-api/) — Agent accounts — service accounts that act on behalf of a parent user when calling the authentik API, with expiring tokens and audited delegation.
- [Authentik Authenticators API](https://apis.io/apis/authentik/authentik-authenticators-api/) — Authenticator device management for TOTP, static, WebAuthn, SMS, email, Duo and endpoint devices, from both the admin and end-user perspectives.
- [Authentik Endpoints API](https://apis.io/apis/authentik/authentik-endpoints-api/) — Endpoint device management — the authentik Agent connectors, device enrollment tokens, device bindings, device access groups, Fleet and Google Chrome…
- [Authentik Enterprise API](https://apis.io/apis/authentik/authentik-enterprise-api/) — Enterprise licensing — license installation, summary and forecast for a licensed authentik deployment.
- [Authentik Lifecycle API](https://apis.io/apis/authentik/authentik-lifecycle-api/) — Identity lifecycle operations, including scheduled user offboarding with session and token revocation and a cancellable pending state.
- [Authentik Managed API](https://apis.io/apis/authentik/authentik-managed-api/) — Blueprints — the YAML templates that declare authentik configuration as code, and the blueprint instances that apply them.
- [Authentik Outposts API](https://apis.io/apis/authentik/authentik-outposts-api/) — Outpost instances and service connections (Docker, Kubernetes) — the deployable components that run the proxy, LDAP and RADIUS providers.
- [Authentik Property Mappings API](https://apis.io/apis/authentik/authentik-propertymappings-api/) — Property mappings — the expressions that shape claims, attributes and payloads for every provider and source type, plus notification webhook bodies.
- [Authentik RAC API](https://apis.io/apis/authentik/authentik-rac-api/) — Remote Access Control — browser-based RDP, SSH and VNC endpoints and their single-use connection tokens.
- [Authentik Reports API](https://apis.io/apis/authentik/authentik-reports-api/) — Reporting surface for exportable user and event data.
- [Authentik Requests API](https://apis.io/apis/authentik/authentik-requests-api/) — Privileged access management — access request rules, rule bindings, grant requests, reviewer workflows and grant revocation.
- [Authentik Root API](https://apis.io/apis/authentik/authentik-root-api/) — Root configuration endpoint describing the running instance to its own frontend.
- [Authentik SSF API](https://apis.io/apis/authentik/authentik-ssf-api/) — OpenID Shared Signals Framework streams — the SSF stream surface a receiving application manages on authentik as transmitter of Security Event Tokens.
- [Authentik Tasks API](https://apis.io/apis/authentik/authentik-tasks-api/) — Background task schedules and runs executed by the authentik worker.
- [Authentik Tenants API](https://apis.io/apis/authentik/authentik-tenants-api/) — Multi-tenant administration for deployments running more than one authentik tenant.
- [Authentik Oauth2 API](https://apis.io/apis/authentik/authentik-oauth2-api/) — The oauth2 API from Authentik — 9 operation(s) for oauth2.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Authentik Events Webhooks](https://apis.io/asyncapis/authentik/authentik-events-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [authentik-mcp.yml](https://apis.io/servers/authentik/authentik-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Authentik Agentic Access](https://apis.io/agentic-access/authentik/authentik-agentic-access/)

#### Collections (11)

Postman and Open Collection request collections.

- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-core-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-crypto-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-events-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-flows-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-policies-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-providers-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-rbac-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-schema-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-sources-api/)
- [Moved to /providers/authentik/](https://apis.io/collections/authentik/open-authentik-stages-api/)

#### Overlays (54)

OpenAPI overlays, including conversational phrasing for each operation.

- [Authentik Admin Api Overlay](https://apis.io/overlays/authentik/authentik-admin-api-overlay/)
- [Authentik Admin Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-admin-api-phrasing-overlay/)
- [Authentik Agents Api Overlay](https://apis.io/overlays/authentik/authentik-agents-api-overlay/)
- [Authentik Agents Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-agents-api-phrasing-overlay/)
- [Authentik Authenticators Api Overlay](https://apis.io/overlays/authentik/authentik-authenticators-api-overlay/)
- [Authentik Authenticators Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-authenticators-api-phrasing-overlay/)
- [Authentik Core Api Overlay](https://apis.io/overlays/authentik/authentik-core-api-overlay/)
- [Authentik Core Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-core-api-phrasing-overlay/)
- [Authentik Crypto Api Overlay](https://apis.io/overlays/authentik/authentik-crypto-api-overlay/)
- [Authentik Crypto Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-crypto-api-phrasing-overlay/)
- [Authentik Endpoints Api Overlay](https://apis.io/overlays/authentik/authentik-endpoints-api-overlay/)
- [Authentik Endpoints Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-endpoints-api-phrasing-overlay/)
- [Authentik Enterprise Api Overlay](https://apis.io/overlays/authentik/authentik-enterprise-api-overlay/)
- [Authentik Enterprise Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-enterprise-api-phrasing-overlay/)
- [Authentik Events Api Overlay](https://apis.io/overlays/authentik/authentik-events-api-overlay/)
- [Authentik Events Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-events-api-phrasing-overlay/)
- [Authentik Flows Api Overlay](https://apis.io/overlays/authentik/authentik-flows-api-overlay/)
- [Authentik Flows Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-flows-api-phrasing-overlay/)
- [Authentik Lifecycle Api Overlay](https://apis.io/overlays/authentik/authentik-lifecycle-api-overlay/)
- [Authentik Lifecycle Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-lifecycle-api-phrasing-overlay/)
- [Authentik Managed Api Overlay](https://apis.io/overlays/authentik/authentik-managed-api-overlay/)
- [Authentik Managed Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-managed-api-phrasing-overlay/)
- [Authentik Oauth2 Api Overlay](https://apis.io/overlays/authentik/authentik-oauth2-api-overlay/)
- [Authentik Oauth2 Api Phrasing Overlay](https://apis.io/overlays/authentik/authentik-oauth2-api-phrasing-overlay/)
- [Authentik Outposts Api Overlay](https://apis.io/overlays/authentik/authentik-outposts-api-overlay/)
- …and 29 more published on APIs.io

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Authentik Authentication](https://apis.io/security/authentik/authentik-authentication/)
- [Authentik Domain Security](https://apis.io/security/authentik/authentik-domain-security/)
- [Authentik Vulnerability Disclosure](https://apis.io/security/authentik/authentik-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Authentik Plans Pricing](https://apis.io/plans/authentik/authentik-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Authentik Rate Limits](https://apis.io/rate-limits/authentik/authentik-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Authentik Finops](https://apis.io/finops/authentik/authentik-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://goauthentik.io)
- [Documentation](https://docs.goauthentik.io)
- [Getting started](https://docs.goauthentik.io/install-config/)
- [API reference](https://api.goauthentik.io/)
- [Pricing](https://goauthentik.io/pricing)
- [Sign up](https://customers.goauthentik.io)
- [Support](https://github.com/goauthentik/authentik/discussions)
- [Changelog](https://github.com/goauthentik/authentik/releases)
- [Blog](https://goauthentik.io/blog/rss.xml)
- [Terms of service](https://goauthentik.io/legal/terms/)
- [Privacy policy](https://goauthentik.io/legal/privacy-policy/)
- [GitHub](https://github.com/goauthentik)
- [Status](https://status.goauthentik.io)

## API Evangelist rating

**Kin Score 70.1** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 56.8 |
| Contract governance | 18.2 |
| Operational transparency | 60.5 |
| Developer ergonomics | 82.7 |
| Access clarity | 84.2 |

**Agent readiness 30.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/authentik/](https://apis.io/providers/authentik/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Authentik: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/authentik/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
