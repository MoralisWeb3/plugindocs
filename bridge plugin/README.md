# Moralis Bridge Plugin

This plugins allows interoperability between different blockchains.

## Available chains

This plugins works with 2 different blockchains:

- Ethereum ("ethereum")
- Polygon ("polygon")

## Available functionalities

- Bridge native coins (Ether) from Ethereum to Polygon
- Bridge ERC20 from Ethereum to Polygon
- Bridge ERC20 from Polygon to Ethereum

## Available networks

- Testnet : 'testnet' (Goerli / Mumbai)
- Mainnet: 'mainnet'

## Useful notes

- The plugin refers to 'native coins' (Ether) using the address: `0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee`

## Available functions

### Brige native coins (Ether) and ERC20 from Ethereum to Polygon

```js
// This function triggers a Metamask transaction
async function deposit() {
  await Moralis.Plugins.bridge.deposit({
    network: 'testnet',
    fromChain: 'ethereum',
    toChain: 'polygon',
    tokenAddress: '0xeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee',
    amount: 10 ** 17,
    userAddress: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
  });
}
```

![Alt Text](https://media.giphy.com/media/oA0Z1ZwkScZInYOiCW/giphy.gif)

## Bridge ERC20 from Polygon to Ethereum

**The 'burn' caveat:**

Withdrawing assets back to Ethereum is a 2 step process in which the asset tokens has to be first burnt on the Polygon chain and then the proof of this burn transaction has to be submitted on the Ethereum chain.
It takes about 20 mins to 3 hours for the burn transaction to be checkpointed into the Ethereum chain. This is done by the Proof of Stake validators. DOCUMENTATION: `https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/getting-started`

In order to burn a token on Polygon it is necessary to call the function `deposit()` (as in the previous example). <br />
In order to claim a token on Ethereum is necessary to call the function `claim()`.

**NOTICE:** Due to the time required for Ethereum to checkpoint the burn transaction, it is necessary to call the function `claim()` at a regular interval. <br />The function throws the following error if the transaction is not checkpointed:

```js
{
  "code": 500006,
  "message": "The blockchains are not synced yet",
  "details": {
    "method": "isChainSynced",
    "network": "testnet",
    "transactionHash": "0x43cf95cdb3946d831f32b7651faeacda975ac281c0f0e8aaf676dd8821288c49"
  }
}
```

The example below calls `claim()` every 2 minutes until it gets a positive response, then triggers metamask to claim the tokens.
User must run the transaction on Ethereum (`Moralis.switchNetwork(_networkId)`) allows you to switch network in Metamask.

```js
// This function triggers a Metamask transaction
setInterval(async () => {
  try {
    const r = await Moralis.Plugins.bridge.claim({
      network: 'testnet',
      fromChain: 'ethereum',
      toChain: 'polygon',
      userAddress: 0xe78dc206875373b351eef2d182025bb9a64d67b3,
      transactionHash: txHash,
    });
    if (r) return;
  } catch (error) {}
}, 2 * 60 * 1000); // load every 2 minutes
```

![Alt Text](https://media.giphy.com/media/I7A7QAV4Kd7kZMOaUF/giphy.gif)

In order to handle ERC20 tokens, this plugin includes the very known functions:

- hasAllowance()
- approveErc20()

hasAllowance:

```js
const hasAllowance = await Moralis.Plugins.bridge.hasAllowance({
  network: 'testnet',
  chain: 'ethereum',
  userAddress: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
  tokenAddress: '0xfe4f5145f6e09952a5ba9e956ed0c25e3fa4c7f1',
  amount: 10 ** 17,
});
```

approveErc20:

```js
await Moralis.Plugins.bridge.approveErc20({
  network: 'testnet',
  userAddress: '0xE78dC206875373B351EEF2D182025bb9a64d67B3',
  tokenAddress: '0xfe4f5145f6e09952a5ba9e956ed0c25e3fa4c7f1',
  amount: 10 ** 17,
});
```

## Notice

This plugin is a wrapper around the Polygon bridge and it relies fully on the Official Polygon bridge to make the swaps.
If something goes wrong with Polygon, their bridge, their validators - it's outside of Moralis control.
There is a 1% transaction fee on each swap.
