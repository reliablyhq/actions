# Reliably Agent Action

A [GitHub Action](https://github.com/features/actions) for installing
[Reliably CLI](https://github.com/reliablyhq/cli) and run its agent in your
workflow.

You can use the Action as follows:

```yaml
name: Run the Reliably Agent in your workflow every minute
on:
  schedule:
    - cron:  '1 * * * *'
  
jobs:
  setup-reliably:
    runs-on: ubuntu-22.04
    steps:
      - name: Checkout source code
        uses: actions/checkout@v3
      - name: Download and install Reliably CLI
        uses: reliablyhq/actions/agent@v1
```

The Reliably Agent Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| python-version | 3.10 | Run Reliably using this version of Python (3.10+) |
| reliably-version | 0.1.0 | Install a specific version of Reliably |
| reliably-config-path | ./.reliably.toml | Reliably configuration path in the repository |
