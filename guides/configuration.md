---
category: Using Form Builder
expires: 2021-01-10
---

# Configuration

These are the available configuration options currently:

## User configurable in the Publisher

Name | Function
------------ | -------------
DEPLOYMENT_REPLICAS | The number of containers deployed in each environment for that form. Default is 2
EXCLUDE_FROM_SEARCH_RESULTS | Stop forms from appearing in search engine results. Default is `false`
FB_GA_TEST | Enables the Form Builder GA tracking if required for testing
FORM_BUILDER_GA_TRACKING_ID | Form Builder Team Google Analytics ID
GA_TRACKING_ID | Google Analytics ID
GTM_TRACKING_ID | Google Tag Manager ID
MAINTENANCE_MODE | Flag to put a form under maintenace and make sure that all pages redirect to the maintenance page (with the exception of ping and healthcheck url)
PASSWORD | Basic authentication password
RESOURCES_LIMITS_CPU | The max compute processing allowed for a container the form is deployed to
RESOURCES_LIMITS_MEMORY | The max memory allocation allowed for a container the form is deployed to
RESOURCES_REQUESTS_CPU | The amount of system compute processing that is reserved for a container the form is deployed to
RESOURCES_REQUESTS_MEMORY | The amount of system memory resource allocated that is reserved for a container the form is deployed to
SERVICE_OUTPUT_CSV | if set eg 'true'. send email with CSV attachment to SERVICE_OUTPUT_EMAIL
SERVICE_OUTPUT_EMAIL | email address to send form output to
SERVICE_OUTPUT_JSON_ENDPOINT | The endpoint which JSON payloads will be sent to
SERVICE_OUTPUT_JSON_KEY | The encryption key used by the runner to encrypt payloads sent to the JSON adapter
SERVICE_SLUG | Slug that identifies service within FB platform. This is the entry point into the app, _not_ the domain
USERNAME | Basic authentication username

## Form Builder configurable

Name | Function
------------ | -------------
APP_DIR | location of app
APP_SHA | version of app
ASSET_PATH | CURRENTLY FIXED. physical location of assets - defaults to [root dir]/public
ASSET_SRC_PATH | CURRENTLY FIXED. url prefix for assets - defaults to /assets
DEPLOYMENT_ENV | Deployment environment which form is deployed to
EMAIL_URL | Url for making requests to send emails. Currently same as SUBMITTER_URL
ENV | environment type
FQD | Fully qualified domain name for form
LOG_LEVEL | Level at which bunyan should log at
NUNJUCKS_NOCACHE | whether nunjucks should not cache output (true/false) defaults to true
NUNJUCKS_WATCH | whether nunjucks should watch templates (true/false) defaults to false
PLATFORM_ENV | Platform environment which form is deployed to
PORT | port to listen on - defaults to 3000
RUNNER_DIR | location of runner
SAVE_RETURN_URL | Url for making requests to save and return api. Currently same as USER_DATASTORE_URL
SENTRY_DSN | Sentry ID
SERVICE_PATH | physical location of site metadata
SERVICE_SECRET | Secret for encrypting values that should only be accessible by runner
SERVICE_SHA | version of deployed form
SUBMISSION_ENCRYPTION_KEY | The key used to encrypt the submission before sending it to the Submitter
SUBMITTER_URL | Url for making requests to submitter
USER_DATASTORE_URL | Url for making requests to user datastore
USER_FILESTORE_URL | Url for making requests to user filestore
