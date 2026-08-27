# infra/bootstrap/tfstate

Two-phase bootstrap of the Terraform **remote state** backend (Azure Blob Storage).

- Phase A (TASK-AZ-003): create RG + Storage Account + private container + versioning
  + soft delete + RBAC + resource lock, using a **temporary local state** (never
  committed — see repo `.gitignore`).
- Phase B (TASK-AZ-004): enable `backend "azurerm" {}`, `terraform init -migrate-state`
  with `../../backend/bootstrap.hcl`, verify `terraform state list` and a clean
  `terraform plan` (`No changes.`).

Empty until TASK-AZ-003. `prevent_destroy` will guard the critical resources.
