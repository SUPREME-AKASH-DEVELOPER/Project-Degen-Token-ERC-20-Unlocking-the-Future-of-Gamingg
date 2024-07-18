# Project-Degen-Token-ERC-20-Unlocking-the-Future-of-Gamingg
# Talent Show Token

The Talent Show Token is an ERC-20 token built on the Avalanche network. It is designed for a gamified ecosystem where players can earn, transfer, and redeem tokens for virtual talent show items. This project leverages the fast and low-fee transactions of Avalanche to provide a seamless and engaging experience for users.

## Contract Overview

### Features

- **Minting Tokens**: Only the owner can mint new tokens and distribute them to players as rewards.
- **Transferring Tokens**: Players can transfer tokens to each other.
- **Redeeming Items**: Players can redeem tokens for talent items such as yoyos, bottles, balls, and puppets. Each item has a specific token cost.
- **Burning Tokens**: Any token holder can burn their tokens to manage supply.
- **Checking Balance**: Players can check their token balance at any time.

### Talent Items

The following items can be redeemed using tokens:

- **Yoyo**: Costs 10 tokens
- **Bottle**: Costs 20 tokens
- **Balls**: Costs 30 tokens
- **Puppet**: Costs 40 tokens

## Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";

contract TalentShowToken is ERC20, Ownable, ERC20Burnable {

    constructor() ERC20("Talent Show", "MST") Ownable(msg.sender) {}

    // Enum for talent items
    enum Talentitems { yoyo, bottle, balls, Puppet }

    // Struct to store player's talent show items balance
    struct PlayerItems {
        uint256 yoyo;
        uint256 bottle;
        uint256 balls;
        uint256 Puppet;
    }

    // Mapping from player address to their talent show items balance
    mapping(address => PlayerItems) public playerItems;

    // Function to mint new tokens, only callable by the owner
    function mintTokens(address to, uint256 amount) external onlyOwner {
        _mint(to, amount);
    }

    // Function to transfer tokens to another address
    function transferTokens(address to, uint256 amount) external {
        _transfer(_msgSender(), to, amount);
    }

    // Function to redeem tokens for talent items
    function redeemItem(Talentitems item) external {
        uint256 cost;
        if (item == Talentitems.yoyo) {
            cost = 10;
            playerItems[msg.sender].yoyo += 1;
        } else if (item == Talentitems.bottle) {
            cost = 20;
            playerItems[msg.sender].bottle += 1;
        } else if (item == Talentitems.balls) {
            cost = 30;
            playerItems[msg.sender].balls += 1;
        } else if (item == Talentitems.Puppet) {
            cost = 40;
            playerItems[msg.sender].Puppet += 1;
        } else {
            revert("Invalid talent items");
        }
        
        require(balanceOf(msg.sender) >= cost, "Insufficient balance");
        burn(cost);
    }

    // Function to burn tokens, callable by anyone for their own tokens
    function burnTokens(uint256 amount) external {
        burn(amount);
    }

    // Function to check token balance
    function checkBalance(address account) external view returns (uint256) {
        return balanceOf(account);
    }
}
```

## Getting Started

### Prerequisites

- Node.js
- Hardhat
- Avalanche network setup

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/talent-show-token.git
   cd talent-show-token
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Deploy the contract:
   ```bash
   npx hardhat run scripts/deploy.js --network avalanche
   ```

## Video Walkthrough

For a detailed walkthrough of the project, watch this [video](https://www.loom.com/share/ccd54e44e0d54068a9d228f2e7949da4?sid=d933099e-2034-44ed-8642-3357f9ced0a6).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- OpenZeppelin for their secure and reliable contract libraries.
- Avalanche for their high-performance blockchain platform.

---
## Author 
   Akash- akashlakhwan2329@gmail.com


   ![image](https://github.com/user-attachments/assets/0975c63d-04d8-41d9-8f0f-704d6c9851cd)
