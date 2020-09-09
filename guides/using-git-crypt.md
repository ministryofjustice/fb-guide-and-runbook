---
category: Using Form Builder
expires: 2021-01-10
---

# Using git-crypt

The Form Bulder platform and services use git-crypt in order to encrypt secrets. The repos that contain them are checked out in each app's deployment pipeline and the decrypted for injection into the app's configuration.

Each time a new secrets repo is initialised (`git-crypt init`) a symmetric key is generated for that specific repo. This key can be shared and used for decrypting the secrets in deployment pipelines.

### Export the symmetric private key

`git-crypt export-key /save/path/for/private.key`

This keys' format is specific to git-crypt. It will need to be base64 encoded before being added to each pipeline in a environment variable called `ENCODED_GIT_CRYPT_KEY`.
