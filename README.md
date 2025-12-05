# Kubeletto Actions

This repository contains reusable GitHub Actions workflows for the Kubeletto platform.

## Workflows

### Reusable Deploy (`reusable-deploy.yml`)

This workflow handles the build and deployment process for Kubeletto projects. It is designed to be called by a "thin wrapper" workflow in the user's repository.

**Inputs:**
- `project_id` (required): The Kubeletto Project ID.
- `api_url` (optional): The Kubeletto Platform API URL. Defaults to `https://api.kubeletto.app`.
- `dockerfile_path` (optional): Path to the Dockerfile. Defaults to `Dockerfile`.
- `build_context` (optional): Build context directory. Defaults to `.`.

**Secrets:**
- `api_key` (required): The Kubeletto API Key.

## Usage

To use this workflow in a user's repository:

```yaml
name: Deploy to Kubeletto

on:
  push:
    branches: [main]

jobs:
  deploy:
    uses: kubeletto/actions/.github/workflows/reusable-deploy.yml@v1
    with:
      project_id: ${{ vars.KUBELETTO_PROJECT_ID }}
    secrets:
      api_key: ${{ secrets.KUBELETTO_API_KEY }}
```

## Publishing

1. Create a public repository named `actions` under the `kubeletto` organization (or your user account).
2. Push this code to the repository.
3. Create a release tagged `v1` so that users can pin to a stable version.
