// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SisonCalorie {
    uint256 public totalCalories;
    uint256 constant CALORIES_PER_CUP = 140;
    event CalorieLogged(address indexed user, uint256 cups, uint256 calories);

    function logCalories(uint256 cups) public {
        uint256 calories = cups * CALORIES_PER_CUP;
        require(calories > 0 && calories <= 2000, "cups must be between 1 and 2000.");
        totalCalories += calories;
        emit CalorieLogged(msg.sender, cups, calories);
        assert(totalCalories >= calories);
    }
    function ResetCalories() public {
        if (totalCalories == 0) {
            revert("Total calories are already zero. No need to reset.");
        }
        totalCalories = 0;
        assert(totalCalories == 0);
    }
}
