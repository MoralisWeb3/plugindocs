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
  const chain = 'bsc';
  const tokens = await Moralis.Plugins.oneInch.getSupportedTokens({
    chain: chain,
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
  const chain = 'bsc';
  const fromTokenAddress = '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4'; // The token you want to swap
  const toTokenAddress = '0x6fd7c98458a943f469e1cf4ea85b173f5cd342f4'; // The token you want to receive
  const tokenAmount = 1000;

  const quote = await Moralis.Plugins.oneInch.quote({
    chain: chain,
    fromTokenAddress: fromTokenAddress,
    toTokenAddress: toTokenAddress,
    amount: tokenAmount,
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
  const chain = 'bsc'; // The blockchain you want to use (eth/bsc/polygon)
  const fromTokenAddress = '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4'; // The token you want to swap
  const user = '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064'; // Your wallet address
  const tokenAmount = 1000;

  const allowance = await Moralis.Plugins.oneInch.hasAllowance({
    chain: chain,
    fromTokenAddress: fromTokenAddress,
    fromAddress: user,
    amount: tokenAmount,
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
  const chain = 'bsc'; // The blockchain you want to use (eth/bsc/polygon)
  const fromTokenAddress = '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4'; // The token you want to swap
  const user = '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064'; // Your wallet address

  await Moralis.Plugins.oneInch.approve({
    chain: chain,
    tokenAddress: fromTokenAddress,
    fromAddress: user,
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
  const chain = 'bsc'; // The blockchain you want to use (eth/bsc/polygon)
  const fromTokenAddress = '0x0da6ed8b13214ff28e9ca979dd37439e8a88f6c4'; // The token you want to swap
  const toTokenAddress = '0x6fd7c98458a943f469e1cf4ea85b173f5cd342f4'; // The token you want to receive
  const user = '0x6217e65d864d77DEcbFF0CFeFA13A93f7C1dD064'; // Your wallet address
  const tokenAmount = 1000;
  const splippage = 1;

  const receipt = await Moralis.Plugins.oneInch.swap({
    chain: chain,
    fromTokenAddress: fromTokenAddress,
    toTokenAddress: toTokenAddress,
    amount: tokenAmount,
    fromAddress: user,
    slippage: splippage,
  });
  console.log(receipt);
}
```

## Transaction fee

There is a 1% transaction fee on each swap.