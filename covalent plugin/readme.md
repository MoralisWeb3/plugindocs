# Moralis Covalent Plugin

This plugin enables interaction with the Covalent API (https://www.covalenthq.com/). <br>

## Get started

Grab a free api key here: https://www.covalenthq.com/

## Optional parameters

When possible, this plugin supports pagination following the interface below. </br>

```ts
interface ApiPagination {
  pageNumber?: number;
  pageSize?: number;
}
```

The parameter `pageNumber` is set to `0` by default. </br>
The parameter `pageSize` is set to `100` by default. </br>

This plugins also supports `quoteCurrency`. </br>
The parameter `quoteCurrency` is set to `USD` by default. </br>

## Endpoints

### Get block

Description: Given chain id and block height return the block.

```ts
interface GetBlockDto {
  chainId: number;
  blockHeight: string;
}
```

```js
await Moralis.Plugins.covalent.getBlock(GetBlockDto)
```
