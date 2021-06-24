---
category: MoJ SaaS Platform
expires: 2021-09-31
---

# Deployments

## Editor

Like other MoJ Forms applications, the Editor is deployed in a Continous Delivery manner using CircleCI with a manual gate to production.

Since it has a significant amount of feature development work that is done concurrently it has a slightly different workflow than the other applications. A developer can deploy out a separate editor in the Test environment that is entirely independent of the one that takes the code from `main`.

The Editor that uses the code on `main` can be found at: `https://fb-editor-test.apps.live-1.cloud-platform.service.justice.gov.uk/`.

### Workflow

It is important that all the unit tests and acceptance tests have been updated and are passing before creating a testable Editor. The purpose of this separate Editor is primarily for manual testing away from the `main` branch. Developers should have already written or updated any unit tests and acceptance tests that are associated with their feature.

The Developer checks out a branch locally and prepends the name of that branch with `testable-`. eg `testable-some-new-awesome-feature`

This branch is what is used to create the URL that a user will visit. The example above becomes `https://testable-some-new-awesome-feature.apps.live-1.cloud-platform.service.justice.gov.uk`. Therefore it is important to _not_ use `/` in branch names as that would then create an invalid URL.

Good: `testable-make-it-work`

Bad: `testable-feature/make-it-work`

Once your branch has been deployed out you will see a message in the `#form-builder-deployments` channel in Slack complete with a URL which can be visited. similar to this one:

![testable editor slack message](/images/testable_editor_success.png)

If however your branch build fails for some reason Jean Luc will express his disappointment with your failure and hope you will do better next time.

![build failure slack message](/images/build_failure.png)

Pipeline overview:

![editor deployment pipeline](/images/editor_deployment_pipeline.png)

### Testable Editor teardown

Once all testing has been completed the Developer can raise a PR from the testable branch as normal for review etc. Once the branch has been merged (and deleted in Github, which is automatic for the Editor repo settings) then a job in CircleCI is triggered which runs a rake task:

`bundle exec rails remove:testable_editors`

The task looks for any branches prepended with `testable-` that have been removed from Github but still exist as `deployments` in Kubernetes and then proceeds to remove all the required configuration associated with those specific Editors and should notify in the `#form-builder-deployments` channel in Slack.

It is dependent upon the environment variable `K8S_SAAS_TOKEN` being set. This is the token for the CircleCI service account associated with the `formbuilder-saas-test` namespace. Most other CircleCI jobs use the token associated with the `formbuilder-repos` namespace CircleCI service account.

If for some reason this is not working or the Developer needs to run it independently of CircleCI they can run the same rake task on their laptop. Before being able to run this the Developer should have set up their Kubernetes config as [documented in the Cloud Platform user guide](https://user-guide.cloud-platform.service.justice.gov.uk/documentation/getting-started/kubectl-config.html#how-to-use-kubectl-to-connect-to-the-cluster).

### Manual Deployments

It is also possible to manually deploy out a specific branch to the test environment. This method will overwrite the Editor at `https://fb-editor-test.apps.live-1.cloud-platform.service.justice.gov.uk/`.

On the branch you are working on just make some changes to the [circle config](https://github.com/ministryofjustice/fb-editor/blob/main/.circleci/config.yml#L227) workflows to add the name of your branch so it triggers CircleCI to deploy it out. For example, given a branch named `my-amazing-branch`:

```
workflows:
  version: 2
  test_and_build:
    jobs:
      - build_and_deploy_to_test:
          filters:
            branches:
              only:
                - my-amazing-branch
```

Pushing up your branch will then trigger CircleCi to deploy it out to the test environment. It might be worth considering commenting out all the jobs in the workflows related to Live and perhaps even Slack notifications.

This approach works for pretty much any app should it be required. The recommendation would be that you would add the above changes to a temporary commit that you would remove from your branch before raising the final PR for review.

Make sure to notify the other developers that you are deploying your branch.
