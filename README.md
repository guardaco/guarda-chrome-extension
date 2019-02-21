# Guarda Chrome Extension
--------------
Guarda Extension allows to access DApps, that works with Ethereum, Bitcoin and other blockchains, directly from Chrome Browser. It integrates Guarda Wallet on the web page.

### Web3
The Guarda Extension exposes the web3 API by an injected web3 object which you can access via JavaScript:
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
Using wallets api you can access such a user’s wallet information as an address and balance.

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
You can add deeplinks (buttons) to the web page. Deeplinks allow users to pay easily.

If the extension is installed in the browser, the popup for payment will open, otherwise, it will be redirected to [guarda.co](https://guarda.co)

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
