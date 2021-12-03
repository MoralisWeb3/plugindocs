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
await Moralis.Plugins.covalent.getBlock(GetBlockDto);
```

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
await Moralis.Plugins.covalent.getNftTokenIdForContract(
  GetNFTTokenIDsForContractDto
);
```

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
await Moralis.Plugins.covalent.getNftTransactionsForContract(
  GetNFTTransactionsForContractDto
);
```

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
await Moralis.Plugins.covalent.getNftExternalMetadataForContract(
  GetNFTExternalMetaForContractDto
);
```

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
await Moralis.Plugins.covalent.getTokenBalancesForAddress(
  GetTokenBalancesForAddressDto
);
```

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
await Moralis.Plugins.covalent.getTransactionsForAddress(
  GetTransactionsForAddressDto
);
```
