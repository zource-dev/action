# Node.js CI/CD workflow


### Usage example

```yaml
name: Example Usage

on: [push, pull_request]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Run CI/CD Pipeline
        uses: zource-dev/action@v1
        with:
          node_version: '20.x'
          github_token: ${{ secrets.GITHUB_TOKEN }}
          autoupdate: minor
          username: Github
          email: github@github.com
          npm_token: ${{ secrets.NPM_TOKEN }}
          codecov_token: ${{ secrets.CODECOV_TOKEN }}
          build: |
            pnpm codegen
            pnpm build
          test: |
            pnpm lint
            pnpm test
```

### License (MIT)[./LICENSE]
