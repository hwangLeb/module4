# BUILDING ON AVALANCHE
FOR THE LAST MODULE, THE TASK FOR THIS IS MINT,BURN,REDEEM,TRANSFER AND CHECK BALANCE OF THE PLAYER OR THE USERS.
# GETTING STARTED
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., module4.sol). Copy and paste the following code into the file:
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract DegenToken is ERC20, Ownable {
    mapping(uint256 => uint256) public itemPrices;

    constructor() ERC20("Degen", "DGN") Ownable(msg.sender) {
    }
        
    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }
     function transfer(address to, uint256 amount) public override returns (bool) {
        require(to != address(0), "ERC20: transfer to the zero address");
        return super.transfer(to, amount);
    }   
    function redeemItems(uint256 itemId, uint256 price) external onlyOwner {
        itemPrices[itemId] = price;
    }

    function redeem(uint256 itemId) public {
        uint256 price = itemPrices[itemId];
        require(price > 0, "Item not available for redemption");
        require(balanceOf(msg.sender) >= price, "Insufficient balance");
        _burn(msg.sender, price);
    }
    function balanceOf(address account) public view virtual override returns (uint256) {
        return super.balanceOf(account);
    }
}

# AUTHOR
Eugenio, Viel

3.1 BSIT
