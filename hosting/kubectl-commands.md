---
category: Runbook
expires: 2020-03-31
---

# kubectl Commands

### If a namespace quota is reached

## Describe the namespace
```
kubectl describe namespace <namespace>
```
## List Pods Running
``` bash
kubectl -n <namespace> get pods
```
## More infomation on Pod(s) running
```bash
kubectl -n <namespace> get pods -o wide
```
```bash
kubectl -n <namespace> describe pods
```
```bash
kubectl -n <namespace> describe pod <podname>
```
## Check logs
```bash
kubectl -n <namespace> get events
```
```bash
kubectl -n <nmespace> logs <podname>
```
## Restarting pods
I found the easisest way to restart a pod is to delete them in order, oldest pod first.

```bash
kubectl -n <namespace> delete pod <podname>
```

## Check Cloud Platform Repos for issues



## Checking Concourse Pipeline



## Other Help
[Cloud Platforms Trouble Shooting Guide](https://user-guide.cloud-platform.service.justice.gov.uk/documentation/other-topics/troubleshooting.html#troubleshooting-guide)

Post a message in the #ask-cloud-platform slack channel.



