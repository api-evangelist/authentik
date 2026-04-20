# Authentik (authentik)
Authentik is an open source identity provider with a comprehensive REST API for managing users, groups, flows, providers, sources, policies, and outposts. It supports OAuth2, OIDC, SAML, LDAP, SCIM, and RADIUS protocols with official client SDKs in TypeScript, Python, Go, Rust, Kotlin, and Swift.

**URL:** [https://goauthentik.io](https://goauthentik.io)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Authentication, Authorization, Identity Provider, LDAP, OAuth, Open Source, OpenID Connect, SAML, SCIM, Self-Hosted

## Timestamps

- **Created:** 2026-03-25
- **Modified:** 2026-04-19

## APIs

### Authentik REST API
The authentik REST API v3 provides complete management of the authentik identity platform including users, groups, tokens, flows, providers, sources, policies, outposts, events, and configuration. Every authentik instance includes a built-in API browser at /api/v3/.

**Human URL:** [https://api.goauthentik.io/](https://api.goauthentik.io/)

#### Tags:

 - Authentication, Identity, REST, Users

#### Properties

- [Documentation](https://docs.goauthentik.io/developer-docs/api/)
- [OpenAPI](https://api.goauthentik.io/#/Schema/schema_retrieve)
- [APIReference](https://api.goauthentik.io/)
- [SDK](https://pypi.org/project/authentik-client/)
- [SDK](https://www.npmjs.com/package/@goauthentik/api)
- [GitHubRepository](https://github.com/goauthentik/authentik)

## Common Properties

- [Website](https://goauthentik.io)
- [Documentation](https://docs.goauthentik.io)
- [GitHubOrganization](https://github.com/goauthentik)
- [GitHubRepository](https://github.com/goauthentik/authentik)
- [ChangeLog](https://github.com/goauthentik/authentik/releases)
- [Support](https://github.com/goauthentik/authentik/discussions)
- [Community](https://discord.gg/jg33eMhnj6)
- [Pricing](https://goauthentik.io/pricing)

## Features

| Name | Description |
|------|-------------|
| Comprehensive REST API | Full REST API covering all authentik features with built-in Swagger UI at /api/v3/ on every instance. |
| Multi-Protocol Support | Native support for OAuth2, OIDC, SAML, LDAP, SCIM, RADIUS, and SSTP protocols for broad integration coverage. |
| Flow Engine | Customizable authentication and enrollment flows with visual flow designer for configuring multi-step authentication processes. |
| Multi-Language SDKs | Official API client SDKs in TypeScript, Python, Go, Rust, Kotlin, and Swift auto-generated from the OpenAPI schema. |
| Terraform Provider | Official Terraform provider for infrastructure-as-code management of authentik resources. |
| Helm Deployment | Official Helm chart for Kubernetes deployment with configurable replicas, persistence, and external database support. |
| RBAC | Role-based access control for granular permission management across authentik resources and administrative functions. |

## Use Cases

| Name | Description |
|------|-------------|
| Self-Hosted Identity Provider | Deploy a complete identity provider on-premises or in private cloud with full data sovereignty. |
| SSO Gateway | Provide single sign-on for all internal applications using OIDC, SAML, or LDAP protocol support. |
| B2C Identity | Build customer-facing registration and authentication flows with customizable enrollment and recovery processes. |
| Zero Trust Access | Implement zero trust application access with forward auth proxy integration and per-application policies. |

## Integrations

| Name | Description |
|------|-------------|
| Nginx/Traefik/Caddy | Forward auth integration with major reverse proxies for transparent application authentication. |
| Kubernetes | Native Kubernetes deployment via Helm chart with optional operator and RBAC integration. |
| LDAP Directory | LDAP outpost that exposes authentik users to LDAP-compatible applications without a directory server. |
| Grafana | Native OAuth2 integration with Grafana for unified authentication in monitoring stacks. |
| Nextcloud | OIDC or SAML integration with Nextcloud for unified login in self-hosted file storage. |

## Solutions

| Name | Description |
|------|-------------|
| Self-Hosted IAM | Complete identity and access management platform deployable on any infrastructure with no vendor lock-in. |
| Application Gateway | Secure and authenticate any application using forward auth with optional MFA and per-user access policies. |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
