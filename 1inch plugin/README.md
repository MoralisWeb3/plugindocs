# Moralis 1Inch Plugin

This plugin integrates the DeFi / DEX aggregator 1Inch to any project that uses Moralis.

## Available chains

This plugins works with 3 different blockchains (chain):

- Ethereum ("eth")
- Binance Smart Chain ("bsc")
- Polygon ("polygon")

## Available functions

The following functions are available:


- **getSupportedTokens({ chain: chain })**

```js
async function getSupportedTokens() {
  const tokens = await Moralis.Plugins.oneInch.getSupportedTokens({
    chain: 'bsc', // The blockchain you want to use (eth/bsc/polygon)
  });
  console.log(tokens);
}
```

- **quote({
  chain: chain,
  fromTokenAddress: fromTokenAddress,
  toTokenAddress: toTokenAddress,
  amount: tokenAmount
  })**

```js
async function getQuote() {

  const quote = await Moralis.Plugins.oneInch.quote({
    chain: 'bsc', // The blockchain you want to use (eth/bsc/polygon)
    fromTokenAddress: '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4', // The token you want to swap
    toTokenAddress: '0x6fd7c98458a943f469e1cf4ea85b173f5cd342f4', // The token you want to receive
    amount: 1000,
  });
  console.log(quote);
}
```

- **hasAllowance({
  chain: chain,
  fromTokenAddress: fromTokenAddress,
  amount: tokenAmount,
  fromAddress: user
  })**

```js
async function hasAllowance() {

  const allowance = await Moralis.Plugins.oneInch.hasAllowance({
    chain: 'bsc', // The blockchain you want to use (eth/bsc/polygon)
    fromTokenAddress: '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4', // The token you want to swap
    fromAddress: '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064', // Your wallet address
    amount: 1000,
  });
  console.log(`The user has enough allowance: ${allowance}`);
}
```

- **approve({
  chain: chain,
  tokenAddress: fromTokenAddress,
  fromAddress: user
  })**

```js
async function approve() {

  await Moralis.Plugins.oneInch.approve({
    chain: 'bsc', // The blockchain you want to use (eth/bsc/polygon)
    tokenAddress: '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4', // The token you want to swap
    fromAddress: '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064', // Your wallet address
  });
  
}
```

- **swap{
  chain: chain,
  fromTokenAddress: fromTokenAddress,
  toTokenAddress: toTokenAddress,
  amount: tokenAmount,
  fromAddress: user,
  slippage: splippage
  }**

```js
async function swap() {

  const receipt = await Moralis.Plugins.oneInch.swap({
    chain: 'bsc', // The blockchain you want to use (eth/bsc/polygon)
    fromTokenAddress: '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4', // The token you want to swap
    toTokenAddress: '0x6fd7c98458a943f469e1cf4ea85b173f5cd342f4',  // The token you want to receive
    amount: 1000,
    fromAddress: '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064', // Your wallet address
    slippage: 1,
  });
  console.log(receipt);
}
```

## Transaction fee

There is a 1% transaction fee on each swap. This fee is charged by Moralis, not 1inch.
