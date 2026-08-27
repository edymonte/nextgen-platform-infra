# .github/workflows

- `terraform-pr.yml` (TASK-AZ-005) — on PR to `ai-main`/`main`: checkout, Azure auth,
  `fmt -check`, `init`, `validate`, lint/security, `plan`. No apply.
- `terraform-apply-dev.yml` (TASK-AZ-006) — on merge to a protected branch: environment
  `azure-dev` approval, self-hosted runner, `init`, `plan`, `apply`. `concurrency` per
  stack.

Empty until those tasks. Workflows must set explicit least-privilege `permissions:` and
pin third-party actions by commit SHA.
