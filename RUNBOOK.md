# RUNBOOK: LogicLegion v0

## Deployment Topology
LogicLegion v0 is deployed as a single Cloud Run service acting as a throwaway test target. It is isolated from other services and serves as an initial architecture dry-run. 

*Note: This is a non-production service. It does not claim production status.*

## Rollback Procedure
If a deployment is faulty, revert the Cloud Run revision immediately to restore stability.

Use the exact `gcloud` command to rollback traffic:
```bash
gcloud run services update-traffic <service-name> --to-revisions=<revision>=100
```
*(Alternatively, `gcloud run services rollback <service-name>` can be used for the latest stable revision)*

## Security & Operational Constraints
- No secrets, DSNs, or cookie values should ever be hardcoded or documented in plain text.
- Refer to the system environment variables or secret manager for sensitive values.