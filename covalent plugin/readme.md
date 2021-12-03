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

</br>

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

</br>

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

</br>

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

</br>

### Get Chains

Description: Returns a list of all chains.

```ts
interface GetChainsDto {}
```

```ts
await Moralis.Plugins.covalent.getChains(GetChainsDto);
```

</br>

### Get Chain Statuses

Description: Returns a list of all chain statuses.

```ts
interface GetChainStatusesDto {}
```

```ts
await Moralis.Plugins.covalent.getChainsStatuses(GetChainStatusesDto);
```

</br>

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

</br>

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

</br>

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

</br>

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

</br>

### Get log events by topic

Description: Given chain id and topic return a paginated list of decoded log events with one or more topic hashes separated by a comma.

```ts
interface GetLogEventsByTopicDto {
  chainId: number;
  topic: Topic;
  endBlock: string;
  secondaryTopic?: Topic;
  startBlock?: string;
  address?: Address;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getTokenHoldersByTopic(GetLogEventsByTopicDto);
```

</br>

### Get NFT Token IDs for contract

Description: Given chain id and contract address, return a list of all token IDs for the NFT contract on the blockchain.

```ts
interface GetNFTTokenIDsForContractDto {
  chainId: number;
  contractAddress: Address;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getNftTokenIdForContract(GetNFTTokenIDsForContractDto);
```

</br>

### Get NFT transactions for contract

Description: Given chain id, contract address and token id, return a list of transactions.

```ts
interface GetNFTTransactionsForContractDto {
  chainId: number;
  contractAddress: Address;
  tokenId: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getNftTransactionsForContract(GetNFTTransactionsForContractDto);
```

</br>


### Get NFT external metadata for contract

Description: Given chain id, contract address and token id, fetch and return the external metadata. Both ERC721 as well as ERC1155 standards are supported.

```ts
interface GetNFTExternalMetaForContractDto {
  chainId: number;
  contractAddress: Address;
  tokenId: string;
}
```

```js
await Moralis.Plugins.covalent.getNftExternalMetadataForContract(GetNFTExternalMetaForContractDto);
```

</br>


### Get token balances for address

Description: Given chain id and wallet address return current token balances along with their spot prices.

```ts
interface GetTokenBalancesForAddressDto {
  chainId: number;
  address: Address;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getTokenBalancesForAddress(GetTokenBalancesForAddressDto);
```

</br>

### Get token holders as of any block height

Description: Given chain id and wallet address, return a paginated list of token holders. If block height is omitted, the latest block is used.

```ts
interface GetBlockTokenHoldersDto {
  chainId: number;
  contractAddress: Address;
  blockHeight: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getBlockTokenHolders(GetBlockTokenHoldersDto);
```

</br>

### Get transactions

Description: Given chain id and transaction hash return return the transaction data with their decoded event logs.

```ts
interface GetTransactionDto {
  chainId: number;
  transactionHash: TransactionHash;
}
```

```js
await Moralis.Plugins.covalent.getTransaction(GetTransactionDto);
```

</br>

### Get transactions for address

Description: Given chain id and wallet address return all transactions along with their decoded log events. This endpoint does a deep-crawl of the blockchain to retrieve all kinds of transactions that references the addressincluding indexed topics within the event logs.

```ts
interface GetTransactionsForAddressDto {
  chainId: number;
  address: Address;
  quoteCurrency?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getTransactionsForAddress(GetTransactionsForAddressDto);
```
