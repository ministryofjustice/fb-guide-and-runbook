---
category: Using Form Builder
expires: 2021-01-10
---

# Regenerate Google Access Token

## Sign into fb-acceptance-tests account

Password is stored in the shared LastPass account. It has 2FA enabled so use one of the backup codes. Regenerate them if required.

## Download credentials

Go to the [Devloper Console](https://console.developers.google.com/).

![developer console](/images/generate_token/developer_console.png)

Click on `Credentials` and then `Download JSON`.

![download credentials](/images/generate_token/download_credentials.png)

Rename the file to `credentials.json` and then move it to `fb-acceptance-tests/scripts/credentials.json`.

## Run the generation script

Run the token generation script:

~~~~~~~~
ruby fb-acceptance-tests/scripts/generate_access_token.rb
~~~~~~~~

This will output a URL to the command line and then wait for you to enter a code.

Visit that URL in the browser which you logged into the fb-acceptance-tests account. You will be prompted to allow access by the fb-acceptance-tests app. Allow this and then copy the code that is shown on the next screen into the terminal.

The script will then output the required environment variables that you need to set either locally or in the CI pipeline in order for the acceptance tests to authenticate with the Gmail API.
