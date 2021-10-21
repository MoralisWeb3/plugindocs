# Moralis OpenSea Plugin

This plugin enables interaction with OpenSea. <br>
Buy and sell items on OpenSea involves multiple steps, but the plugin together with the Moralis SDK take care of everything. <br>

## Supported chains

This plugins works with 2 different blockchains:

- Ethereum Mainnet ('mainnet')
- Ethereum Rinkeby ('testnet')

## Supported tokens

- ERC721
- ERC1155

# SDK

Import the Moralis SDK in your project.

```html
<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
<script src="https://npmcdn.com/moralis@latest/dist/moralis.js"></script>
```

# Utils

## Get asset

```js
await Moralis.Plugins.opensea.getAsset({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
});
```

## Get orders

```js
await Moralis.Plugins.opensea.getOrders({
  network: network,
  tokenAddress: tokenAddress,
  tokenId: tokenId,
  orderSide: side,
  page: 1, // pagination shows 20 orders each page
});
```

# Sellers

To sell an asset, call `createSellOrder`. <br>
You can do a fixed-price listing, where `startAmount` is equal to `endAmount`, or a declining Dutch auction, where `endAmount` is lower and the price declines until `expirationTime` is hit.

```js
// Expire this auction one day from now.
// Note that we convert from the JavaScript timestamp (milliseconds):
const expirationTime = Math.round(Date.now() / 1000 + 60 * 60 * 24);

await Moralis.Plugins.opensea.createSellOrder({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
  tokenType: 'ERC1155',
  userAddress: '0x7fB3948c368A943e4EFE848F251E4f254dA1a2b2',
  startAmount: 1,
  endAmount: 1,
  // expirationTime: expirationTime, Only set if you startAmount > endAmount
});
```

# Buyers

You can create a buy order by calling `createBuyOrder`. <br>
Buy orders must be placed using wrapped ETH or an ERC-20 token.

```js
await Moralis.Plugins.opensea.createBuyOrder({
  network: 'testnet',
  tokenAddress: '0xdbe8143c3996c87ecd639ebba5d13b84f56855c2',
  tokenId: '0',
  tokenType: 'ERC1155',
  amount: 0.5,
  userAddress: '0x6057b9bA4BAe35B8128685f342a8e1016b77046d',
  paymentTokenAddress: '0xc778417e063141139fce010982780140aa0cd5ab',
});
```

# Fulfill orders

To buy an item you need to fulfill a sell order. <br>
To sell an item you need to fulfill a buy order. <br>

You can fetch orders for a given token by using the `getOrder` endpoint described above, then use it as parameter in `fulfillOrder`.

```js
await Moralis.Plugins.opensea.fulfillOrder({
  network: 'testnet',
  userAddress: '0x6057b9bA4BAe35B8128685f342a8e1016b77046d',
  order: {},
});
```

# Cancel orders

You can cancel an order by calling `cancelOrder`. <br>
You can fetch orders for a given token by using the `getOrder` endpoint described above, then use it as parameter in `fulfillOrder`.

```js
await Moralis.Plugins.opensea.cancelOrder({
  network: 'testnet',
  userAddress: '0x6057b9bA4BAe35B8128685f342a8e1016b77046d',
  order: {},
});
```
