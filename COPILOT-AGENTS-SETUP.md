# Liferay DXP 2025.Q1 Copilot Agents — Installation, Setup & Test Guide

Extract the agent files into your **repo root**, the folder that holds `.git`, which for a Liferay Workspace is also the folder with `gradle.properties` and `settings.gradle`. It's the same folder you open in VS Code.

---

## 1. File layout after extracting

```
D:\develop\<your-liferay-repo>\        ← repo root = Liferay Workspace root = folder opened in VS Code
├── .git\
├── .github\
│   ├── copilot-instructions.md        ← shared rules for all agents
│   ├── agents\
│   │   ├── liferay-upgrade-agent.agent.md
│   │   ├── aws-configuration-specialist.agent.md
│   │   ├── aws-architecture.agent.md
│   │   ├── liferay-api-integration-agent.agent.md
│   │   ├── liferay-backend-osgi-agent.agent.md
│   │   ├── liferay-client-extension-agent.agent.md
│   │   ├── liferay-compatibility-security-watcher.agent.md
│   │   ├── liferay-delivery-coordinator.agent.md
│   │   ├── liferay-dxp-source-investigator.agent.md
│   │   ├── liferay-theme-frontend-agent.agent.md
│   │   └── liferay-platform-engineer.agent.md
│   └── workflows\                     ← your existing CI files, untouched
├── AGENTS-README.md                   ← keep OUT of .github\agents\
├── COPILOT-AGENTS-SETUP.md            ← this guide (optional)
├── gradle.properties
├── settings.gradle
├── modules\
├── client-extensions\
├── themes\
└── configs\
```

### Common mistakes

- **An extra folder level.** Windows "Extract All" puts the files in a new `liferay-copilot-agents\` folder by default. That gives you `...\liferay-copilot-agents\.github\`, and Copilot won't find it.
- **Overwriting an existing file.** If your repo already has `.github\copilot-instructions.md`, merge the two files by hand instead of replacing yours.
- **Wrong folder opened in VS Code.** Open the repo root, not `D:\develop` and not a subfolder like `modules\`.
- **README inside the agents folder.** VS Code loads every `.md` file in `.github\agents\` as an agent, so keep `AGENTS-README.md` and this guide out of it.

---

## 2. Extract (PowerShell)

```powershell
cd D:\develop\<your-liferay-repo>

# Check first: is there already a copilot-instructions.md?
Test-Path .github\copilot-instructions.md

# Extract to a temp folder, then copy in (no overwrite surprises)
Expand-Archive -Path "$HOME\Downloads\liferay-copilot-agents.zip" -DestinationPath "$env:TEMP\lr-agents" -Force
New-Item -ItemType Directory -Force .github\agents | Out-Null
Copy-Item "$env:TEMP\lr-agents\.github\agents\*.agent.md" .github\agents\
Copy-Item "$env:TEMP\lr-agents\AGENTS-README.md" .
# Only if Test-Path returned False; otherwise merge by hand:
Copy-Item "$env:TEMP\lr-agents\.github\copilot-instructions.md" .github\

