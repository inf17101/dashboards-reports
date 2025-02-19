## Developer Guide

So you want to contribute code to this project? Excellent! We're glad you're here. Here's what you need to do.

## Setup

1. Download OpenSearch for the version that matches the [OpenSearch Dashboards version specified in package.json](./package.json#L7).
1. Download the OpenSearch Dashboards source code for the [version specified in package.json](./package.json#L7) you want to set up.

1. Change your node version to the version specified in `.node-version` inside the OpenSearch Dashboards root directory.
1. Create a `plugins` directory inside the OpenSearch Dashboards source code directory, if `plugins` directory doesn't exist.
1. Check out this package from version control into the `plugins` directory.
   ```
   git clone git@github.com:opensearch-project/dashboards-reports.git plugins --no-checkout
   cd plugins
   echo 'dashboards-reports/*' >> .git/info/sparse-checkout
   git config core.sparseCheckout true
   git checkout dev
   ```
1. Run `yarn osd bootstrap` inside `OpenSearch-Dashboards/plugins/dashboards-reports`.

Ultimately, your directory structure should look like this:

<!-- prettier-ignore -->
```md
.
├── OpenSearch-Dashboards
│   └──plugins
│      └── dashboards-reports
```

## Build

To build the plugin's distributable zip simply run `yarn build`.

Example output: `./build/reports-dashboards-0.0.1.zip`

## Run

- `yarn start`

  Starts OpenSearch Dashboards and includes this plugin. OpenSearch Dashboards will be available on `localhost:5601`.

- `yarn test:jest`

  Runs the plugin tests.

### Backports

The Github workflow in [`backport.yml`](../.github/workflows/backport.yml) creates backport PRs automatically when the original PR
with an appropriate label `backport <backport-branch-name>` is merged to main with the backport workflow run successfully on the
PR. For example, if a PR on main needs to be backported to `1.x` branch, add a label `backport 1.x` to the PR and make sure the
backport workflow runs on the PR along with other checks. Once this PR is merged to main, the workflow will create a backport PR
to the `1.x` branch.