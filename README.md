# Project: Degen Token (ERC-20): Unlocking the Future of Gaming
This repository will allow us to create an ERC20 token and deploy it on the Avalanche network for Degen Gaming. The smart contract should have the following functionality:

o	Minting new tokens: The platform should be able to create new tokens and distribute them to players as rewards. Only the owner can mint tokens.

o	Transferring tokens: Players should be able to transfer their tokens to others.

o	Redeeming tokens: Players should be able to redeem their tokens for items in the in-game store.

o	Checking token balance: Players should be able to check their token balance anytime.

o	Burning tokens: Anyone should be able to burn tokens they own that are no longer needed.

## Getting Started

Open the code folder and click on the google drive link, which should redirect you to a zip file. Download it and open it in your visual studio code application.

Copy the code in the DegenToken.Sol and go to https://remix.ethereum.org/#lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.18+commit.87f61d96.js. Create a new file with the name, paste the code, and flatten the code.

```Java
// SPDX-License-Identifier: MIT
pragma solidity 0.8.9;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Degen is ERC20 {
    address public owner;

    event Redeem(address _user, uint256 _amount);
    event Burn(address _user, uint256 _amount);

    constructor() ERC20("Degen", "DGN") {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function");
        _;
    }

    modifier checkAmount(uint256 _amount) {
        require(_amount != 0, "_amount should be non-zero!");
        _;
    }

    function mint(address _to, uint256 _amount) public onlyOwner checkAmount(_amount) {
        _mint(_to, _amount);
    }

    function redeem(uint256 _amount) external checkAmount(_amount) {
        _burn(msg.sender, _amount);

        emit Redeem(msg.sender, _amount);
    }

    function burn(uint256 _amount) external checkAmount(_amount){
        _burn(msg.sender, _amount);

        emit Burn(msg.sender, _amount);
    }
}
```

## Executing the Program

Ensure you are already signed in to Metamask. Ensure you have at least three accounts set up with enough test funds tokens to execute and play with the functions.

If you do not have any test funds tokens go to https://core.app/en/tools/testnet-faucet/?subnet=c&token=c. You will only be able to get two tokens per day at max.

Once that is set up, head over to the left side of the Remix page, wherein you will see different icons, Select the 4th icon named "Solidity Compiler." Check the auto-compile checkbox.

Next, click the 5th icon named "Deploy and run transactions." 

For the environment, select "Injected Provider - Metamask."

Your account should be detected directly from your Metamask.

For the contract, select "Degen - DegenToken_flatenned.sol."

Then in the "At Address" button copy this contract address and paste it: 0x08F0C975385F1Eaf68aAAa927315b97d6314e706. Click the "At Address" button to deploy it.

The contract should be deployed after clicking the "At Address" button and found in the "Deployed Contracts" tab.

Click the drop-down button of the deployed contract, and you should be able to see different functions for the contract such as burn, mint, and transfer.

## What the output of the deployed contract does?

o	Admin account will be the only one permitted to mint tokens. If the account is not an admin, it will throw an error.

o	All users can burn and transfer tokens if there are sufficient balance and task token funds; otherwise, it will throw an error.

o	Users can also check the balance of account addresses, check the token name and symbol, and view the total supply of tokens during the transactions.

o	Users can also redeem their tokens; the process is quite similar to the burn function as it would deduct the amount from the contract then it will make the user buy the item, (but in my case, I didn't create one) and the token will be burned from the token contract.

