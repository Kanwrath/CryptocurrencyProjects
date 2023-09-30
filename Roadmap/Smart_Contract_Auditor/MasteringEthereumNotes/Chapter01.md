## What is Ethereum?

* An open source, globally decentralized, computing infastructure that executes programs called _smart contracts_. It uses blockchain to synchronize and stor the systems state changes along with a crypto currency called ether to meter and constrain execution reseources.

  - What are [smart contracts?](https://ethereum.org/en/developers/docs/smart-contracts/)
      -  They are a program that runs on the the Ethereum blockchain. A collection of code(it's functions) and data (its state) reside at a specific address on the Ethereum blockchain.
      -  Smart contracts are deployed to the network and run as programmed. A metaphor for them is like a vending machine. Vending machines are deployed with pre programmed logic and when the right inputs are used, a certain output is guaranteed.
      -  In the same way a vending machine removes the human vendor, the smart contract removes the need for intermediaries in many industries and examples.
      -  Characteristics of smart contracts
          - Permissionless - Anyone can write a smart contract and deploy it using the appropriate coding language(Solidity)
          - Composability - Smart contracts are public and are essentially open API's contracts can call other contracts extending capability and possibility.

## Ethereum was a response to Bitcoin

* Developers wanted to build and the limitations of Bitcoin proved to be the catalyst for ethereum to be created.

## Components of a Blockchain

* A peer-to-peer (P2P) network connecting participants and propagating transactions and blocks of verified transactions, based on a standardized "gossip" protocol

* Messages, in the form of transactions, representing state transitions

* A set of consensus rules, governing what constitutes a transaction and what makes for a valid state transition

* A state machine that processes transactions according to the consensus rules

* A chain of cryptographically secured blocks that acts as a journal of all the verified and accepted state transitions

* A consensus algorithm that decentralizes control over the blockchain, by forcing participants to cooperate in the enforcement of the consensus rules

* A game-theoretically sound incentivization scheme (e.g., proof-of-work costs plus block rewards) to economically secure the state machine in an open environment

* One or more open source software implementations of the above ("clients")

## Ethereum Overview

### The idea was that by using a general-purpose blockchain like Ethereum, a developer could program their particular application without having to implement the underlying mechanisms of peer-to-peer networks, blockchains, consensus algorithms, etc. The Ethereum platform was designed to abstract these details and provide a deterministic and secure programming environment for decentralized blockchain applications.

The original blockchain, namely Bitcoin’s blockchain, tracks the state of units of bitcoin and their ownership. You can think of Bitcoin as a distributed consensus state machine, where transactions cause a global state transition, altering the ownership of coins. The state transitions are constrained by the rules of consensus, allowing all participants to (eventually) converge on a common (consensus) state of the system, after several blocks are mined.

Ethereum is also a distributed state machine. But instead of tracking only the state of currency ownership, Ethereum tracks the state transitions of a general-purpose data store, i.e., a store that can hold any data expressible as a key–value tuple. A key–value data store holds arbitrary values, each referenced by some key; for example, the value "Mastering Ethereum" referenced by the key "Book Title". In some ways, this serves the same purpose as the data storage model of Random Access Memory (RAM) used by most general-purpose computers. Ethereum has memory that stores both code and data, and it uses the Ethereum blockchain to track how this memory changes over time. Like a general-purpose stored-program computer, Ethereum can load code into its state machine and run that code, storing the resulting state changes in its blockchain. Two of the critical differences from most general-purpose computers are that Ethereum state changes are governed by the rules of consensus and the state is distributed globally. Ethereum answers the question: "What if we could track any arbitrary state and program the state machine to create a world-wide computer operating under consensus?"

## Ethereum Components

* P2P network
  - Ethereum runs on the Ethereum main network, which is addressable on TCP port 30303, and runs a protocol called ÐΞVp2p.

* Consensus rules
  - Ethereum’s consensus rules are defined in the reference specification, the Yellow Paper (see Further Reading).

* Transactions
  - Ethereum transactions are network messages that include (among other things) a sender, recipient, value, and data payload.

* State machine
  - Ethereum state transitions are processed by the Ethereum Virtual Machine (EVM), a stack-based virtual machine that executes bytecode (machine-language instructions). EVM programs, called "smart contracts," are written in high-level languages (e.g., Solidity) and compiled to bytecode for execution on the EVM.

* Data structures
  - Ethereum’s state is stored locally on each node as a database (usually Google’s LevelDB), which contains the transactions and system state in a serialized hashed data structure called a Merkle Patricia Tree.

* Consensus algorithm
  - Ethereum uses Bitcoin’s consensus model, Nakamoto Consensus, which uses sequential single-signature blocks, weighted in importance by PoW to determine the longest chain and therefore the current state. However, there are plans to move to a PoS weighted voting system, codenamed Casper, in the near future.

* Economic security
  - Ethereum currently uses a PoW algorithm called Ethash, but this will eventually be dropped with the move to PoS at some point in the future.

* Clients
  - Ethereum has several interoperable implementations of the client software, the most prominent of which are Go-Ethereum (Geth) and Parity.

## The Turing Complete Problem

* Turing completeness is very dangerous, particularly in open access systems like public blockchains, because of the halting problem we touched on earlier. For example, modern printers are Turing complete and can be given files to print that send them into a frozen state. The fact that Ethereum is Turing complete means that any program of any complexity can be computed by Ethereum. But that flexibility brings some thorny security and resource management problems. An unresponsive printer can be turned off and turned back on again. That is not possible with a public blockchain.

* Infinite loops are possible and can introduce DoS risks to the network. i.e a smart contract can be created to run forever when a when a doe attempts to validate it.

## Gas, the solution to the Turing Complete issue

* Ethereum introduces a metering mechanism called gas. As the EVM executes a smart contract, it carefully accounts for every instruction (computation, data access, etc.). Each instruction has a predetermined cost in units of gas. When a transaction triggers the execution of a smart contract, it must include an amount of gas that sets the upper limit of what can be consumed running the smart contract. The EVM will terminate execution if the amount of gas consumed by computation exceeds the gas available in the transaction. Gas is the mechanism Ethereum uses to allow Turing-complete computation while limiting the resources that any program can consume.
  
* Gas comes from the ether balance.Any unused gas is refunded to the sender after the transaction is complete

## DApp, the next evolution of Ethereum

* What is a DApp?
    - A DApp is composed of 
        - Smart contracts on a block chain
        - A web front end user inter face
    - May also include
        - A decentralized storage protocol and platform
        - a decentralized messaging protocol and platform
     
## [DApp structure](https://www.geeksforgeeks.org/architecture-of-a-dapp/#)

![alt text](https://github.com/Kanwrath/Web3-Ethereum-Smart_Contracts-Blockchains/blob/main/Roadmap/img/ArchitectureofaDApp.jpeg)

1. Ethereum blockchain: Ethereum is a decentralized and open-source blockchain platform that establishes a peer-to-peer network that securely executes and verifies application code, called smart contracts. Decentralized applications have their backend code (smart contracts) running on a decentralized network and not a centralized server. DApps use the Ethereum blockchain for data storage.

2. Smart Contracts: DApps use smart contracts to define the state changes happening on the blockchain. A smart contract is a collection of code and data that resides at a specific address on the Ethereum Blockchain and runs on the Ethereum blockchain. They are written in high-level languages such as Solidity and Vyper.
``` solidity

// Example of smart contract in 
// decentralized application
  
// SPDX-License-Identifier: MIT
pragma solidity >=0.4.22 <0.9.0;
  
contract Migrations 
{
  address public owner = msg.sender;
  uint public last_completed_migration;
  
  modifier restricted() 
  {
    require(
      msg.sender == owner,
      "This function is restricted to the contract's owner"
    );
    _;
  }
  
  function setCompleted(uint completed) public restricted 
  {
    last_completed_migration = completed;
  }
}
```

3. Ethereum Virtual Machine(EVM): The Ethereum Virtual Machine is the global virtual computer that executes the logic defined in the smart contracts and processes the state changes that happen on this Ethereum network.

4. Front-end: The front-end is the part of the DApps users can see and interact with such as the graphical user interface(GUI), but the front-end also communicates with the application logic defined in smart contracts.

## What is a "provider"

* The nodes one connects with to interact with the blockchain are often called “providers.”

* Ethereum provider (i.e. nodes) implements a JSON-RPC specification. This ensures that there’s a uniform set of methods when our frontend applications want to interact with the blockchain. One can read the state stored on the blockchain once connected to the blockchain through a provider.

## What is a signer? 

* if one wants to write to the state before one can submit the transaction to the blockchain there’s one more thing that needs to be done and the thing is “sign” the transaction using the private key.

* Enter Metamask
    - Metamask is a browser plugin that serves as an Ethereum wallet. we know that the Ethereum blockchain is a network and we need a special browser extension to connect that network.
    - Metamask will allow us to connect the blockchain with our personal account and interact with the smart contract.
    - A user’s private keys are stored by Metamask in the browser, and when a user wants to write to the state, the user needs to “sign” the transaction using the private key.
    - Metamask acts both as a provider and a signer because Metamask provides a connection to the blockchain (as a “provider”) and since it needs it to sign transactions that’s why it is also a signer.
