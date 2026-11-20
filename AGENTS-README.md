# Liferay DXP 2025.Q1 — GitHub Copilot custom agents

## Install
Copy the `.github/` folder into the root of your Liferay Workspace repo:
```
.github/
├── copilot-instructions.md                     # shared baseline for every agent
└── agents/
    ├── liferay-upgrade-agent.agent.md
    ├── aws-configuration-specialist.agent.md
    ├── aws-architecture.agent.md
    ├── liferay-api-integration-agent.agent.md
    ├── liferay-backend-osgi-agent.agent.md
    ├── liferay-client-extension-agent.agent.md
    ├── liferay-compatibility-security-watcher.agent.md
    ├── liferay-delivery-coordinator.agent.md
    ├── liferay-dxp-source-investigator.agent.md
    ├── liferay-theme-frontend-agent.agent.md
    └── liferay-platform-engineer.agent.md
```
Keep this README **out of** `.github/agents/` — VS Code loads every `.md` file there as an agent.

## Roster
| Agent | Role | Edits code? |
|---|---|---|
| liferay-delivery-coordinator | Plans, routes, tracks (entry point for multi-area work) | Planning docs only |
| liferay-upgrade-agent | 2025.Q1 → later quarterly/LTS, javax→jakarta, DB upgrade | Yes |
| liferay-backend-osgi-agent | OSGi / Service Builder / REST Builder | Yes |
| liferay-client-extension-agent | All client extension types | Yes |
| liferay-theme-frontend-agent | Style Books, Theme CSS CX, fragments, React/TS | Yes |
| liferay-api-integration-agent | Headless/GraphQL/Objects, OAuth2, integrations | Yes |
| liferay-dxp-source-investigator | Core source analysis, extension-point discovery | No (read-only) |
| liferay-compatibility-security-watcher | Compatibility matrix, CVEs, advisories, config risks | No (read-only) |
| liferay-platform-engineer | Workspace, Docker, CI/CD, env config, ops | Yes |
| aws-architecture | AWS design, ADRs, failure modes | ADRs only |
| aws-configuration-specialist | AWS IaC/config | Yes (proposes, doesn't apply) |

## Compatibility notes
- **Tools** use GitHub's portable aliases (`read`, `search`, `edit`, `execute`, `web`, `todo`, `agent`). Unrecognised tool names are ignored. To expose MCP servers (e.g. GitHub, AWS), add them to `tools:` as `server-name/*`.
- **`handoffs`** work in VS Code's local agent harness only; Copilot cloud agent on GitHub.com ignores them.
- No `model:` is set — pick the model in the chat UI, or add `model:` per agent.
- Update the platform table in `copilot-instructions.md` whenever `liferay.workspace.product` changes.
