// SPDX-License-Identifier: MIT
pragma solidity ^0.8.25;

contract ErrorControl {
    function Require(uint userInput) public pure {
        require(userInput > 10, "Input must be greater than 10");
    }
    
    function Revert(uint userInput) public pure {
        if (userInput <= 10) {
            revert("Input must be greater than 10");
        }
    }

    uint public value;

    function Assert() public view {
        assert(value == 0);
    }

    error InsufficientFunds(uint currentBalance, uint requiredAmount);

    function CustomizedError(uint amount) public view {
        uint balance = address(this).balance;
        if (balance < amount) {
            revert InsufficientFunds({currentBalance: balance, requiredAmount: amount});
        }
    }
}
