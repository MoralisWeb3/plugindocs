# Moralis OpenSea Plugin

This plugin enables interaction with OpenSea.

## Supported chains

This plugins works with 2 different blockchains:

- Ethereum Mainnet ('mainnet')
- Ethereum Rinkeby ('testnet')

## Supported tokens

- ERC721
- ERC1155

# Utils

Useful endpoints in this plugin:

## Get asset

```js
const asset = await Moralis.Plugins.opensea.getAsset({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
});
console.log(asset);
```

## Get orders

```js
const orders = await Moralis.Plugins.opensea.getOrders({
  network: network,
  tokenAddress: tokenAddress,
  tokenId: tokenId,
  orderSide: side,
  page: 1, // pagination shows 25 order each page
});
console.log(orders);
```

# Sellers

Sell an item on OpenSea involves these requirements:

- The `seller` needs to have a proxy contract deployed
- The `seller` has to approve the proxy contract

## Verify seller approvals

```js
const { proxyContract, approveForAll } = await Moralis.Plugins.opensea.checkSellerApprovals({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
});
```

`proxyContract` and `approveForAll` are two booleans.
They should both be `true` in order to post a new sell order, however if both or one of them is `false`, you can proceed as follow.

## Deploy a proxy contract

If `checkSellerApprovals()` returns `"proxyContract": false` the users has to deploy a proxy. <br>
<u> This is a one-time operation in order to be able to sell on OpenSea. </u>

```js
await Moralis.Plugins.opensea.deployProxy({
  network: 'testnet',
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
});
```

The Moralis SDK will trigger a transaction that deploys the proxy contract.

## Approve ERC721 / 1155

If `checkSellerApprovals()` returns `"approveForAll": false` the user has to approve his proxy contract to spend ERC 721 / 1155 tokens.

```js
await Moralis.Plugins.opensea.approveForAll({
  network: 'testnet',
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
});
```

## Create a sell order

Once the seller approvals have been granted, the user can place a new sell order. <br>
Create a new sell order requires two steps:

- Sign the order
- Post the order

### Sign the order

You can sign a sell order as follow:

```js
const result = await Moralis.Plugins.opensea.signSellOrder({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
  tokenType: 'ERC1155',
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
  asset: {
    tokenId: '0',
    tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
    schemaName: 'ERC1155',
  },
  startAmount: 1,
  endAmount: 0.5, // set it equal to `startAmount` to fix price (not declining)
  expirationTime: 10000000000, // do not set if [not declining]
  // paymentTokenAddress:, //set if you want to use another erc !== WETH
});
```

Once the sell order has been signed by the user web3 provider (such as MetaMask) the `result` will contain useful data, necessary to post the sell order.

### Post the order

You can post a sell order as follow:

```js
await Moralis.Plugins.opensea.postOrder({
  message: result._payload.data.hash,
  signature: result.response,
  orderSide: 1, // Sell
});
```

The approvals and sell order creation can be merged in one function, to offer the best user experience

```js
async function signSellOrder() {
  // Verify seller approvals
  const { proxyContract, approveForAll } = await Moralis.Plugins.opensea.checkSellerApprovals({
    network: 'testnet',
    tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
    userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
  });

  if (!proxyContract) {
    await Moralis.Plugins.opensea.deployProxy({
      network: 'testnet',
      userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
    });
  }
  if (!approveForAll) {
    await Moralis.Plugins.opensea.approveForAll({
      network: 'testnet',
      userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
      tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
    });
  }

  const result = await Moralis.Plugins.opensea.signSellOrder({
    network: 'testnet',
    tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
    tokenId: '0',
    tokenType: 'ERC1155',
    userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
    asset: {
      tokenId: '0',
      tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
      schemaName: 'ERC1155',
    },
    startAmount: 1,
    endAmount: 0.5, // set to equal to startAmount to fix price (not declining)
    expirationTime: 10000000000, // do not set if [not declining]
    // paymentTokenAddress:  //set if you want to use another erc !== WETH
  });

  const isPosted = await Moralis.Plugins.opensea.postOrder({
    message: result._payload.data.hash,
    signature: result.response,
    orderSide: 1,
  });
  if (isPosted) alert('The sell order has been posted!');
}
```

## Create a buy order

Create a new buy order requires two steps:

- Sign the order
- Post the order

It also requires the `buyer` to approve ERC20 Opensea so that it can take ERC20 tokens from the `buyer`.
If this is necessary, the Moralis SDK will automatically trigger an `approve` transaction when the `buyer` tries to place a buy order.

### Sign the order

You can sign a buy order as follow:

```js
const result = await Moralis.Plugins.opensea.signBuyOrder({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
  amount: 1,
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
  tokenType: 'ERC1155',
});
```

Once the buy order has been signed by the user web3 provider (such as MetaMask) the `result` will contain useful data, necessary to post the sell order.

### Post the order

You can post a buy order as follow:

```js
await Moralis.Plugins.opensea.postOrder({
  message: result._payload.sign.data.hash,
  signature: result.response,
  orderSide: 0,
});
```

The buy order sign and post can be merged in one function, to offer the best user experience

```js
async function signBuyOrder() {
  const result = await Moralis.Plugins.opensea.signBuyOrder({
    network: 'testnet',
    tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
    tokenId: '0',
    amount: 1,
    userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475',
    tokenType: 'ERC1155',
  });
  const isPosted = await Moralis.Plugins.opensea.postOrder({
    message: result._payload.sign.data.hash,
    signature: result.response,
    orderSide: 0,
  });
  if (isPosted) alert('The buy order has been posted!');
}
```

### Fulfill a buy order

A `seller` can fulfill any open buy order.
Orders on a single asset can be retrieved by using `getOrders()`.

```js
await Moralis.Plugins.opensea.fulfillOrder({
  network: 'testnet',
  userAddress: '0x730fe9Fa053BB19841D1C2410f5f871F39c8C475', //seller in this case
  order: Order,
});
```
