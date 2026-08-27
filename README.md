# nextgen-platform-infra

Terraform + GitHub Actions delivery for the **NextGen Platform** Azure foundation
(Phase 1). This repository holds infrastructure code only; the engineering board,
docs and task dashboard live in `edymonte/nextgen_pilot`.

`LANDING_ZONE_READY = false` — this repo builds and proves the delivery chain
(runner → identity → Terraform → Azure Blob remote state → Azure DEV) before any
full Landing Zone work. See
`nextgen_pilot:Docs/Escopo/NEXTGEN_PLATFORM_AZURE_LANDING_ZONE_IMPLEMENTATION_CONTEXT_v1.1.md`.

## Branch model

| Branch | Meaning |
|---|---|
| `main` | protected; production-intent; only via PR from `ai-main` |
| `ai-main` | protected; validated integration |
| `task/TASK-NNN-slug` | one task, one branch, PR into `ai-main` |

No direct pushes to `main` or `ai-main`. Apply to Azure happens only from GitHub
Actions after merge + environment approval, never from a workstation (except the
one-time remote-state bootstrap).

## Layout

```
infra/
  bootstrap/tfstate/   two-phase Terraform remote-state bootstrap (TASK-AZ-003/004)
  modules/             cohesive reusable modules
  live/dev/            DEV compositions (platform / connectivity / shared-services / workload)
  backend/             azurerm backend-config .hcl files (non-secret)
.github/workflows/     CI (PR: fmt/init/validate/lint/plan) and CD (apply DEV, approved)
docs/evidence/         per-task evidence for work done in this repo
```

## Runner

Self-hosted runner on the existing Azure VM `vm-gha-runner-01`, label `nextgen-dev`
(`runs-on: [self-hosted, nextgen-dev]`). Passwordless auth to Azure (see TASK-AZ-002).

## Status

Scaffold only (TASK-006). No Terraform logic, no backend, no pipeline yet.
