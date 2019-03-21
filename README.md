# GitHub Action for Sentry.io

Action wraps the [Sentry CLI](https://docs.sentry.io/cli/) to enable Sentry release management.

## Usage

An example workflow to build a docker container from source and push and release the image to an existing application on Heroku:

```hcl
workflow "Create new Sentry Release Version" {
  on = "push"
  resolves = "release version"
}

action "release version" {
  uses = "juankaram/sentry@master"
  needs = "push"
  args = "releases propose-version"
  secrets = ["SENTRY_AUTH_TOKEN"]
  env = {
    SENTRY_ORG     = "foo"
    SENTRY_PROJECT = "bar"
  }
}
```

### Secrets

- `SENTRY_AUTH_TOKEN` - **Required**. The authentication token to use for all communication with Sentry. ([more info](https://docs.sentry.io/cli/configuration/))

### Environment variables

- `SENTRY_ORG` - **Optional**. The slug of the organization to use for a command.
- `SENTRY_PROJECT` - **Optional**. The slug of the project to use for a command.
- `SENTRY_URL` - **Optional**. The URL to use to connect to sentry. This defaults to https://sentry.io/.

## Attribution

Heavily inspired by [GitHub Actions](https://github.com/actions).

## License

The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).
