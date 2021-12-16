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

```js
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

```js
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

```js
await Moralis.Plugins.covalent.getBlockHeights(GetBlockHeightsDto);
```

</br>

### Get Chains

Description: Returns a list of all chains.

```ts
interface GetChainsDto {}
```

```js
await Moralis.Plugins.covalent.getChains(GetChainsDto);
```

</br>

### Get Chain Statuses

Description: Returns a list of all chain statuses.

```ts
interface GetChainStatusesDto {}
```

```js
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

```js
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

```js
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

```js
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

```js
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

</br>

## Uniswap Endpoints <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Uniswap_Logo.svg/1026px-Uniswap_Logo.svg.png" width="40"/>

</br>

### Get Uniswap v2 pools

Description: Return pool information across all Uniswap V2 pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetUniswapV2PoolsDto {
  tickers?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV2Pools(GetUniswapV2PoolsDto);
```

</br>

### Get Uniswap V2 Address Exchange Balances

Description: Given an address, return pool balances across all Uniswap v2 pools and their quote rates.

```ts
interface GetUniswapV2AddressExchangeBalancesDto {
  address: string;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV2AddressExchangeBalances(GetUniswapV2AddressExchangeBalancesDto);
```

</br>

### Get Uniswap V2 Address Liquidity Transactions

Description: Given an address, return a list of liquidity additions and removals. Optionally include swaps as well if requested.

```ts
interface GetUniswapV2AddressLiquidityTransactionsDto {
  address: string;
  swaps?: boolean;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV2AddressLiquidityTransactions(GetUniswapV2AddressLiquidityTransactionsDto);
```

</br>

### Get Uniswap V3 Pools

