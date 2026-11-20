# Repository-wide Copilot instructions — Liferay DXP project

These instructions apply to every Copilot interaction in this repository, including all custom agents in `.github/agents/`.

## Platform baseline (source of truth)

| Item | Value |
|---|---|
| Current product | **Liferay DXP 2025.Q1 (LTS)** — Quarterly Release, long-term support line |
| Workspace product key | `liferay.workspace.product=dxp-2025.q1.<N>-lts` in `gradle.properties` (confirm the exact patch level in the repo) |
| Java runtime | JDK 21 (certified; bundled Zulu 21 in the official Docker image). JDK 17 also supported on 2025.Q1 |
| Servlet / EE namespace | **Java EE 8 / `javax.*`** on 2025.Q1. Liferay's roadmap moves to **Jakarta EE (`jakarta.*`) from 2025.Q3 onward** — treat this as the largest upgrade risk |
| Build | Liferay Workspace (Gradle), Blade CLI, Node/Yarn for frontend & client extensions |
| Search | Elasticsearch (native) or OpenSearch (GA connector from 2025.Q1, with feature limitations) |
| Preferred extension model | Client Extensions first, then OSGi modules, never core/EXT changes unless unavoidable |

If the repository says something different (e.g. a newer `liferay.workspace.product`), **the repository wins** — re-read it before answering.

## Non-negotiable rules for all agents

1. **No fabrication.** Do not invent Liferay APIs, OSGi services, configuration PIDs, portal properties, REST endpoints or feature flags. If unsure, say so and show how to verify (API Explorer at `/o/api`, Gogo shell, source at the matching release tag, learn.liferay.com).
2. **Version-specific answers.** Always state which DXP version an answer applies to. Behaviour differs between 7.4 updates, 2024.Qx, 2025.Q1 and the Jakarta-based releases.
3. **Least invasive extension point first:** configuration → client extension → OSGi module (DS component, model listener, service wrapper) → module fragment / JSP override (last resort) → never modify Liferay core or ship EXT plugins without explicit approval.
4. **Production quality:** error handling, input validation, logging via `com.liferay.portal.kernel.log.Log` / SLF4J, no secrets in code or `portal-ext.properties` committed to Git.
5. **Security by default:** respect permission checkers, Service Access Policies, OAuth2 scopes, CSRF (`p_auth`) and CORS configuration; never disable them to "make it work".
6. **Small, reviewable changes.** Prefer targeted fixes over rewrites. Explain significant design decisions briefly.
7. **Hand off** to the specialised agent when a task leaves your scope (see the agent roster in `AGENTS-README.md`).

## Repository conventions (adjust to your repo)

- `modules/` — OSGi modules (Java, Service Builder, REST Builder)
- `client-extensions/` — Client Extension projects (`client-extension.yaml`)
- `themes/` — legacy WAR themes (migrate to Theme CSS client extensions where feasible)
- `configs/{common,local,dev,uat,prod}/` — environment configs (`portal-ext.properties`, `osgi/configs/*.config`)
- `infra/` — IaC (Terraform / CDK / Helm values) for AWS
- Ticket IDs: Liferay's own issues are `LPD-`, `LPS-`, `LPP-`; reference them when citing behaviour.
