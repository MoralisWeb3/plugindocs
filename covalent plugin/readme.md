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

```ts
await Moralis.Plugins.covalent.getBlock(GetBlockDto);
```

### Get All Contract Metadata

Description: Given chain id, return a list of all contracts on a blockchain along with their metadata.

```ts
interface GetAllContractMetaDto {
  chainId: number;
  pageNumber?: number;
  pageSize?: number;
}
```

```ts
await Moralis.Plugins.covalent.getAllContractMetadata(GetAllContractMetaDto);
```

### Get Block Heights

Description: Given chain id, start date, end date return all the block height(s) of a particular chain within a date range.

```ts
interface GetBlockHeightsDto {
  chainId: number;
  blockHeight: string;
  startDate: string;
  endDate: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```ts
await Moralis.Plugins.covalent.getBlockHeights(GetBlockHeightsDto);
```

### Get Chains

Description: Returns a list of all chains.

```ts
interface GetChainsDto {}
```

```ts
await Moralis.Plugins.covalent.getChains(GetChainsDto);
```

### Get Chain Statuses

Description: Returns a list of all chain statuses.

```ts
interface GetChainStatusesDto {}
```

```ts
await Moralis.Plugins.covalent.getChainsStatuses(GetChainStatusesDto);
```

### Get Changes In Token Holders

Description: Given chain id and wallet address, return a paginated list of token holders and their current/historical balances, where the token balance of the holder changes between starting block and ending block.

```ts
interface GetChangesInTokenHoldersDto {
  chainId: number;
  address: Address;
  startingBlock: string;
  endingBlock: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```ts
await Moralis.Plugins.covalent.getChangesInTokenHolerBetweenBlockHeights(GetChangesinTokenHoldersDto);
```

### Get Erc20 Token Transactions For Address

Description: Given chain id user address and transaction hash return all ERC20 token contract transfers along with their historical prices at the time of their transfer.

```ts
interface GetErc20TokenTransactionsForAddressDto {
  chainId: number;
  address: Address;
  tokenAddress: Address;
  quoteCurrency?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```ts
await Moralis.Plugins.covalent.getErc20TokenTransfersForAddress(GetErc20TokenTransactionsForAddressDto);
```

### Get Historical Portfolio Value Over Time

Description: Given chain id and wallet address return wallet value for the last 30 days at 24 hour interval timestamps.

```ts
interface GetHistoricalPortfolioValueOverTimeDto {
  chainId: number;
  address: Address;
  quoteCurrency?: string;
}
```

```ts
await Moralis.Plugins.covalent.getHistoricalPortfolioValueOverTime(GetHistoricalPortfolioValueOverTimeDto);
```

### Get Log Events By Contract Address

Description: Given chain id, and contract address, return a paginated list of decoded log events emitted by a particular smart contract.

```ts
interface GetLogEventsByContractAddressDto {
  chainId: number;
  contractAddress: Address;
  startingBlock: string;
  endingBlock: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```ts
await Moralis.Plugins.covalent.getLogEventsByContractAddress(GetLogEventsByContractAddressDto);
```
