---
category: Using Form Builder
expires: 2021-01-10
---

# Regenerate Google Refresh Token

## Sign into fb-acceptance-tests account

Password is stored in the shared LastPass account. It has 2FA enabled so use one of the backup codes. Regenerate them if required.

## View credentials

Go to the [Devloper Console](https://console.developers.google.com/).

![developer console](/images/refresh_token/developer_console.png)

Click on `Credentials`, and under 'OAuth 2.0 Client IDs' you should see the 'FB Acceptance Tests' credentials.

![credentials page](/images/refresh_token/credentials.png)

Click on that and you will see the Client ID and Client Secret.

![view credentials](/images/refresh_token/view_credentials.png)

## Regenerate Refresh Token

Next go to the [OAuth Playground](https://developers.google.com/oauthplayground). On the right hand side click on the cog icon.

![oauth config](/images/refresh_token/oauth_config.png)

The `Oauth flow` needs to be "Server-side", `Access type` should be "Offline". Tick the `Use your own OAuth Credentials` box and then enter the `Client ID` and `Client secret` from the previous Credentials page into the fields.

On the left hand side of the screen you will see `Step 1 Select & Authorize APIs`.

![playground step 1](/images/refresh_token/playground_step_1.png)

Search for the `Gmail V1 API` and make sure "https://mail.google.com" is selected.

Click `Authorize APIs` and you will be presented with a permissions screen.

![allow access](/images/refresh_token/allow_access.png)

Click `Allow` and follow the instructions.

Step 2 is where you generate the tokens.

![generate refresh token](/images/refresh_token/playground_step_2.png)

Click `Exchange authorization code for tokens`. The Refresh Token is the important one.

You do not need to go to Step 3.

Take a copy of the Refresh Token and add it to the `GOOGLE_REFRESH_TOKEN` environment variable in CI or on your local machine. You will also need the `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET` from the previous credentials screen.
