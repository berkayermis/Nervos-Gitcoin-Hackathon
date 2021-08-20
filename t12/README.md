# How to Port An Existing Ethereum DApp To Polyjuice To Run On Nervos' EVM Compatible Layer 2.

## Introduction

Polyjuice is an Ethereum compatible layer on top of Nervos CKB. By polyjuice, it is perfectly possible to use account model on Nervos CKB and it is designed to be used with the Godwoken layer 2 rollup framework. This allows Polyjuice to completely move smart contract execution off of layer 1 to layer 2, providing scalability that goes far beyond what the Ethereum Mainnet is capable of today.

- [Github](https://github.com/nervosnetwork/polyjuice)

In this article, you will clone an existing Ethereum DApp or you can use your special DApp as well. Then you will setup the Godwoken Testnet Network in MetaMask, 
install the all dependencies including Polyjuice dependencies, build the smart contracts, configure the Web3 Provider, set high gas limit for the current version on the Testnet and 
display Polyjuice address in your application.

## Prerequisites (Step 1)

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

## Setup the Godwoken Testnet Network in MetaMask (Step 2)

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

## View the Ethereum Application (Step 3)

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

## Install Polyjuice Dependencies (Step 4)

Finally, it's time to begin porting this Ethereum application to use Nervos' Layer 2.

Use the following command to install Polyjuice dependencies.

~~~
$ cd ~/projects/simple-DApp
$ yarn add @polyjuice-provider/web3@0.0.1-rc7 nervos-godwoken-integration@0.0.6
~~~




