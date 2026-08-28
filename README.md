# cloud-platform-lab-infra

Infrastructure-as-code lab: a real **Terraform + GitHub Actions + self-hosted runner +
Azure remote state** delivery chain, built end to end for practice and as portfolio
evidence. Runs on a personal Azure subscription (dev/test).

The engineering board, task specs, agent roles and the Grafana task dashboard live in
[`edymonte/cloud-platform-lab`](https://github.com/edymonte/cloud-platform-lab). The
reusable scaffold behind both is
[`edymonte/engineering-os-template`](https://github.com/edymonte/engineering-os-template).

## Practice curriculum (task sequence)

| Task | Goal |
|---|---|
| TASK-AZ-002 | Pipeline Azure identity — passwordless (Managed Identity / OIDC), least privilege |
| TASK-AZ-003 | Terraform remote-state bootstrap — RG + Storage Account + private container + versioning/soft-delete + RBAC + lock (local state, phase A) |
| TASK-AZ-004 | Migrate the bootstrap to the `azurerm` backend (`init -migrate-state`), verify `No changes.` |
| TASK-AZ-005 | GitHub Actions CI — PR: `fmt` / `init` / `validate` / lint / `plan`, no apply |
| TASK-AZ-006 | GitHub Actions CD — merge -> `azure-dev` environment approval -> self-hosted runner -> `apply` |
| TASK-AZ-007 | A small DEV baseline resource to prove the whole chain, then iterate |

`DELIVERY_CHAIN_READY` stays a personal learning checklist, not a client gate.

## Branch model

| Branch | Meaning |
|---|---|
| `main` | protected; only via PR from `ai-main` |
| `ai-main` | protected; validated integration |
| `task/TASK-NNN-slug` | one task, one branch, PR into `ai-main` |

No direct pushes to `main`/`ai-main`. Apply to Azure runs only from GitHub Actions after
merge + environment approval — never from a workstation (except the one-time remote-state
bootstrap).

## Layout

```
infra/
  bootstrap/tfstate/   two-phase Terraform remote-state bootstrap (TASK-AZ-003/004)
  modules/             cohesive reusable modules
  live/dev/            DEV compositions (platform / connectivity / shared-services / workload)
  backend/             azurerm backend-config .hcl files (non-secret)
.github/workflows/     CI (PR) and CD (apply DEV, approved)
docs/evidence/         per-task evidence for work done in this repo
```

## Runner

Self-hosted runner on the personal Azure VM `vm-gha-runner-01`, label `lab`
(`runs-on: [self-hosted, lab]`). Passwordless auth to Azure via the VM's managed
identity (see TASK-AZ-002).

## Status

Scaffold only. No Terraform logic, no backend, no pipeline yet.
