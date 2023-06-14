# Reliably Plan Action

A [GitHub Action](https://github.com/features/actions) for running a Reliably
Plan using the [Reliably CLI](https://github.com/reliablyhq/cli).

You can use the Action as follows:

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

The Reliably Plan Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| python-version | "3.11" | Run Reliably using this version of Python (3.11+) |
| reliably-service-token | | Reliably token to authenticate with Reliably services |
| reliably-host | "app.reliably.com" | The Reliably host. Only useful if you run Reliably on your own host |
| org-id | | Reliably organization identifier for this run |
| plan-id | | Reliably plan identifier for this run |
| working-dir | | Repository relative directory where to run the plan from |
| reliably-experiment-extra | | A JSOn encoded object loaded by reliably to add to the results |


## Various notes

* The action automatically installs the Reliably CLI and many
  [Chaos Toolkit extensions](ctk) for you
* If you create a `bin` directory at the top of your repository, the
  action will automatically add it to the `PATH` if your plan requires access
  to specific utilities.
* The action downloads and provided the `aws-iam-authenticator` binary for you
  so you can authenticate against AWS EKS clusters


[ctk]: https://github.com/reliablyhq/actions/blob/main/pyproject.toml#L8
