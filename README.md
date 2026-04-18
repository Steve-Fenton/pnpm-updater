# PNPM Updater GitHub Action

This GitHub Action automatically updates dependencies using `pnpm` and creates a pull request with the changes.

## Usage

### Simple Usage (Defaults)

```yaml
name: Update Dependencies

on:
  schedule:
    - cron: '0 0 * * 1' # Every Monday at 00:00 UTC
  workflow_dispatch:

permissions:
  contents: write
  pull-requests: write

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Steve-Fenton/pnpm-updater@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

### Advanced Usage (Custom versions and script)

```yaml
name: Update Dependencies

on:
  schedule:
    - cron: '0 0 * * 1' # Every Monday at 00:00 UTC
  workflow_dispatch:

permissions:
  contents: write
  pull-requests: write

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Steve-Fenton/pnpm-updater@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          node_version: '24'
          pnpm_version: '10.22.0'
          update_script: 'pnpm refresh'
```

## Inputs

| Input           | Description                               | Required | Default                  |
| --------------- | ----------------------------------------- | -------- | ------------------------ |
| `github_token`  | GitHub token for creating pull requests   | Yes      | `${{ github.token }}`    |
| `node_version`  | The version of Node.js to use             | No       | `'latest'`               |
| `pnpm_version`  | The version of pnpm to use                | No       | `'latest'`               |
| `update_script` | The command to run to update dependencies | No       | `'pnpm update --latest'` |

## License

MIT

## Maintenance

To trigger different types of version bumps, use the following hashtags in your commit message to `main`:

- `#major` -> v2.0.0
- `#minor` -> v1.1.0
- `#patch` -> v1.0.2 (Default)
