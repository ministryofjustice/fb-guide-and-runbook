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

## Hosting
Form Builder is hosted on the Ministry of Justice Cloud Platform. To be able to use it, you need to connect to the cluster.

If you have any questions about the Cloud Platform, contact the Cloud Platform team on the #ask-cloud-platform Slack channel.

### Environments
There are 2 two environments, live and test.

**Live**
The live environment holds all the production forms.

**Test**
The test environment is for testing component changes (eg runner, file store, data store, pdf generator).

Within each of these environments the user has two environments - Staging and Production.

**Staging**
Form Editors can use Staging to keep test versions of their forms for checking before going live with them.

**Production**
Once a form editor is ready to make their form fully live, they can publish it in Production.

### Namespaces
In each of these environments there are two namespaces - Services and Platform. The Services namespace contains the runners. The Platform namespace holds all the backend components.

There are then two publisher environments, one for test and one for live.

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

## Adding new guidance

Create a new Markdown file that follows this pattern, add a link to it
from this page, and make a pull request:

```markdown
---
category: The broader area this fits into
expires: yyyy-mm-dd (6 months from now)
---
# Thing you're writing about

Introduction of a couple of paragraphs to explain why the thing you're
writing about is important. The [title should probably be a verb, not a
noun][good-services-are-verbs] (e.g. “Storing source code”, not “Code
repositories”).

[good-services-are-verbs]: https://designnotes.blog.gov.uk/2015/06/22/good-services-are-verbs-2/

## User needs

Why do we do this thing? Who is it helping?

## Principles

What broad approaches do we follow when we do this thing?

## Tools

What specific bits of software (commercial or open source) do
we use to help us do this thing?
```

The service manual has some useful information on [learning about and writing user needs](https://www.gov.uk/service-manual/user-research/start-by-learning-user-needs).
