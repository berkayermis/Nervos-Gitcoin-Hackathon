![Yellow Bordered Photo Eye Donation Poster (2)](https://user-images.githubusercontent.com/67913214/130240999-3bca03f1-df59-4f1b-b610-3505f4437c37.png)


# How to Port An Existing Ethereum DApp To Polyjuice To Run On Nervos' EVM Compatible Layer 2.

## Introduction

Polyjuice is an Ethereum compatible layer on top of Nervos CKB. By polyjuice, it is perfectly possible to use account model on Nervos CKB and it is designed to be used with the Godwoken layer 2 rollup framework. This allows Polyjuice to completely move smart contract execution off of layer 1 to layer 2, providing scalability that goes far beyond what the Ethereum Mainnet is capable of today.

- [Github](https://github.com/nervosnetwork/polyjuice)

In this article, you will clone an existing Ethereum DApp or you can use your special DApp as well. Then you will setup the Godwoken Testnet Network in MetaMask, 
install the all dependencies including Polyjuice dependencies, build the smart contracts, configure the Web3 Provider, set high gas limit for the current version on the Testnet and 
display Polyjuice address in your application.

## Prerequisites

### Installing MetaMask Wallet

You should install a MetaMask wallet in your browser and configure it.

MetaMask is a software cryptocurrency wallet used to interact with the Ethereum blockchain.
It allows users to access their Ethereum wallet through a browser extension or mobile app, which can then be used to interact with DApp.

Install MetaMask via [here](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn).
The installation process with a [video](https://youtu.be/Af_lQ1zUnoM).

### Installing Node.js and npm or yarn

Node.js is an open-source cross-platform JavaScript run-time environment that allows server-side execution of JavaScript code. 
This means that you can run JavaScript code on your machine.

Npm is the default package manager for Node.js.

install Node.js and npm by typing:

~~~
$ sudo apt install nodejs
~~~

The nodejs package contains both the node and npm binaries.

Check the Node.js and npm were successfully installed:

~~~
$ node --version
$ npm --version
~~~

If you want, you can use yarn to install the dependencies in the upcoming processes or use npm insted yarn.

yarn: It stands for **Yet Another Resource Negotiator** and it is a package manager just like npm.

In this example, I will show you how to use yarn but to install yarn, you should install npm before.

~~~
$ npm install --global yarn
~~~

Check that Yarn is installed by running:

~~~
$ yarn --version
~~~

## Setup the Godwoken Testnet Network in MetaMask (Step 1)

You should configure your MetaMask wallet to communicate with the Godwoken Layer 2 network. Hence, you need to configure a new custom RPC.
To do that, follow the below instructions.

![metamask-network-menu](https://user-images.githubusercontent.com/67913214/130223193-62fd7ab8-1f71-4d0e-8516-cba10566fc20.png)
![metamask-networks](https://user-images.githubusercontent.com/67913214/130223198-381fa9cb-8631-4ab6-9d85-8b4d35ffc8a0.png)

Fill out the form as below:

~~~
Network Name: Godwoken Testnet
RPC URL: https://godwoken-testnet-web3-rpc.ckbapp.dev
Chain ID: 71393
Currency Symbol: <Leave Empty>
Block Explorer URL: <Leave Empty>
~~~

## View the Ethereum Application (Step 2)

In this DApp, you will store the "Employee of the Month" datas inside the SimpleStorage.sol smart contract.
Feel free to use your own application or just clone my DApp by following below instructions.

Create a ~/projects directory.

~~~
$ mkdir ~/projects
$ cd ~/projects
$ git clone https://github.com/berkayermis/EmployeeDapp-Solidity.git simple-DApp
$ cd simple-DApp
~~~

In the next step, you should install the dependencies, build the simple storage smart contract and start the Ganache.

~~~
$ cd ~/projects/simple-DApp
$ yarn & yarn build & yarn start:ganache
~~~

After a while, Ganache should start and create some blocks at that moment.

Now, switch your MetaMask wallet network to **Localhost 8545** 

Then, type the below command.

~~~
$ cd ~/projects/simple-DApp
$ yarn ui
~~~

After you see the **Compiled successfully.** you will be able to access the application thorugh http://localhost:3000 

It will be something like that interface:

![Screenshot from 2021-08-11 08-00-31](https://user-images.githubusercontent.com/67913214/130226497-5ba003ad-508c-43fa-a9f3-c35ea604159e.png)

## Install Polyjuice Dependencies (Step 3)

Finally, it's time to begin porting this Ethereum application to use Nervos' Layer 2.

Use the following command to install Polyjuice dependencies.

~~~
$ cd ~/projects/simple-DApp
$ yarn add @polyjuice-provider/web3@0.0.1-rc7 nervos-godwoken-integration@0.0.6
~~~

```@polyjuice-provider/web3``` is a custom Polyjuice web3 provider. It is required for interaction with Nervos' Layer 2 smart contracts.
```nervos-godwoken-integration``` is a tool that can generate Polyjuice address based on your Ethereum address. You might be required to use Polyjuice address if you store values mapped to addresses in your contracts.

## Configure the Web3 Provider (Step 4)

This configuration process will replace the normal web3 provider that may be currently in use for Ethereum with one for the Godwoken Testnet.
Firstly, you need to create a new ```config.ts``` file inside your src folder and set the below informations.

As well as the Web3 provider, we need to add 2 more values to the config file which are ```ROLLUP_TYPE_HASH``` and ```ETH_ACCOUNT_LOCK_CODE_HASH``` respectively.

Now, go to the ```~/projects/simple-DApp/src/config.ts``` directory and add these constants there.

~~~
export const CONFIG = {
    WEB3_PROVIDER_URL: 'https://godwoken-testnet-web3-rpc.ckbapp.dev',
    ROLLUP_TYPE_HASH: '0x4cc2e6526204ae6a2e8fcf12f7ad472f41a1606d5b9624beebd215d780809f6a',
    ETH_ACCOUNT_LOCK_CODE_HASH: '0xdeec13a7b8e100579541384ccaf4b5223733e4a5483c3aec95ddc4c1d5ea5b22'
};
~~~

After configuring these values, we need to import the config file inside our application file by following below instructions:

~~~
$ ~/projects/simple-DApp/src/ui/app.tsx.
~~~

~~~
import { PolyjuiceHttpProvider } from '@polyjuice-provider/web3';
import { CONFIG } from '../config';
~~~

Now, we need to add Polyjuice provider and use web3 instance in our application to communicate with Polyjuice!

~~~
const godwokenRpcUrl = CONFIG.WEB3_PROVIDER_URL;
const providerConfig = {
    rollupTypeHash: CONFIG.ROLLUP_TYPE_HASH,
    ethAccountLockCodeHash: CONFIG.ETH_ACCOUNT_LOCK_CODE_HASH,
    web3Url: godwokenRpcUrl
};
const provider = new PolyjuiceHttpProvider(godwokenRpcUrl, providerConfig);
const web3 = new Web3(provider);
~~~

## Set High Gas Limit (Step 5)

For the transactions, Godwoken needs a gas limit, this process is necessary for the current version of testnest but it might not be appear in the future. We will see the progress of it but we need to set gas limit for now.

Open the ```~/projects/blockchain-workshop-ethereum-simple/src/lib/contracts/SimpleStorageWrapper.ts``` file in your editor and define the gas property as 6000000 at the top of the file.

~~~
const DEFAULT_SEND_OPTIONS = {
    gas: 6000000
};
~~~

## Display Polyjuice Address in the DApp (Step 6)

By using the ```AddressTranslator``` class we can translate the Ethereum address into the Polyjuice address.
To do that, import below library in the top region of your ```app.tsx``` file.

~~~
import { AddressTranslator } from 'nervos-godwoken-integration';
~~~

And finally, we can find the Polyjuice address by adding the following script.

~~~
const addressTranslator = new AddressTranslator();
const polyjuiceAddress = addressTranslator.ethAddressToGodwokenShortAddress(ethereumAddress);
~~~

## View Your Final DApp (Step 7)

Lastly, you can view you Godwoken demo application at this point which is working a Polyjuice DApp.
Now, you can visit the ```http://localhost:3000``` and view your final DApp which interacts with your MetaMask wallet and established all the needs for Polyjuice by changing the MetaMask wallet's network as ```Godwoken Testnet```.

If you fully completed all the instructions in this example, you will be able to see a similar interface as below.

![Screenshot from 2021-08-11 08-00-47](https://user-images.githubusercontent.com/67913214/130239177-a42e073a-184a-4767-9a2f-688139403107.png)

## Final Notes and Useful Links

So, now you have learned many things in this guide such as Polyjuice, configuration processes, MetaMask, dependencies, creating a new RPC network which is Godwoken Testnet in this example to completely make a Polyjuice DApp.

Now below links might be useful at this point, check this out and learn more!

[Polyjuice](https://docs.nervos.org/docs/essays/polyjuice)

[Godwoken Testnet](https://github.com/jjyr/godwoken-testnet)

[Frameworks](https://github.com/Kuzirashi/gw-gitcoin-instruction/blob/master/src/conceptual-explainers/frameworks.md#polyjuice)
