# Guarda Chrome Extension
--------------
### What is Guarda Chrome Extension?
Guarda Extension allows accessing DApps (Decentralised Applications) working on Ethereum, Bitcoin and other blockchains. The access is performed through integrating Guarda Wallet with the Chrome Browser web page.

![Guarda Chrome Extension](guarda_extension.png?raw=true "Guarda Chrome Extension")

### How to work with the code?
If you want to interact with a blockchain from your web page, you will need web3. We’ve re-developed it to provide access to a wallet without accessing the user’s private keys.

### Web3
Guarda Extension exposes the web3 API with an injected web3 object that is accessible though JavaScript:
``` javascript
window.addEventListener('load', function() {
  // Checking if Web3 has been injected by the browser
  if (typeof web3 !== 'undefined') {
    // Use Guarda provider
    web3js = new Web3(web3.currentProvider);
    // Check if extension is unlocked:
    setInterval(function() {
        // Old fashion way.
        var isUnlocked = window.web3.eth.accounts[0].length > 0;
        // New way (See next section)
        var isLocked = !!window.guarda.defaultWallet
      }, 1000);
  } else {
    // Guarda Extension is not install, handle this case:
    handleThisCase();
  }
  // Now you can start your app
  startYourApp()
})
```
### Wallets api:
You can access the wallet public addresses and balances with the wallet’s API.

```javascript
// Check is extension is unlocked
window.addEventListener('load', () => {
    // provides info about all wallets
    const defaultWallet = windows.guarda.defaultWallet;

    //   {address: "0xc0539d482eFF70648540dddddddddddddd",
    //    balance: "0.1",
    //    currency: "eth"}

    // provides info about deafault wallet
    const wallets = window.guarda.wallets;

    //   [{address: "RViGdXfC7BR2U6iYt5BJFJasdasddqwqd", currency: "kmd", balance: "0"}
    //    {address: "QWWwr8XwcEyp6tgPeRBbxXmoAsdqdawqew", currency: "qtum", balance: "0"}
    //    {address: "0xc0539d482eFF70648540dddddddddddddd", currency: "eth",balance:"0.1"}]
})
```

### Deep Links:
You can add the deeplinks (buttons) to a web page to ease the payment process.

The payment popup will appear immediately with the Extension installed. In case it is not, you will be redirected to [guarda.co](https://guarda.co)

Example:
```html
<a target="_blank" href="https://guarda.co/app/send?amount=0.001&currencyFrom=btc&addressTo=1BZS3jJSCQRJiZJUaaS9t2yYv32nJ4NYcQ">
  Pay with guarda
</a>
```
Search params:
* amount: number
* addressTo: string
* currencyFrom: string
* gasLimit: string
* gasPrice: string
* nonce: string
* extraId: string
