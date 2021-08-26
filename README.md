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

## License

[MIT](./LICENSE) - Copyright &copy; Jan Müller
