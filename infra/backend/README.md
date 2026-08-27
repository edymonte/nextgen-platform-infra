# infra/backend

`azurerm` backend-config files (`*.hcl`), one per state, e.g.:

```
bootstrap.hcl
dev-platform.hcl
dev-connectivity.hcl
dev-shared-services.hcl
dev-workload.hcl
```

Non-secret only: `resource_group_name`, `storage_account_name`, `container_name`,
`key`. No credentials. Files ending `.local.hcl` are git-ignored.
