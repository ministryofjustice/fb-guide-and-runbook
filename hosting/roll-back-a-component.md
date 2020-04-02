---
category: Hosting Runbook
expires: 2020-03-31
---

# Roll back a component

We use [CircleCI](https://circleci.com/workflow-run/5949728f-0971-4b31-a45e-335671daedfd) for deployments.

To roll back a component, you need to [find the relevant component workflow](https://circleci.com/workflow-run/5949728f-0971-4b31-a45e-335671daedfd) within Circle CI.

Find the previous version you want to deploy, then trigger the workflow for that version.

This will run a test for the component, and then build and deploy the component to the test environment. Once complete, you can deploy the component to live.