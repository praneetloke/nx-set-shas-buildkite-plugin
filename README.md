# nx-set-shas-buildkite-plugin

A Buildkite plugin to set base and HEAD SHAs for Nx.

This plugin will search for the last successful commit in your base branch (if current build is a PR)
or the current branch and sets the environment variables: `NX_BASE` and `NX_HEAD`.

You can use the environment variables this plugin sets to run the `nx affected ...` command in
a Buildkite pipeline. Running `nx affected ...` allows Nx to only run the selected targets only
for the affected projects. This is important if you have a few projects in your monorepo and would
not like to run build targets for all the projects every time.

For more background on the problem, see the Nx docs for the `affected` [command](https://nx.dev/ci/features/affected).

## Usage

Create an [API access token](https://buildkite.com/user/api-access-tokens) for your organization with the GraphQL scope.

Add this plugin along with any other plugins you are using.

```yaml
steps:
  ...
  ...
  - label: "Run nx"
    commands:
      - npx nx affected -t lint build test
    plugins:
      ...
      ...
      - secrets:
          variables:
            GRAPHQL_API_TOKEN: GRAPHQL_API_TOKEN
      - nx-set-shas#v1.0.0
      ...
      ...
  ...
  ...
```
