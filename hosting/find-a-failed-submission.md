---
category: Hosting Runbook
expires: 2020-03-31
---

# Find a failed submission in the queue
If there’s a failed submission in the queue, you should see a notification in the #form-builder-alerts Slack channel. The alert will show you which environment the job or submission is failing in.

Once you know which environment the failure is in, log on to one of the submitter components through Kubernetes.

* Identify the submitter pods that you can log in to
```
kubectl get pods -n formbuilder-platform-live-production | grep submitter-worker
```
* Log in to one of those pods
```
kubectl exec -ti -n formbuilder-platform-live-production POD_NAME ash
```
* Start a Ruby on rails console
```
bundle exec rails c
```
* Identify the first failed job
```
dj = Delayed::Job.first
```
* Display the stack trace of the error
```
dj.last_error
```
* Find the location of the submission
```
Submission.find(dj.payload_object.submission_id)
```
