# Jina AI Executor CI/CD Workflows

Call these workflows remotely from your Executor's repo

## Add via workflow template
1. Follow the instructions at [Jina Workflow Templates](https://github.com/jina-ai/.github)

## Add via copy-paste

1. add `.github/workflows/cd.yml` with the following:

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
    uses: jina-ai/workflows-executors/.github/workflows/cd.yml@master
    with:
      event_name: ${{ github.event_name }}
    secrets:
      jinahub_token: ${{ secrets.JINAHUB_TOKEN }}
```

2. add `.github/workflows/ci.yml` with the following:

```yaml
name: CI

on: [pull_request]

jobs:
  call-external:
    uses: jina-ai/workflows-executors/.github/workflows/ci.yml@master
```

3. [optional] add `.github/workflows/ci-gpu.yml` with the following:

```yaml
name: CI-GPU

on: [pull_request]

jobs:
  call-external:
    uses: jina-ai/workflows-executors/.github/workflows/ci-gpu.yml@master
```
