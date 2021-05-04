---
category: MoJ Forms Platform
expires: 2021-09-31
---

# HMCTS Adapter

Handles submissions for two forms on behalf of HMCTS. It maps submission payloads to the required keys before sending them on to the OPTICS case management system.

Repository: https://github.com/ministryofjustice/hmcts-complaints-formbuilder-adapter

Despite the name it accepts submissions for both complaints and correspondence form types.

The two namespaces associated with it are:

- hmcts-complaints-formbuilder-adapter-production
- hmcts-complaints-formbuilder-adapter-staging

Both forms require `SERVICE_OUTPUT_JSON_ENDPOINT` and `SERVICE_OUTPUT_JSON_KEY` to be set in their configuration before publishing.

## Complaints

Form repository: https://github.com/ministryofjustice/fb-hmcts-complaints

It is called `complain-about-a-court-or-tribunal` in the [Publisher](https://fb-publisher-live.apps.live-1.cloud-platform.service.justice.gov.uk/services/complain-about-a-court-or-tribunal).

The API endpoint is `/v1/complaint`.

The first. It works. Just let it be.

## Correspondence

Form repository: https://github.com/ucd-hmcts/money-claim-queries

It is called `Money claim queries` in the [Publisher](https://fb-publisher-live.apps.live-1.cloud-platform.service.justice.gov.uk/services/money-claim-queries).

The API endpoint is `/v1/correspondence`.

This has significant business logic in order to map the correct properties that OPTICS is expecting. [The code](https://github.com/ministryofjustice/hmcts-complaints-formbuilder-adapter/blob/master/app/lib/presenter/correspondence.rb) is very much the documentation here so there is no need to repeat it.

The form caters for two different types of users (the person filling out the form). In terms of nomenclature the `Applicant` is always the person filling out the form.

### Representing

The `Applicant` in these instances are also known as a `Representative` . OPTICS also has the idea of an `Intermediary` but currently there is nothing in the form that maps this in the payload.

They will be filling out the form on behalf of a `Client` or `Subject`.

OPTICS will log this user as an `Agent`.

### Self Representing

The `Applicant` is filling out the form for themselves.

OPTICS will log this user as `Main`.

### Other considerations

There is one unused field, `CaseContactCustom18.Subject`, which was meant the `Intermediary` mentioned above but in the end it was decided not to be used. We have left it in there as OPTICS still allows the property in the payload despite it not being filled.
