---
category: MoJ Forms Editor
expires: 2021-09-31
---

# Auth0

Locally the [MoJ Forms Editor](https://github.com/ministryofjustice/fb-editor) uses the devloper callback that comes with Auth0 in order to present the user with a faux login screen. However in production it will actually show the Universal Login page that is configured in the [moj-forms tenant](https://manage.auth0.com/dashboard/eu/moj-forms/).

There are two connections configured currently, Google and Microsoft. The former is set up using a Social connection and the latter is configured using Enterprise Azure AD.

Currently the only user data we keep is their name and email address, both of which are encrypted before being saved in the DB.

The Universal Login screen can be configured directly in the moj-forms tenant dashboard. It is possible to create custom HTML and JS.

There are two editor apps, one for Live and one for Test. Aside from the obvious differences between callback URLs, the Test app also has the username and password fields active in order for the acceptance tests to be able to log in.

## Debugging

If a developer needs to debug the real login screen then they will need to change the URL that the initial POST request goes to. This resides in the home controller of the Editor app. `/auth/developer` would need to be changed to `/auth/auth0`. They will also need to add `http://localhost:3000/auth/auth0/callback` to the Allowed Callback URLs list and `http://localhost:3000` to the Allowed Logout URLs list. Both are comma separated lists.

You will also need to set the following environment variables:

```
AUTH0_CLIENT_ID
AUTH0_CLIENT_SECRET
AUTH0_DOMAIN
```

Once those changes are in place, opening the editor locally in an incognito window, or clearing the associated cookie, will allow a login experience very similar to what an end user will see.
