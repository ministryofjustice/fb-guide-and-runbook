---
category: Form Builder
expires: 2021-01-10
---

## Disaster Recovery

### Infrastructure

The infrastructure for Form Builder is codified in the [Cloud Platform Environments repo](https://github.com/ministryofjustice/cloud-platform-environments/tree/master/namespaces/live-1.cloud-platform.service.justice.gov.uk). There is a [deployment pipeline](https://concourse.cloud-platform.service.justice.gov.uk/teams/main/pipelines/environments-terraform) for which applies the terraform and helm chart configurations.

If any environment needs to be rebuilt from scratch it should simply the case of running the `apply-live-1` job and the base infrastructure will be built for all environments.

### Applications

All Form Builder applications have deployment pipelines in CircleCI. As long as the infrastructure is in place it should simply be the case to run the deployment jobs and the app containers will deploy out to the required environments.

If for some reason the CircleCI jobs have been lost then each app will need to be readded and the required environment variables set. These will differ for each application. See the [fb-deploy](https://github.com/ministryofjustice/fb-deploy) repo for more instructions.

### Databases

Users main submission data is held encrypted in RDS Postgres instances which have regular snapshot backups. We would need to ask the Cloud Platform team to restore these for us if required.

Currently the developers on the MoJ Online team are unable to access the AWS accounts that hold any of our databases and their snapshots. This means that we would need Cloud Platform's assistance to restore any snapshot. If a snapshot recovery is required get in contact with Cloud Platform and follow [these instructions](https://user-guide.cloud-platform.service.justice.gov.uk/documentation/other-topics/rds-snapshots.html#restoring-live-services-from-a-rds-db-snapshot).

Currently the RDS instances we have are:

- Datastore
- HMCTS Adapater
- Metadata API
- Publisher
- Submitter

We also have a Redis Elasticache instance connected to the Service Token Cache, but if this goes down then all the public keys will simply be retrieved from Kubernetes upon the next request to the cache.
