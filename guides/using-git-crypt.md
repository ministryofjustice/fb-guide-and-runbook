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

### Adding a new collaborator to a git-crypt repo

You need to get the public key from the user you wish to add. You can use the ID of the public key or their email address, basically the thing which identifies their key.

e.g

```
pub   rsa4096 2020-06-15 [SC]
      F829701787B97465C7E503E9976DB76C0F8DE955
uid   [ultimate] From Builder Team <form-builder-team@digital.justice.gov.uk>
sub   rsa4096 2020-06-15 [E]
```

The ID in the above case is `F829701787B97465C7E503E9976DB76C0F8DE955`.

You will need to trust their key ultimately before git-crypt will allow you to add them as a collaborator.

`gpg --edit-key F829701787B97465C7E503E9976DB76C0F8DE955`

Then type `trust`.

The options you will be presented with are:

```
1 = I don't know or won't say
2 = I do NOT trust
3 = I trust marginally
4 = I trust fully
5 = I trust ultimately
m = back to the main menu
```

Choose `5` and follow the prompts.

Assuming your repo is `unlocked`, you'll then be able to add that user to your git-crypt repo:

`git-crypt add-gpg-user F829701787B97465C7E503E9976DB76C0F8DE955`

git-crypt adds the users public key and then automatically adds a commit to the repo in the background.
