---
category: Using Form Builder
expires: 2021-10-31
---

# Deleting services

## Kubernetes

There are 5 commands that need to be run per form. Assuming the name of your form is `dummy-form` and we are deleting forms in the `formbuilder-services-test-dev` namespace:

- kubectl delete deployment dummyform -n formbuilder-services-test-dev
- kubectl delete ingress dummyform-ingress -n formbuilder-services-test-dev
- kubectl delete service dummyform -n formbuilder-services-test-dev
- kubectl delete configmaps fb-dummyform-config-map -n formbuilder-services-test-dev
- kubectl delete secrets fb-dummyform-secrets -n formbuilder-services-test-dev

This assumes that the naming convention for each form has not changed recently. i.e ingress name is always `<form-name>-ingress` etc.

## Metadata API

To delete the forms in the API you will need to log into a metadata-api container in the required namespace and manually delete the form you want.

## Service Configuration

Each service has configuration saved to the editor DB. This will also need to be deleted per service manually.

## Automated Deletion

All of the above will happen automagically when we get round to writing it.
