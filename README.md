# Create React dApp -- An Ethereum App Bootstrapper

## Quick Start

### [Install Truffle](http://truffleframework.com/docs/getting_started/installation)
```
npm install -g truffle
```
### Create your app and start a Ganache blockchain.
```
npx create-react-dapp mydapp
cd mydapp
npm run ganache
```

### Compile and deploy contracts, then launch the app.

In a separate shell

```
npm run migrate
npm start
```

# Contents

<!-- toc -->

- [Features](#features)
- [Depolyment Options](#depolyment-options)
  * [Ganache and Ganache UI](#ganache-and-ganache-ui)
  * [Rinkeby and Other TestNets](#rinkeby-and-other-testnets)
  * [Ethereum MainNet](#ethereum-mainnet)

<!-- tocstop -->

## Features

1. Uses Facebook's `create-react-app` directly, so it will always retrieve the latest React and Webpack features and best practices, with no configuation.
2. Clear separation of concerns between the React and Ethereum programming.
3. Uses Truffle for compilation and migration management of Ganache, Rinkeby, and MainNet configurations.
4. Minimal self-contained installation. Doesn't require Remix, Geth, or Parity.

## Deployment Options

All of the out-of-the box deployment configurations are in the [truffle.js](./template/dapp/truffle.js) file.

All of the `npm run ...` scripts are in the [package.json](./template/package.json) file.

BTW feel free to use **yarn** instead of **npm** in any of the commands below (I do).

### Ganache and Ganache UI

The Quick Start section uses the `ganache-cli` testnet (formerly `testrpc`). This is the simplest and default configuration.

The [Ganache UI](http://truffleframework.com/ganache/) gives a more visual and interactive interaction to a Ganache testnet. After installing and launching the Ganache UI. Use

```
npm run migrate_ganacheUI
```
... and in a separate shell
```
npm run start_ganacheUI
```

> 💡 Restarting the GanachUI is easy but not obvious. Click on the ⚙️ icon in the upper right of the UI. Then click the "Restart" button.

### Rinkeby and Other Public TestNets

For the public test nets you will need to install [MetaMask](https://metamask.io/) in your browser. Follow the installation instructions, create an account, then use the upper right menu to select the "Rinkeby Test Network".

> ⚠️ **Security precaution.** If you already have a real Ethereum account on the Main Ethereum Network, you should create a new dummy account for use with Rinkeby. This will prevent accidental exposure of your real account's PrivateKey. To do so use the MetaMask account selection icon (upper, second from the right).

You will also need to get some test "ether" from the [Rinkeby Faucet](https://www.rinkeby.io/#faucet)

Next copy the account's Private Key from MetaMask. To do so click on the **▪️ ▪️ ▪️** icon to the right of the account's name, click "Export Private Key", follow the password prompt, then click on the private key to copy it to the clipboard.

Now we're ready to go. 
```
ETH_PK=<paste private key here> npm run migrate_rinkeby
```
... and in a separate shell
```
npm run start_rinkeby
```

Once a smart contract is deployed to a public network it lives there forever. However our sample contracts inherit from the standard `mortal` contract, which means they have a "kill" switch. To kill the contracts in Rinkeby use

```
ETH_PK=<paste private key here> npm run kill_rinkeby
```
> ⚠️ Redo'ing the "migrate" step overwrites the contract address in the compilation artifacts, so the "kill" script will not be able to find the contract to kill. So be sure to "kill" the contracts before re-migrating.

> 💡 Truffle migrations are designed to be roughly analogous to database migrations, in that they replace and/or extend the original contracts. Migrations need to be thought through carefully and are case specific. So for simplicity the included `npm run migrate...` scripts heavy handedly `--reset` and `--compile-all`.

The other test nets (Kovan and Ropsten) should be similar, but you will need to add their configs to [truffle.js](./template/dapp/truffle.js) and optionally migrate and start scripts to [package.json](./template/package.json)

### Ethereum Main Network

Once everything is tested thoroughly on Rinkeby, you'll want to deploy to the Ethereum Main Network. No scripts are included for working with the "live" network, because if you are to this point you don't need to use the scripts as training wheels.

> ⚠️ Deploying the scripts will cost you. At the time of this writing it's about $5, and each "vote" in the app costs about $0.10. However if you set your `gasPrice` too high it can cost you a lot more. So don't put your life savings into the account that you deploy from, and be careful how you set the `gas` and `gasPrice` parameters in [truffle.js](./template/dapp/truffle.js)
