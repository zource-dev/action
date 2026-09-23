# Node.js CI/CD workflow


### npm publishing

Configure the npm package to trust the caller repository's `upgrade.yml` workflow and allow direct publishing. The caller job needs `contents: write` for the Git pushes and `id-token: write` for npm publishing. No npm token is needed.

### Usage example

```yaml
name: Autoupdate

on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      id-token: write
    steps:
      - name: Run CI/CD Pipeline
        uses: zource-dev/action@31474013f2af73d421da2a009e0f7af6777336ae
        with:
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
