## Ethereum Basics

### Ether Currency Units

* Ether
    - Main currency of Ethereum
    - Represented as an unsigned integer value(uint)
* Wei
    -  One ether is 1 quintillion wei (1 * 1018 or 1,000,000,000,000,000,000)
    -  The value of ether is always represented internally in Ethereum as an unsigned integer value denominated in wei. When you transact 1 ether, the transaction encodes 1000000000000000000 wei as the value.

| Value (in wei)                    | Exponent        | Common name | SI name               |
|-----------------------------------|-----------------|-------------|-----------------------|
| 1                                 | 1               | wei         | wei                   |
| 1,000                             | 10<sup>3<sup/>  | Babbage     | Kilowei or femtoether |
| 1,000,000                         | 10<sup>6<sup/>  | Lovelace    | Megawei or picoether  |
| 1,000,000,000                     | 10<sup>9<sup/>  | Shannon     | Gigawei or Nanoether  |
| 1,000,000,000,000                 | 10<sup>12<sup/> | Szabo       | Microether or micro   |
| 1,000,000,000,000,000             | 10<sup>15<sup/> | Finney      | Milliether or milli   |
| 1,000,000,000,000,000,000         | 10<sup>18<sup/> | Ether       | Ether                 |
| 1,000,000,000,000,000,000,000     | 10<sup>21<sup/> | Grand       | Kiloether             |
| 1,000,000,000,000,000,000,000,000 | 10<sup>24<sup/> |             | Megaether             |

## Ethereum Wallet

*  A "wallet" is a software application that helps you manage your Ethereum account. In short, an Ethereum wallet is your gateway to the Ethereum system. It holds your keys and can create and broadcast transactions on your behalf.

### Wallets

* [Metamask](https://metamask.io/)
  - MetaMask is a browser extension wallet that runs in your browser (Chrome, Firefox, Opera, or Brave Browser). It is easy to use and convenient for testing, as it is able to connect to a variety of Ethereum nodes and test blockchains. MetaMask is a web-based wallet that also includes mobile apps for both iOS and Android.
* [Jaxx](https://www.jaxx.io/downloads)
  - Jaxx is a multiplatform and multicurrency wallet that runs on a variety of operating systems, including Android, iOS, Windows, macOS, and Linux. It is often a good choice for new users as it is designed for simplicity and ease of use. Jaxx is either a mobile or a desktop wallet, depending on where you install it.
* [MyEtherWallet](https://www.myetherwallet.com/)
  - MyEtherWallet is primarily a web-based wallet that runs in any browser. It is also available on Android and iOS. It has multiple sophisticated features we will explore in many of our examples.
* [EmeraldWallet](https://emerald.cash/)
  - Emerald Wallet is designed to work with the Ethereum Classic blockchain, but is compatible with other Ethereum-based blockchains. It’s an open source desktop application and works under Windows, macOS, and Linux. Emerald Wallet can run a full node or connect to a public remote node, working in a "light" mode. It also has a companion tool to do all operations from the command line.
 
## Using and getting started with Metamask

### Switching Networks

* Main Ethereum Network
    - The main public Ethereum blockchain. Real ETH, real value, and real consequences.

* Ropsten Test Network
    - Ethereum public test blockchain and network. ETH on this network has no value.

* Kovan Test Network
    - Ethereum public test blockchain and network using the Aura consensus protocol with proof of authority (federated signing). ETH on this network has no value. The Kovan test network is supported by Parity only. Other Ethereum clients use the Clique consensus protocol, which was proposed later, for proof of authority–based verification.

* Rinkeby Test Network
    - Ethereum public test blockchain and network, using the Clique consensus protocol with proof of authority (federated signing). ETH on this network has no value.

* Localhost 8545
    - Connects to a node running on the same computer as the browser. The node can be part of any public blockchain (main or testnet), or a private testnet.

* Custom RPC
    - Allows you to connect MetaMask to any node with a Geth-compatible Remote Procedure Call (RPC) interface. The node can be part of any public or private blockchain.
 
### TestEther

* Go to [https://faucet.metamask.io](https://goerlifaucet.com/)
