# LogicLegion v0 Runbook

This document serves as the central reference for the deployment topology and basic operational procedures for LogicLegion v0 (alpha environment).

## Deployment Topology

LogicLegion v0 is deployed as a containerized application running on Google Cloud Run. 

## Operational Procedures

### Reverting a Faulty Deployment

If a recent deployment causes issues, you can roll back to a previous revision using the `gcloud` CLI.

1. List the available revisions to find the name of the previous stable revision:
   ```bash
   gcloud run revisions list --service logiclegion-v0 --region <YOUR_REGION>
   ```

2. Update the traffic allocation to point 100% of the traffic to the stable revision:
   ```bash
   gcloud run services update-traffic logiclegion-v0 \
       --region <YOUR_REGION> \
       --to-revisions=<STABLE_REVISION_NAME>=100
   ```
