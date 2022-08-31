# eth-json-rpc-infura

## Installation

`yarn add @metamask/eth-json-rpc-infura`

or

`npm install @metamask/eth-json-rpc-infura`

## Usage

### Creating a provider


```js
const { createInfuraProvider } = require('@metamask/eth-json-rpc-infura');
const EthQuery = require('eth-query');

const provider = createInfuraProvider({
  network: 'ropsten',
  projectId: 'abcdef1234567890',
});
const ethQuery = new EthQuery(provider);
ethQuery.blockNumber((err, result) => {
  if (err) {
    // do something with the error
  } else {
    // use the result in some way
  }
});
```

### Creating `json-rpc-engine` middleware

```js
const { createInfuraMiddleware } = require('@metamask/eth-json-rpc-infura');
const JsonRpcEngine = require('json-rpc-engine');

const engine = new JsonRpcEngine();
engine.push(
  createInfuraMiddleware({
    network: 'ropsten',
    projectId: 'abcdef1234567890',
  }),
);
const result = await engine.handle({
  id: 1,
  jsonrpc: '2.0',
  method: 'eth_blockNumber',
  params: [],
});
```

## Contributing

### Setup

- Install [Node.js](https://nodejs.org) version 12
  - If you are using [nvm](https://github.com/creationix/nvm#installation) (recommended) running `nvm use` will automatically choose the right node version for you.
- Install [Yarn v1](https://yarnpkg.com/en/docs/install)
- Run `yarn setup` to install dependencies and run any requried post-install scripts
  - **Warning:** Do not use the `yarn` / `yarn install` command directly. Use `yarn setup` instead. The normal install command will skip required post-install scripts, leaving your development environment in an invalid state.
