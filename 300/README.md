# 300 - Building Our Application

## 100 - Using uv in a GitHub Actions workflow

Below is an example of using **uv** in a GitHub Actions workflow:

``` yaml
name: Do Something With Python

on:
  push:

permissions:
  contents: read

jobs:
  tests:
    runs-on: ubuntu-latest
    services:
      docker:
        image: docker:dind
        options: --privileged --shm-size=2g
    steps:
      - name: Checkout
        uses: actions/checkout@de0fac2e4500dabe0009e67214ff5f5447ce83dd # v6.0.2
      - name: Install uv
        uses: astral-sh/setup-uv@803947b9bd8e9f986429fa0c5a41c367cd732b41 # v7.2.1
#      - name: Miscellaneous
#        uses: ???
      - name: Do something with uv, like running a pytest from directory /tests/unit/
        run: |
          uv run --frozen pytest tests/unit -vv
```
.github/workflows/unit-tests.yaml

In the above example, one would have the following supporting documents also:

```
tests
  |- unit
       |- __init__.py
       |- test_do_something.py
```

This GitHub Actions workflow is triggered when a Commit is attempted to be pushed.

Should you want to manually trigger the GitHub Actions workflow, follow [Manually running a workflow](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/manually-run-a-workflow).
