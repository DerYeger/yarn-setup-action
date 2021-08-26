# Yarn Setup

> GitHub Action for setting up a Yarn environment. Caches dependencies for reduced execution times.

## Features

- 🔽 Performs a **checkout** using [actions/checkout](https://github.com/actions/checkout).
- ⚒️ Sets up a **Node.js environment** using the specified `node-version` with [actions/setup-node](https://github.com/actions/setup-node).
- 💽 **Caches** and retrieves `node_modules` for reduced execution time. Based on [actions/cache](https://github.com/actions/cache).
- ⌛ Runs `yarn install` with the cached `node_modules`.

## Usage

```yml
steps:
  - name: Yarn setup
    uses: DerYeger/yarn-setup-action@master
    with:
      node-version: 16
```

### Inputs

- `node-version`: The version of Node.js that will be used.

### Outputs

- `cache-hit`: Indicates a cache hit.

### Example

Splitting long jobs into multiple allows for parallel execution and thus faster workflow execution.
However, every job requires its own setup and environment initialization.
This Action allows for easy installation of dependencies while maintaining fast execution times thanks to built-in caching.

The following example workflow demonstrates parallel execution of three jobs (`build`, `lint` and `test`), which run in parallel.
They all depend on the `prepare` job, which either validates that dependencies are cached or installs (then caches) them itself.
This setup ensures that each of the following jobs has access to Node.js and dependencies with minimal overhead (usually in the order of 3 to 5 seconds, depending on the project and `postinstall` setup).

```yml
name: CI

on: [pull_request, push]

jobs:
  prepare:
    name: Prepare
    runs-on: ubuntu-latest
    steps:
      - uses: DerYeger/yarn-setup-action@master
        with:
          node-version: 16
  build:
    name: Build
    runs-on: ubuntu-latest
    needs: prepare
    steps:
      - uses: DerYeger/yarn-setup-action@master
        with:
          node-version: 16
      - run: yarn build
  lint:
    name: Lint
    runs-on: ubuntu-latest
    needs: prepare
    steps:
      - uses: DerYeger/yarn-setup-action@master
        with:
          node-version: 16
      - run: yarn lint
  test:
    name: Test
    runs-on: ubuntu-latest
    needs: prepare
    steps:
      - uses: DerYeger/yarn-setup-action@master
        with:
          node-version: 16
      - run: yarn test
```

## License

[MIT](./LICENSE) - Copyright &copy; Jan Müller
