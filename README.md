# ETH-AVAX-MODULE-3-PROJECT
## Project Description 
For this project, we will write an ERC20-compliant smart contract to create your own token on a local Hardhat network. To get started, we will use the Hardhat boilerplate project that is shown in the Hardhat Website itself, which provides a solid foundation. Once you have set up the Hardhat project, you can begin writing your smart contract. The contract should be compatible with Remix, allowing easy interaction. As the contract owner, you should have the ability to mint tokens to a specified address. Additionally, any user should be able to burn and transfer tokens to other addresses.
### Hardhat Boilerplate Repository
https://hardhat.org/tutorial/boilerplate-project
## Deployment Instructions 
1. In the terminal, run the following command: npm install
2. To install the remixd package, run the following command: npm install -g @remix-project/remixd
3. To start the remixd server and share a local directory with the Remix IDE, run the following command: remixd -s ./ --remix-ide https://remix.ethereum.org
4. Install the OpenZeppelin Contracts library as a dependency by executing the following command: npm install @openzeppelin/contracts
5. To run the hardhat package, and start a local Ethereum development network, open another terminal and execute the following command: npx hardhat node

### Token.sol
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.3.0/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    address private owner;

    constructor() ERC20("Chocolate", "CHOC") {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the contract owner can call this function");
        _;
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        require(amount <= balanceOf(msg.sender), "Insufficient balance");
        return super.transfer(recipient, amount);
    }
}

```
