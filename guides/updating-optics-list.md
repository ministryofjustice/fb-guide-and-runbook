---
category: Using Form Builder
expires: 2021-06-17
---

# Updating OPTICS list on the HMCTS Online Complaints Form
The OPTICS list is found on the HMCTS Online Complaint Form. This is an autocomplete list that contains a number of courts and tribunals. Form users are currently unable to edit autocomplete lists so the Form Builder developers need to do this for them.


## Pre-requisites
- Clone the [fb-hmcts complaints](https://github.com/ministryofjustice/fb-hmcts-complaints) repo
- Run `npm install` to install Node dependencies

## Procedure
- Remove the desired courts/tribunals from the `OPTIC-courts-list.csv` file
- Run `node index.js`

This will update the autocomplete items on the location page.

As a result the `metadata/page/page.location.json` and `optics/courts-list-options.json` files will have updated to reflect the changes in the csv file.

- Add the names and/or value of items excluded to the `OPTIC-exclude.txt` file.

## Testing the new form
You can test the new form in the `test-dev` environment. This involves running the Publisher in a test environment, [Test Form Builder Publisher](https://fb-publisher-test.apps.live-1.cloud-platform.service.justice.gov.uk/services)

## Deploying
- Add, commit and push the changes to Github.
- Someone will need to merge these changes before you can Publish the form.
- Once, the changes have been approved, you can publish the form via the [Production Form Builder Publisher](https://fb-publisher-live.apps.live-1.cloud-platform.service.justice.gov.uk/services)
