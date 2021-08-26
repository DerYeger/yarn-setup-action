<h1 align="center">Yarn Setup</h1>

<p align="center">
  GitHub Action for setting up a Yarn environment. Performs a checkout and installs dependencies.
</p>

## Features

- 🔽 Performs a **checkout** using [actions/checkout](https://github.com/actions/checkout).
- ⚒️ Sets up a **Node.js enviroment** using the specified `node_version`.
- 💽 **Caches** and retrieves `node_modules` for reduced execution time.
- ⌛ Runs `yarn install` if there was no cache hit.

## Usage

```yml
steps:
  - name: Yarn setup
    uses: DerYeger/yarn-setup-action@master
    with:
      node-version: 16
```

## License

[MIT](./LICENSE) - Copyright &copy; Jan Müller
