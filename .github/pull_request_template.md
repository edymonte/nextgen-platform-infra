## Task

<!-- TASK-NNN / TASK-AZ-NNN — link to the task in cloud-platform-lab -->

## What changed

## Terraform evidence

- [ ] `terraform fmt -check -recursive`
- [ ] `terraform init`
- [ ] `terraform validate`
- [ ] `terraform plan` reviewed (summary below / linked artifact)

```
<plan summary — no secrets, no full state>
```

## Checklist

- [ ] Branch is `task/TASK-NNN-slug`, PR targets `ai-main` (not `main`)
- [ ] No secrets, tenant/subscription IDs, or `.tfstate` added
- [ ] Least-privilege `permissions:` on any workflow touched
- [ ] Cost impact stated (resource, SKU, region, paid/free, cheaper option)
- [ ] Rollback documented
