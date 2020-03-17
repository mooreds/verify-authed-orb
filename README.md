# Verify Authed Orb

This CircleCI orb exposes a command that verifies a user exists and can authenticate against a FusionAuth authentication server.

To use, add the following to your 2.1 CircleCI `config.yml`

```
orbs:
  verifyauth: mooreds/verifyauth@0.0.2
```

Set the following environment variables

`BUILDER_PASS`: the password for the end user you're trying to authenticate
`FUSION_AUTH_API`: the API key for FusionAuth

Then add a set calling the `verifyauth/verifyauth` command:

```
      - verifyauth/verifyauth:
          username: "username"
          applicationid: "1111111111-1111-111111-111111-1111111111"
          hostbaseurl: "https://fusionauth.url"
```

For example:

```
jobs:
  build:
    docker:
      - image: "circleci/node:9.6.1"
    steps:
      - run: echo testing that we are authorized
      - verifyauth/verifyauth:
          username: "user"
          applicationid: "1111111111-1111-111111-111111-1111111111"
          hostbaseurl: "https://fusionauth.url"
      - run: echo success
      - run: echo do the rest of the build

workflows:
  your-workflow:
    jobs:
      - build
```
