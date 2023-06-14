<h2 align="center">
  <br>
  <p align="center"><img src="https://raw.githubusercontent.com/reliablyhq/cli/main/public/logo.png"></p>
</h2>

<h4 align="center">Reliably GitHub Actions | Optimise your operations</h4>

<p align="center">
   <a href="https://github.com/reliablyhq/actions/blob/master/LICENSE.md">
   <img alt="License" src="https://img.shields.io/github/license/reliablyhq/cli">
</p>

<p align="center">
  <a href="#installation">Installation</a> •
  <a href="https://reliably.com/docs/cli/">Documentation</a>
</p>

---

The Reliably CLI is your interface to the Reliably services. 


# Requirements

This action requires the following:

* That you have created an account with [Reliably][reliably]
* A token. You can generate one from the [Reliably dashboard](token) then
  store it as an Environment secret in your GitHub repository under the name
  `RELIABLY_SERVICE_TOKEN`

[reliably]: https://reliably.com
[token]: https://app.reliably.com/settings/tokens/


# Actions

## Plan

[plan]: https://reliably.com/docs/concepts/plans/

The main action in this repository is the `plan` action. It features:

* Runs [Reliably plan](plan) from within a GitHub workflow
* Allows you to keep your sensitive data in a GitHub Environment so that
  you keep them close to your operations
* Reports its results back to Reliably
* Stores the result files (the log and journal) as a commit in the repository
* Stores a file listing all the licences of all the packages used as part
  of run within the commit

The basic action usage is as follows:

```yaml
name: Execute a Reliably Plan

on:
  workflow_dispatch:

jobs:
  execute-reliably-plan:
    runs-on: ubuntu-22.04
    steps:
    - uses: actions/checkout@v3
    - uses: reliablyhq/actions/plan@main
```

Store this as a workflow called `reliably-plan.yaml`.

[More information](https://reliably.com/docs/deployment/#github-1)

The Reliably Plan Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| python-version | "3.11" | Run Reliably using this version of Python (3.11+) |
| github-token | | GitHub token with enough permissions to commit to the repository. Usually set it with `${{ secrets.GITHUB_TOKEN }}` |
| reliably-service-token | | Reliably token to authenticate with Reliably services. Usually set it with `${{ secrets.RELIABLY_SERVICE_TOKEN }}` |
| reliably-host | "app.reliably.com" | The Reliably host. Only useful if you run Reliably on your own host |
| org-id | | Reliably organization identifier for this run |
| plan-id | | Reliably plan identifier for this run |
| working-dir | | Repository relative directory where to run the plan from |
| reliably-experiment-extra | | A JSOn encoded object loaded by reliably to add to the results |


### Various notes

* The action automatically installs the Reliably CLI and many
  [Chaos Toolkit extensions](ctk) for you
* If you create a `bin` directory at the top of your repository, the
  action will automatically add it to the `PATH` if your plan requires access
  to specific utilities.
* The action downloads and provided the `aws-iam-authenticator` binary for you
  so you can authenticate against AWS EKS clusters


[ctk]: https://github.com/reliablyhq/actions/blob/main/pyproject.toml#L8

## Setup

This action is useful when you want to install the Reliably CLI and call one
of its commands.