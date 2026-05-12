# bigbang — Claude Code Context

## What this repo is

Big Bang is a declarative, continuous delivery tool for deploying DoD hardened and approved packages into a Kubernetes cluster.

---

## ADO project details

- **ADO org:** https://dev.azure.com/hybridcloudsolutions
- **ADO project:** Platform Engineering
- **Area path:** Platform Engineering\Onboarding
- **Work item format:** `AB#<id>` in commit messages and PR descriptions

---

## Standards

This repo follows all HCS platform standards defined in the Platform Engineering repo:

| Standard | Reference |
|---|---|
| Governance | [docs/standards/governance.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/governance.md) |
| Scripting (PowerShell 7) | [docs/standards/scripting.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/scripting.md) |
| Automation | [docs/standards/automation.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/automation.md) |
| Variables and naming | [docs/standards/variables.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/variables.md) |
| Documentation | [docs/standards/documentation.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/documentation.md) |
| Claude Code | [docs/standards/claude-code.md](https://dev.azure.com/hybridcloudsolutions/Platform%20Engineering/_git/Platform%20Engineering?path=/docs/standards/claude-code.md) |

Key rules:
- All scripts: PowerShell 7+ only. `#Requires -Version 7.0`, `Set-StrictMode -Version Latest`, ` $ErrorActionPreference = 'Stop'`.
- All docs: Markdown only. No Word documents in any repo.
- Commit format: `type(scope): short description` — types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`
- No secrets, tokens, or credentials committed to any file.

---

## Key facts

| Fact | Value |
|---|---|
| Primary language | PowerShell 7+ |
| GitHub org | kristopherjturner |
| Azure login | kris@hybridsolutions.cloud |
| Key Vault | kv-hcs-vault-01 |

### Environment variables expected

| Variable | Source | Purpose |
|---|---|---|
| `GITHUB_TOKEN` | kv-hcs-vault-01 via Load-HCSEnvironment.ps1 | GitHub CLI and git operations |
| `AZURE_DEVOPS_EXT_PAT` | kv-hcs-vault-01 via Load-HCSEnvironment.ps1 | ADO CLI (`az boards`, `az devops`) |
| `AZURE_SUBSCRIPTION_ID` | kv-hcs-vault-01 via Load-HCSEnvironment.ps1 | Azure CLI subscription context |
Load before starting a session:
```powershell
. E:\git\platform\scripts\Load-HCSEnvironment.ps1
```

### Build and test commands

```
# Run scripts from the scripts/ directory
pwsh -NoProfile -File scripts/<ScriptName>.ps1

# Pester tests (if present)
Invoke-Pester -Output Detailed
```

---

## Repo structure

```
bigbang/
├── .claude/
    └── settings.json
├── .gitlab/
    ├── issue_templates/
    ├── merge_request_templates/
    └── base_config.md.gotmpl
├── .vscode/
    └── settings.json
├── base/
    ├── flux/
    ├── bigbang-dev-cert.yaml
    ├── configmap.yaml
    ├── gitrepository.yaml
    └── helmrelease.yaml
├── chart/
    ├── dashboards/
    ├── templates/
    ├── Chart.yaml
    ├── ingress-certs.yaml
    └── values.yaml
├── dev/
    ├── bigbang.yaml
    ├── configmap.yaml
    └── kustomization.yaml
├── docs/
    ├── assets/
    ├── developer/
    ├── guides/
    ├── prerequisites/
    └── understanding-bigbang/
├── prod/
    ├── bigbang.yaml
    ├── configmap.yaml
    └── kustomization.yaml
├── scripts/
    ├── install_flux.sh
    ├── remove-ns-finalizer.sh
    └── sync.sh
├── terraform/
    ├── modules/
    ├── options/
    ├── storageclass/
    ├── us-gov-west-1/
    └── README.md
├── tests/
    ├── images.txt
    ├── rke2-test-values.yaml
    └── test-values.yaml
├── .gitignore
├── .gitlab-ci.yml
├── .sops.yaml
├── CHANGELOG.md
├── CLAUDE.md
├── CODEOWNERS
├── CONTRIBUTING.md
└── ...
```

---

## Claude Code actions

**Run autonomously:**
- Read, search, and grep any file in this repo
- Write and edit files in this repo
- `git add`, `git commit`, `git push`
- `gh issue`, `gh pr`, `gh run` CLI commands
- `az` CLI read operations: `az ... show`, `az ... list`
- PowerShell scripts in `scripts/` already committed
- `Invoke-Pester` for running tests

**Always confirm before:**
- Creating or deleting Azure resources
- Any `az` CLI write operation that modifies Azure state
- Running destructive operations
- Making API calls to external services
- Any `az` CLI write operation
- Scripts that modify Key Vault secrets or Azure resources

---

## Subagents available in this repo

- `bigbang-engineer` (model: sonnet) — Expert in `bigbang`: deep knowledge of this repo's structure, conventions, and development workflow.

User-level agents (available in every repo session): `triage-lookup`, `markdown-prose-editor`, `azurelocal-domain-expert`, `mkdocs-material-doctor`, `turner-module-scaffold-engineer`, `mms-2026-demo-presenter`.

---

## Owner

**Kristopher Turner**
kris@hybridsolutions.cloud
Senior Product Technology Architect, TierPoint | Microsoft MVP (Azure) | MCT
Owner, Hybrid Cloud Solutions LLC — hybridsolutions.cloud
Country Cloud Boy — thisismydemo.cloud