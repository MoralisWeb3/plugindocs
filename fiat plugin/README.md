
## This plugin is for all dapps that want to allow their users to buy crypocurrencies straight from their dapp. This plugin supports most fiat currencies and most cryptocurrencies.

### Supported Platforms This version of the plugin only supports web apps. In the future we will add support for Unity and Mobile platforms.

### Usage After installing the plugin you can start using it with the following code:

This code will open up a new browser window and guide the user through the steps to purchase cryptocurrencies.

`Moralis.Plugins.fiat.buy()`

This will not open a new window with fiat onramp - instead you can embed the onramp in an iframe.

`let response = await Moralis.Plugins.fiat.buy({}, {disableTriggers: true});

document.getElementById('iframeid').style.display = 'block';

document.getElementById('iframeid').src = response.result.data;`

This code will preselect the coin and the receiver.

`Moralis.Plugins.fiat.buy({ coin: 'usdc', receiver: '0x...', });`
