# LogicLegion v0 RUNBOOK

## Deployment Topology
LogicLegion v0 is deployed as a containerized application running on Google Cloud Run.
This document outlines the current non-production deployment topology and operational procedures.

### Infrastructure Components
- **Compute:** Google Cloud Run (fully managed serverless platform).
- **Registry:** Artifact Registry (for storing Docker images).

## Operational Procedures

### Rollback a Faulty Deployment
If a deployment fails or exhibits issues, you can revert traffic to a previous known-good Cloud Run revision.

To find available revisions:
```bash
gcloud run revisions list --service=logiclegion-v0
```

To roll back the Cloud Run revision to a previous state, route 100% of traffic to the desired revision:
```bash
gcloud run services update-traffic logiclegion-v0 \
  --to-revisions=logiclegion-v0-xxxxx=100
```
Replace `logiclegion-v0-xxxxx` with the target revision name.
