# Form Builder Guide and Runbook

## Introduction

Form builder is a tool for creating and publishing digital forms using components from the GOV.UK Design System.

It uses 4 applications: Console, Editor, Publisher, Runner.

### Console
The Console is a Node.js app built using the Electron Framework. To create a new form or edit an existing one, you must install the Console on your local machine.

### Editor
The Editor is a Node.js app that allows you to make changes to the forms you’ve created (update form schemas). You can only run the Editor on your local machine. You can use GitHub to push your changes to version control. The Publisher app will pull these changes which will update your forms in the cloud.

### Publisher
Publisher is a Ruby on Rails app deployed to the Cloud platform. You will need to use it to deploy your forms. Once you have deployed a form, the Publisher will fetch the latest version from GitHub.

### Deploying a form
Deploying a form fetches the form schema from GitHub and creates runner instances and ingresses inside the Cloud platform. There is a short delay between deploying a form and seeing it published online. There is also a short delay between deploying changes to a form and seeing them online.

### Runner
This is a Node.js app that displays forms to end users. Runners are single-tenanted, and each runner instance hosts an individual form.

An example of a runner (live version of a form) is Complain about a court of tribunal.

### Form Builder Support
For help using Form Builder, email the Form Builder team on form-builder-team@digital.justice.gov.uk or contact us on the #ask-formbuilder Slack channel.

## Guides

{% assign guides = site.pages
  | where: "guide", true
  | group_by: "category" %}

{% for guide_group in guides %}
{% if guide_group.name != "" %}
### {{ guide_group.name }}
{% else %}
### General
{% endif %}

{% for guide in guide_group.items %}
- [{{ guide.title }}]({{ guide.url | relative_url }})
{% endfor %}
{% endfor %}

## Troubleshooting

{% assign troubleshootings = site.pages
  | where: "troubleshooting", true
  | group_by: "category" %}

{% for troubleshooting_group in troubleshootings %}
{% if troubleshooting_group.name != "" %}
### {{ troubleshooting_group.name }}
{% else %}
### General
{% endif %}

{% for troubleshooting in troubleshooting_group.items %}
- [{{ troubleshooting.title }}]({{ troubleshooting.url | relative_url }})
{% endfor %}
{% endfor %}


## Hosting
Form Builder is hosted on the Ministry of Justice Cloud Platform. To be able to use it, you need to connect to the cluster.

If you have any questions about the Cloud Platform, contact the Cloud Platform team on the #ask-cloud-platform Slack channel.

### Environments
Environments are split into slightly unusual groupings. It's unfortunately complicated.

Environment Type | Potential Value
------------ | -------------
Platform Environment | `test` or `live`
Deployment Environment | `dev` or `production`

The Platform Environment `test` is used only by developers. `live` is used by form owners and also relates to public facing forms. Conceptually it might be helpful to think of the `dev` part of the Deployment Environment to represent a "draft" or "preview" state of a service and the `production` Deployment Environment to represent a "published" state of a service.

These types are then amalgamated and used to describe the full namespaces (more on that below). They take the following forms:

Platform Deployment | Description
------------ | -------------
test-dev | Developer only environment that is used for acceptance testing and a representation of all things in "preview" or "draft"
test-production | Developer only environment that is effectively meant to represent a `test` version of a published service
live-dev | Mainly used by form owners for previewing their forms
live-production | The public facing, published forms

High level overview of the platform and services as well as the user facing elements which may help to explain the groupings better:

![environments overview](/images/mojo_environments.png)

There are some applications that are deployed to a specific Platform Environment but they straddle both Deployment Environments

- Publisher
- V2 Editor
- Metadata API

These apps manage the transition between draft/preview and fully published.

### Namespaces
In each of these environments there are two namespaces - Services and Platform. The Services namespace contains the runners. The Platform namespace holds all the backend components.

There are then two publisher environments, one for test and one for live.

These are the namespaces that currently make up the Form Builder product:

Namespace | Purpose
------------ | -------------
formbuilder-base-adapter-test | The base adapter is there to emulate an API endpoint for the JSON output
formbuilder-monitoring | Contains all the infrastructure monitoring for the Form Builder platform
formbuilder-platform-live-dev | Contains all the platform apps for the live-dev environment
formbuilder-platform-live-production | Contains all the platform apps for the live-production environment
formbuilder-platform-test-dev | Contains all the platform apps for the test-dev environment
formbuilder-platform-test-production | Contains all the platform apps for the test-production environment
formbuilder-product-page-prod | The Form Builder product page in the production environment
formbuilder-product-page-staging | The Form Builder product page in the staging environment
formbuilder-publisher-live | The Form Builder publisher catering for services running in live-dev and live-production
formbuilder-publisher-test | The Form Builder publisher catering for services running in test-dev and test-production
formbuilder-repos | Contains all the ECR repos required for all the Form Builder applications
formbuilder-saas-test | Contains the V2 Form Builder Editor and Metadata API applications for the test environment
formbuilder-services-live-dev | Contains all the form services pods for the live-dev environment
formbuilder-services-live-production | Contains all the form services pods for the live-production environment
formbuilder-services-test-dev | Contains all the form services pods for the test-dev environment
formbuilder-services-test-production | Contains all the form services pods for the test-production environment
hmcts-complaints-formbuilder-adapter-production | Contains the HMCTS Complaints Adapter for the production environment
hmcts-complaints-formbuilder-adapter-staging |  Contains the HMCTS Complaints Adapter for the staging environment

{% assign hostings = site.pages
  | where: "hosting", true
  | group_by: "category" %}

{% for hosting_group in hostings %}
{% if hosting_group.name != "" %}
### {{ hosting_group.name }}
{% else %}
### General
{% endif %}

{% for hosting in hosting_group.items %}
- [{{ hosting.title }}]({{ hosting.url | relative_url }})
{% endfor %}
{% endfor %}

### Other Help
[Cloud Platforms Trouble Shooting Guide](https://user-guide.cloud-platform.service.justice.gov.uk/documentation/other-topics/troubleshooting.html#troubleshooting-guide])

Post a message in the #ask-cloud-platform slack channel.

## Technical and Security Guidance

Both the [technical](https://ministryofjustice.github.io/technical-guidance/) and [security](https://ministryofjustice.github.io/security-guidance/) should be read.