# Verify
Get-ChildItem .github -Recurse -File | Select-Object FullName
```

You should see 11 `*.agent.md` files plus `copilot-instructions.md`.

---

## 3. Set up Copilot

1. **Get up to date.** Update VS Code to the latest stable version, along with the GitHub Copilot and GitHub Copilot Chat extensions, and sign in with the GitHub account that has your Copilot license.
2. **Check org policy (company accounts).** If your org manages Copilot, an admin may have turned off preview features or custom agents. If no agents show up in step 4, check this first.
3. **Open the right folder.** Use File → Open Folder → the repo root.
4. **Confirm the agents loaded.** Run **Chat: Open Customizations** from the Command Palette and select the **Agents** tab. Confirm all 11 agents are listed without file errors, and hover over one to check that its source location is `.github\agents\`.
5. **Select an agent.** Start a new chat in the same repo folder and pick the agent from the **Agent** dropdown.
6. **Pick a model** in the chat model picker. The agent files don't set one.

---

## 4. Test that the agents work

Run each test in a **new chat**. Check what the agent actually does with your files, not just its wording.

| # | Agent | Prompt | Pass if… |
|---|---|---|---|
| 1 | Plain Agent (no custom agent) | "What Liferay version and Java namespace is this project on?" | It answers DXP 2025.Q1, JDK 21, `javax`, which shows `copilot-instructions.md` was applied. Expand **References** in the response and look for that file. |
| 2 | liferay-upgrade-agent | "What is our exact current product key? Give me a high-level plan to reach the next LTS." | It **reads `gradle.properties`** and quotes the real value, then flags the Jakarta move from 2025.Q3 onward. |
| 3 | liferay-dxp-source-investigator | "Fix the bug in modules/xyz by editing the file." | It **refuses to edit** and offers to hand off. This shows the read-only setup works. |
| 4 | liferay-compatibility-security-watcher | "Review our Dockerfile and configs for compatibility and security issues." | You get a findings table with sources and no file edits. |
| 5 | liferay-backend-osgi-agent | "What's the portal property to enable feature X?" (use a made-up name) | It says it can't verify the property and tells you how to check, instead of inventing one. |
| 6 | liferay-client-extension-agent | "Should a widget that lists Object entries be a module or a CX? Scaffold it." | It recommends a custom element CX and shows a full `client-extension.yaml`. |
| 7 | liferay-delivery-coordinator | "Plan adding an S3 doc store and a React dashboard." | You get a work-item table with owner agents, followed by handoff buttons. |
| 8 | Handoff | Click a handoff button from test 7 | The chat switches to the target agent with the prompt filled in but not sent. |

### About handoffs (test 8)

Handoff buttons work only in VS Code's **Local** harness, which VS Code's docs say is deprecated and will be removed in February 2027. If you use the newer **Copilot** harness, the buttons won't appear, and that's expected. You can switch agents manually from the dropdown. The rest of each agent file still works: in the Copilot harness, an agent's instructions are added to your custom instructions and win if the two conflict.

---

## 5. Troubleshooting

| Symptom | Fix |
|---|---|
| Agent not listed | Check that the path is exactly `<repo>\.github\agents\`, the file names end in `.agent.md`, and you opened the root folder. An uncommitted agent file may also be missing from a new Git worktree. |
| Listed but not in the dropdown | Look for frontmatter errors and check whether `user-invocable` is set to `false`. Common causes are tabs in the YAML or a file saved with a BOM. Save as UTF-8 and run **Developer: Reload Window**. |
| An agent appears called "AGENTS-README" | The README ended up inside `.github\agents\`. Move it out. |
| Agent ignores its role | Start a new chat, since agent selection doesn't carry over cleanly mid-chat. Compare the request, the instructions and the tool activity in the chat to see where it went off course. |
| Agent can't read files or run commands | You're probably in Ask mode, or tool approval is pending. Use Agent mode and approve the tool prompts. |
| Unexpected or missing tools | Make sure the tool names in the agent file are ones your harness supports. Unrecognised names are ignored. |

---

## 6. Share with the team

```powershell
git checkout -b chore/copilot-agents
git add .github/agents .github/copilot-instructions.md AGENTS-README.md COPILOT-AGENTS-SETUP.md
git commit -m "Add Liferay DXP 2025.Q1 Copilot custom agents"
git push -u origin chore/copilot-agents
```

- After the PR merges, everyone who opens the repo gets the agents automatically.
- To use them with Copilot's cloud agent on GitHub.com, the files need to be on the **default branch**. On GitHub.com the handoff buttons are ignored.

---

## 7. Before testing

Edit the **"Repository conventions"** section of `.github/copilot-instructions.md` so its folder names match your repo (`modules/`, `client-extensions/`, `configs/`, `infra/`, …). Test 2 depends on that being accurate.

---

### Reference

- VS Code: Custom agents — https://code.visualstudio.com/docs/copilot/customization/custom-agents
- GitHub: Custom agents configuration — https://docs.github.com/en/copilot/reference/custom-agents-configuration