Description: Return pool information across all Uniswap V3 pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetUniswapV3PoolsDto {
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV3Pools(GetUniswapV3PoolsDto);
```

</br>

### Get Uniswap V3 Liquidity Transactions

Description: Return pool information across all Uniswap V3 pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetUniswapV3LiquidityTransactionsDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV3LiquidityTransactions(GetUniswapV3LiquidityTransactionsDto);
```

</br>

### Get Uniswap V3 Pool Swaps

Description: Return pool information across all Uniswap V3 pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetUniswapV3PoolSwapsDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getUniswapV3PoolSwaps(GetUniswapV3PoolSwapsDto);
```

</br>

## Pancakeswap Endpoints <img src="https://github.com/pancakeswap/pancake-frontend/blob/develop/public/logo.png?raw=true" width="40"/>

### Get Pancakeswap V2 Pools

Description: Return a paginated list of Pancake pools sorted by exchange volume. Only pools with swaps in the last 24 hours are included.

```ts
interface GetPancakeswapV2PoolsDto {
  tickers?: string;
  addresses?: string;
  quoteCurrency?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2Pools(GetPancakeswapV2PoolsDto);
```

</br>

### Get Pancakeswap V2 Pools By Address

Description: Given an address, return detailed pool information for the specified pool address.

```ts
interface GetPancakeswapV2PoolsByAddressDto {
  address: string;
  quoteCurrency?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2PoolsByAddress(GetPancakeswapV2PoolsByAddressDto);
```

</br>

### Get Pancakeswap V2 Address Balance

Description: Given a wallet address, return a list of Pancake V2 exchange balances.

```ts
interface GetPancakeswapV2AddressBalanceDto {
  address: string;
  quoteCurrency?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2AddressBalance(GetPancakeswapV2AddressBalanceDto);
```

</br>

### Get Pancakeswap V2 Network Exchange Tokens

Description: Return Pancakeswap v2 network exchange tokens.

```ts
interface GetPancakeswapV2NetworkExchangeTokensDto {}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2NetworkExchangeTokens(GetPancakeswapV2NetworkExchangeTokensDto);
```

</br>

### Get Pancakeswap V2 Single Network Exchange Token

Description: Given a tokenAddress, return Pancakeswap v2 single network exchange token for token address.

```ts
interface GetPancakeswapV2SingleNetworkExchangeTokenDto {
  tokenAddress: string;
  tickers?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2SingleNetworkExchangeToken(
  GetPancakeswapV2SingleNetworkExchangeTokenDto
);
```

</br>

### Get Pancakeswap V2 Ecosystem Chart Data

```ts
interface GetPancakeswapV2EcosystemChartDataDto {}
```

```js
await Moralis.Plugins.covalent.getPancakeswapV2EcosystemChartData(GetPancakeswapV2EcosystemChartDataDto);
```

</br>

## Sushiswap Endpoints <img src="https://github.com/sushiswap/sushiswap-interface/blob/canary/public/logo.png?raw=true" width="40"/>

</br>

### Get Sushiswap Address Exchange Balances

Description: Given a chainId and wallet address, return a list of Sushiswap address exchange balances.

```ts
interface GetSushiswapAddressExchangeBalancesDto {
  chainId: string;
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getSushiswapAddressExchangeBalances(GetSushiswapAddressExchangeBalancesDto);
```

</br>

### Get Sushiswap Address Liquidity Transactions

Description: Given a chainId and address, return a list of Sushiswap address exchange liquidity transactions.

```ts
interface GetSushiswapAddressLiquidityTransactionsDto {
  chainId: string;
  swaps?: boolean;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getSushiswapAddressLiquidityTransactions(GetSushiswapAddressLiquidityTransactionsDto);
```

</br>

### Get Sushiswap Pools

Description: Given a chainId, return pool information across all Sushiswap pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetSushiswapPoolsDto {
  chainId: string;
  tickers?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getSushiswapPools(GetSushiswapPoolsDto);
```

</br>

## Aave Endpoints <img src="https://raw.githubusercontent.com/aave/aave-ui/bf9b52643fdeefc53a6ebf179efd904d86505568/public/aave.svg" width="40"/>

</br>

### Get Aave V2 Address Balances

Description: Given a chainId and address, return a list of Aave v2 address balances, supply and borrow positions.

```ts
interface GetAaveV2AddressBalancesDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getAaveAddressV2Balances(GetAaveV2AddressBalancesDto);
```

</br>

### Get Aave V2 Network Assets Dto

Description: Given a chainId, return a list of Aave v2 pools.

```ts
interface GetAaveV2NetworkAssetsDto {
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getAaveV2Pools(GetAaveV2NetworkAssetsDto);
```

</br>

## Compound Endpoints <img src="https://raw.githubusercontent.com/compound-finance/compound-components/9a9ff55e565baf434e4013d0de971557596c0613/src/public/assets/asset_COMP.svg" width="40"/>

</br>

### Get Compound Address Activity

Description: Given an address, return a list of Compound address activity.

```ts
interface GetCompoundAddressActivityDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getCompoundAddressActivity(GetCompoundAddressActivityDto);
```

</br>

### Get Compound Address Balance

Description: Given an address, return a list of Compound address balances.

```ts
interface GetCompoundAddressBalanceDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getCompoundAddressBalances(GetCompoundAddressBalanceDto);
```

</br>

### Get Compound Pools

Description: Return a list of Compound pools.

```ts
interface GetCompoundPoolsDto {
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getCompoundPools(GetCompoundPoolsDto);
```

</br>

## Curve Endpoints <img src="https://image.pngaaa.com/550/5986550-middle.png" width="40"/>

</br>
 
### Get Curve Address Balances

Description: Given an address, return a list of Curve address balances.

```ts
interface GetCurveAddressBalancesDto {
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getCurveAddressBalances(GetCurveAddressBalancesDto);
```

</br>

## XYK Endpoints <img src="https://www.covalenthq.com/static/images/class-b/header/xy=k.svg" width="40"/>

xy=k is a generalized Uniswap-like endpoints for exchanges on various chains.
Supported chains: `'uniswap_v2', 'sushiswap', 'pancakeswap_v2', 'quickswap', 'pangolin', 'spiritswap', 'spookyswap', 'traderjoe'`

</br>

### Get XYK pools

Description: Given chainId and dexName, return pool information across all XY=K pools including LP token prices, reserves, exchange volumes and fees.

```ts
interface GetXYKpoolsDto {
  chainId: string;
  dexName: string;
  tickers?: string;
  addresses?: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKpools(GetXYKpoolsDto);
```

</br>

### Get XYK Pools By Address

Description: Given chainId, dexName and address, return pool information across all XY=K pools including LP token prices, reserves, exchange volumes and fees for address.

```ts
interface GetXYKPoolsByAddressDto {
  chainId: string;
  dexName: string;
  address: string;
  pageNumber?: number;
  pageSize?: number;
  tickers?: string;
}
```

```js
await Moralis.Plugins.covalent.getXYKPoolsByAddress(GetXYKPoolsByAddressDto);
```

</br>

### Get XYK Address Exchange Balances

Description: Given a chainId, dexName and address, return address exchange balances for a specific DEX.

```ts
interface GetXYKAddressExchangeBalancesDto {
  chainId: string;
  dexName: string;
  address: string;
  pageNumber?: number;
  pageSize?: number;
  quoteCurrency?: string;
}
```

```js
await Moralis.Plugins.covalent.getXYKAddressExchangeBalances(GetXYKAddressExchangeBalancesDto);
```

</br>

### Get XYK Network Exchange Tokens

Description: Given chainId and dexName, return network exchange tokens for a specific DEX.

```ts
interface GetXYKNetworkExchangeTokensDto {
  chainId: string;
  dexName: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKNetworkExchangeTokens(GetXYKNetworkExchangeTokensDto);
```

</br>

### Get XYK Single Network Exchange Token

Description: Given chainId and dexName, return network exchange tokens for a specific DEX.

```ts
interface GetXYKSingleNetworkExchangeTokenDto {
  chainId: string;
  dexName: string;
  tokenAddress: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKSingleNetworkExchangeToken(GetXYKSingleNetworkExchangeTokenDto);
```

</br>

### Get XYK Transactions For Account Address

Description: Given chainId, dexName and address, return transactions for account address for a specific DEX.

```ts
interface GetXYKTransactionsForAccountAddressDto {
  chainId: string;
  dexName: string;
  address: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKTransactionsForAccountAddress(GetXYKTransactionsForAccountAddressDto);
```

</br>

### Get XYK Transactions For TokenAddress

Description: Given chainId, dexName and tokenAddress, return transactions for token address for a specific DEX.

```ts
interface GetXYKTransactionsForTokenAddressDto {
  chainId: string;
  dexName: string;
  tokenAddress: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKTransactionsForTokenAddress(GetXYKTransactionsForTokenAddressDto);
```

</br>

### Get XYK Transactions For Exchange

Description: Given chainId, dexName and address, return transactions for exchange for a specific DEX.

```ts
interface GetXYKTransactionsForExchangeDto {
  chainId: string;
  dexName: string;
  address: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKTransactionsForExchange(GetXYKTransactionsForExchangeDto);
```

</br>

### Get XYK Ecosystem Chart Data

Description: Given chainId and dexName, return ecosystem chart data for a specific DEX.

```ts
interface GetXYKEcosystemChartDataDto {
  chainId: string;
  dexName: string;
  pageNumber?: number;
  pageSize?: number;
}
```

```js
await Moralis.Plugins.covalent.getXYKEcosystemChartData(GetXYKEcosystemChartDataDto);
```

</br>

### Get XYK Health Data

Description: Given chainId and dexName, return last synced block height data and latest block height for a specific DEX.

```ts
interface GetXYKHealthDataDto {
  chainId: string;
  dexName: string;
}
```

```js
await Moralis.Plugins.covalent.getXYKHealthData(GetXYKHealthDataDto);

```
