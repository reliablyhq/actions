# Reliably Setup Action

A [GitHub Action](https://github.com/features/actions) for installing
[Reliably CLI](https://github.com/reliablyhq/cli) within your workflow,
so that the command is directly available in a job step.

You can use the Action as follows:

```yaml
name: Install Reliably CLI example
on: push
jobs:
  setup-reliably:
    runs-on: ubuntu-22.04
    steps:
    - uses: reliablyhq/actions/setup@v1
```

The Reliably Setup Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| reliably-version | 0.1.0 | Install a specific version of Reliably |
