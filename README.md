# BUILDING ON AVALANCHE
FOR THE LAST MODULE, THE TASK FOR THIS IS MINT,BURN,REDEEM,TRANSFER AND CHECK BALANCE OF THE PLAYER OR THE USERS.
# GETTING STARTED
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., DEGEN.sol). Copy and paste the following code into the file:


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC20/ERC20.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/access/Ownable.sol";

contract DegenToken is ERC20, Ownable {
    struct InGameItem {
        uint256 id;
        string name;
        uint256 price;
    }

    InGameItem[] public inGameItems;

    constructor() ERC20("Degen", "DGN") {
        inGameItems.push(InGameItem(1, "NewJeans Album", 100 * 1 ** decimals()));
        inGameItems.push(InGameItem(2, "Le Sserafim Photocard", 200 * 1 ** decimals()));
        inGameItems.push(InGameItem(3, "GFriend Lightstick ver. 3", 500 * 1 ** decimals()));
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function transferTokens(address to, uint256 amount) public {
        require(amount > 0, "Transfer amount must be greater than 0");
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");

        _transfer(msg.sender, to, amount);
    }   

    function redeemTokens(uint256 itemId) public {
        require(itemId < inGameItems.length, "Invalid item ID");
        InGameItem storage item = inGameItems[itemId];
        require(balanceOf(msg.sender) >= item.price, "Insufficient balance");
        _burn(msg.sender, item.price);
    }

    function checkTokenBalance(address account) public view returns (uint256) {
        return balanceOf(account);
    }

    function burnTokens(uint256 amount) public {
        require(amount > 0, "Burn amount must be greater than 0");
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");

        _burn(msg.sender, amount);
    }
}

# AUTHOR
Eugenio, Viel

3.1 BSIT
