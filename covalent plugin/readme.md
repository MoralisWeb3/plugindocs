# Moralis Covalent Plugin

This plugin enables interaction with the Covalent API (https://www.covalenthq.com/). <br>

## Get started

Grab a free api key here: https://www.covalenthq.com/

## Supported Protocols

- UniSwap
- SushiSwap
- PancakeSwap
- Aave
- Balancer
- Compound
- Curve
- Balancer
- Farming Stats

## Optional parameters

When possible, this plugin supports pagination following the interface below. <br>

```ts
interface ApiPagination {
  pageNumber?: number;
  pageSize?: number;
}
```

The parameter `pageNumber` is set to `0` by default. <br>
The parameter `pageSize` is set to `100` by default. <br>

This plugins also supports `quoteCurrency`. <br>
The parameter `quoteCurrency` is set to `USD` by default. <br>

Last but not least the plugin also supports the `swaps: boolean` parameter when possibile <br>
You will see this parameter available in endpoints that return exchange liquidity transactions. <br>
Swaps is set to `false` by default.

## Uniswap Endpoints <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Uniswap_Logo.svg/1026px-Uniswap_Logo.svg.png" width="40"/>

- getUniswapAssets <br>
  <b>Description:</b> Returns a paginated list of Uniswap pools sorted by exchange volume.<br>

```ts
await Moralis.Plugins.covalent.getUniswapAssets({
  tickers: 'BTC',
});
```

- getUniswapAddressBalances <br>
  <b>Description:</b> Gets Uniswap v2 address exchange balances.<br>

```ts
await Moralis.Plugins.covalent.getUniswapAddressBalances({
  address: '0xccf1c3f73b04bfc1874f08197b69fe5edaaba73d',
});
```

- getUniswapAddressLiquidityTransactions <br>
  <b>Description:</b> Gets Uniswap v2 address exchange liquidity transactions.<br>

  `Support swaps: true`

```ts
await Moralis.Plugins.covalent.getUniswapAddressLiquidityTransactions({
  address: '0xccf1c3f73b04bfc1874f08197b69fe5edaaba73d',
});
```

## Pancakeswap Endpoints <img src="https://github.com/pancakeswap/pancake-frontend/blob/develop/public/logo.png?raw=true" width="40"/>

- getPancackeAssets <br>
  <b>Description:</b> Returns a paginated list of Pancake V2 pools sorted by exchange volume. Only pools with swaps in the last 24 hours are included.<br>

```ts
await Moralis.Plugins.covalent.getPancackeAssets({
  tickers: 'BNB',
  // addresses: '' If addresses (a comma separated list) is present, only return the pools that contain these contracts.
});
```

- getPancackePool <br>
  <b>Description:</b> Returns detailed pool information for the specified pool address.<br>

```ts
await Moralis.Plugins.covalent.getPancackePool({
  address: '0xcad7019d6d84a3294b0494aef02e73bd0f2572eb',
});
```

- getPancackeUserBalance <br>
  <b>Description:</b> Gets Pancakeswap V2 address exchange balances.<br>

```ts
await Moralis.Plugins.covalent.getPancackeAddressBalance({
  address: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
});
```

## Sushiswap Endpoints <img src="https://github.com/sushiswap/sushiswap-interface/blob/canary/public/logo.png?raw=true" width="40"/>

In order to query Sushiswap related endpoints, you must provide a chainId parameter. <br>
The following chain IDs are available: <br>
['1', '137', '80001', '56', '43114', '43113', '250']

- getSushiswapAssets <br>
  <b>Description:</b> Returns a paginated list of Sushiswap pools sorted by exchange volume.<br>

```ts
await Moralis.Plugins.covalent.getSushiswapAssets({
  chainId: '1',
  tickers: 'BTC',
});
```

- getSushiswapAddressBalance <br>
  <b>Description:</b> Get Sushiswap address exchange balances.<br>

```ts
await Moralis.Plugins.covalent.getSushiswapAddressBalance({
  chainId: '1',
  address: '0xe55c3e83852429334a986b265d03b879a3d188ac',
});
```

- getSushiswapAddressLiquidityTransactions <br>
  <b>Description:</b> Gets Sushiswap address exchange liquidity transactions.<br>

  `Support swaps: true`

```ts
await Moralis.Plugins.covalent.getSushiswapAddressLiquidityTransactions({
  chainId: '1',
  address: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
});
```

## Aave Endpoints <img src="https://raw.githubusercontent.com/aave/aave-ui/bf9b52643fdeefc53a6ebf179efd904d86505568/public/aave.svg" width="40"/>

- getAaveAssets <br>
  <b>Description:</b> Returns a paginated list of Aave pools sorted by exchange volume.<br>

```ts
await Moralis.Plugins.covalent.getAaveAssets();
```

- getAaveAddressBalance <br>
  <b>Description:</b> Gets Aave address exchange balances.<br>

```ts
await Moralis.Plugins.covalent.getAaveAddressBalance({
  address: '0xb53c1a33016b2dc2ff3653530bff1848a515c8c5',
});
```

## Compound Endpoints <img src="https://raw.githubusercontent.com/compound-finance/compound-components/9a9ff55e565baf434e4013d0de971557596c0613/src/public/assets/asset_COMP.svg" width="40"/>

- getCompoundAssets <br>
  <b>Description:</b> Get Compound network assets.<br>

```ts
await Moralis.Plugins.covalent.getCompoundAssets();
```

- getCompoundAddressBalances <br>
  <b>Description:</b> Get Compound address balances.<br>

```ts
await Moralis.Plugins.covalent.getCompoundAddressBalances({
  address: '0xf5dce57282a584d2746faf1593d3121fcac444dc',
});
```

- getCompoundAddressActivity <br>
  <b>Description:</b> Get Compound address activity.<br>

```ts
await Moralis.Plugins.covalent.getCompoundAddressActivity({
  address: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
});
```

## Curve Endpoints <img src="https://image.pngaaa.com/550/5986550-middle.png" width="40"/>

- getCurveAddressBalances <br>
  <b>Description:</b> Get Curve address balances.<br>

```ts
await Moralis.Plugins.covalent.getCurveAddressBalances({
  address: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
});
```

## Balancer Endpoints <img src="https://avatars.githubusercontent.com/u/48451921?s=200&v=4" width="40"/>

- getBalancerAddressBalances <br>
  <b>Description:</b> Get Balancer address balances.<br>

```ts
await Moralis.Plugins.covalent.getBalancerAddressBalances({
  address: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
});
```

## Farming stats Endpoints

- getBalancerAddressBalances <br>
  <b>Description:</b> Get farming positions on Uniswap, Sushiswap, and Harvest.<br>

```ts
await Moralis.Plugins.covalent.getFarmingStats({
  address: '0xfcade2c82f8f1f53ff6b2463c3470126d27f3f3b',
});
```
