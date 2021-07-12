---
category: Using Form Builder
expires: 2022-01-12
---

# Alerts Guide

Most of the information can be found in the [MOJ Form Builder Runbook](https://ministryofjustice.github.io/fb-guide-and-runbook/#form-builder-guide-and-runbook)
This is a quick guide about the common alerts you may come across in the [#form-builder-alerts](https://mojdt.slack.com/archives/CH4FJB8E4) channel.

## Application Related Alerts

### Failed Delayed Jobs
This is something that needs to be investigated. A walk through of how to investigate these alerts are found in the [MOJ Form Builder Documentation](https://ministryofjustice.github.io/fb-guide-and-runbook/troubleshooting/find-a-failed-submission/#delayed-job-failures)

### Client Error Response
These usually resolve within 5 minutes of firing.
If there are a number (say 5 or more) of these alerts in short succession, it could be a bot trying to get into the service.

### Slow Responses
These usually resolve quickly after firing with no intervention needed.


## Kubernetes Related Alerts

### Kube Namespace Quota Nearing
We have an alert that lets us know when we hit 80%. If this goes off it could be because the pods are creating and draining, which is normal. To check this run:

`kubectl get pods -n <namespace>`

This will give you all the pods in a namespace. There should be 2 for each form, if there are some that are restarting then you may have more than 2 - which could be why the quota has been reached. If this is the case, then there is no issue.
If there are no pods restarting in the list, the best to chat with the team about whether we need to increase the number of pods.

### Kube Pod Crash Looping
Each form has 2 pods, so the form should still be running despite a pod being down. Check the form, then check the logs. A way to fix this could be to restart the problem pod.

[Documentation]((https://ministryofjustice.github.io/fb-guide-and-runbook/hosting/kubectl-commands/#check-logs)) on checking the logs and restarting the pods.

### Namespace Missing
To check whether the namespace is missing:

`kubectl get namespace | grep < namespace >`

If the namespace is there, then there isn’t much to worry about. If it doesn’t resolve itself and the namespace is there, it might be worth flagging with cloud platform.
If the namespace is in fact not there, then we have a problem and will need to let the other devs know.

### Kube Pod Not Ready
There are always 2 pods for every form, as such this alert is generally nothing to worry about. This should resolve itself once the pod is up and running.

## Sentry related alerts
All Sentry alerts are found on the [Sentry dashboard](https://sentry.io/organizations/ministryofjustice/issues/).
Please ensure the alert is resolved once you have completed your investigation, otherwise we will not be alerted for the unresolved error in future.

### Faraday::Unprocessable Entity Error
This is the metadata-api returning a 422, this happens when either:

- The user has tried to create a page with a URL that already exists
- The editor is trying to send metadata to the API that it shouldn’t be

If the issue is the former, then that is not anything we need to investigate.

However, if it is due to the Editor sending metadata it should not be sending, we will need to investigate the issue further.

### Action View Template Error
This could be due to a form owner interacting with a form that was made prior to breaking changes were introduced.
This is not a serious issue, we may need to ask the form owner to re-publish a form to get the latest changes.

### Net Read Timeout
This usually occurs on the HMCTS complaints adapter. Generally it is a communication error with Optics, it is best to keep an eye out for any ‘Failed Delay Jobs’ alerts as this will point to the job not being processed.

### Type Error
If this is for the GET `/upload-upload-summary` endpoint, this is a known error and from the legacy Runner. No need to do anything about this.
