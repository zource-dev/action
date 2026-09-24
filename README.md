# Node.js CI/CD workflow


### npm publishing

Configure the npm package to trust the caller repository's `upgrade.yml` workflow and allow direct publishing. The caller job needs `contents: write` for the Git pushes and `id-token: write` for npm publishing. No npm token is needed.

For an existing version tag that was not published, manually run the caller workflow with `release_tag` set to that tag. The action verifies the tag against `package.json` and the release branch, then builds, tests, and publishes without creating a commit or tag.

### Usage example

```yaml
name: Autoupdate

on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:
    inputs:
      release_tag:
        description: 'Existing version tag to publish'
        required: true
        type: string

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      id-token: write
    steps:
      - name: Run CI/CD Pipeline
        uses: zource-dev/action@v2
        with:
          release_tag: ${{ inputs.release_tag }}
          node_version: '24.14.1'
          github_token: ${{ secrets.GITHUB_TOKEN }}
          autoupdate: minor
          username: Github
          email: github@github.com
          codecov_token: ${{ secrets.CODECOV_TOKEN }}
          build: |
            pnpm codegen
            pnpm build
          test: |
            pnpm lint
            pnpm test
```

### License (MIT)[./LICENSE]
