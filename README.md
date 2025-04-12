# Node.js Dependencies Cache Setup Action

This GitHub Action automates the setup of Node.js and efficiently manages dependency caching using Yarn. It helps reduce workflow execution time by caching and restoring node_modules based on your yarn.lock and package.json files.

## Features

- 📦 Automatic Node.js setup using .nvmrc file
- 🚀 Smart caching of node_modules and Yarn state
- ⚡ Optimized dependency installation
- 🔄 Automatic cache updates on dependency changes

## Usage

Add this action to your workflow:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: Act-Aks/cached-setup@v1
```

## Prerequisites

- A `.nvmrc` file in your repository specifying the Node.js version
- `yarn.lock` and `package.json` files for dependency management

## How it works

1. Sets up Node.js based on your .nvmrc file
2. Attempts to restore cached dependencies
3. Installs dependencies if cache miss occurs
4. Saves the new cache for future workflows

## Cache Keys

The action uses the following cache key format:

```
{runner.os}-yarn-{hash of yarn.lock}-{hash of package.json files}
```

Fallback keys:

```
{runner.os}-yarn-{hash of yarn.lock}
{runner.os}-yarn-
```

## Example Workflow

```yaml
name: Build and Test

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Act-Aks/cached-setup@v1
      - run: yarn build
      - run: yarn test
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Act-Aks
