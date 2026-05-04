# LogicLegion v0 Runbook

## Deployment Topology
LogicLegion v0 is deployed as a containerized service running on Google Cloud Run. This is an alpha/pre-production environment (not production).

## Operational Procedures

### Reverting a Faulty Deployment
If a developer needs to revert a faulty deployment, the following `gcloud` command can be used to roll back the Cloud Run revision by splitting traffic to a previous stable revision:

1. **Find the previous stable revision:**
   ```bash
   gcloud run revisions list --service=logiclegion-service --region=<REGION>
   ```

2. **Roll back the Cloud Run revision:**
   ```bash
   gcloud run services update-traffic logiclegion-service \
     --to-revisions=<PREVIOUS_REVISION_NAME>=100 \
     --region=<REGION>
   ```
