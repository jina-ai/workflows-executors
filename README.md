# Jina AI Executor CI/CD Workflows

Call these workflows remotely from your Executor's repo

1. Add your secret as `EXECUTOR_SECRET` (or whatever you want to call it)
2. add `.github/workflows/cd.yml` with the following:

```yaml
name: CD

on:
  push:
    branches:
      - main
  release:
    types:
      - created
  workflow_dispatch:
  # pull_request:
  # uncomment the above to test CD in a PR

jobs:
  call-external:
    uses: jina-ai/.github/.github/workflows/cd.yml@master
    with:
      event_name: ${{ github.event_name }}
    secrets:
      secret: ${{ secrets.EXECUTOR_SECRET }}
```

3. add `.github/workflows/ci.yml` with the following:

```yaml
name: CI

on: [pull_request]

jobs:
  call-external:
    uses: jina-ai/.github/.github/workflows/ci.yml@master
```
