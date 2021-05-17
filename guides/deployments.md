---
category: MoJ SaaS Platform
expires: 2021-09-31
---

# Deployments

## Editor

Like other MoJ Forms applications, the Editor is deployed in a Continous Delivery manner using CircleCI with a manual gate to production.

While we come up with a more resilient technical solution to allow for QA testing changes on the Editor, it is possible to manually deploy out a specific branch to the test environment.

Just make some changes to the [circle config](https://github.com/ministryofjustice/fb-editor/blob/main/.circleci/config.yml#L111) workflows to add the name of your branch so it triggers CircleCI to deploy it out. For example, given a branch named `my-amazing-branch`:

```
workflows:
  version: 2
  test_and_build:
    jobs:
      # - test
      - build_and_deploy_to_test:
          # requires:
          #   - test
          filters:
            branches:
              only:
                - main
                - my-amazing-branch
```

The example above also comments out the `test` job and the requirement for the job to pass before pushing out the branch. This approach works for pretty much any app should it be required. The recommendation would be that you would add the above changes to a temporary commit that you would remove from your branch before raising the final PR for review.

Make sure to notify the other developers that you are deploying your branch.
