# Kingdom Treasury Smart Contract

Welcome to the Kingdom Treasury Smart Contract! This Solidity smart contract is designed to manage a simple kingdom's treasury. This is where citizens can deposit and withdraw Ether, and the king can perform special actions.

## Overview

The Kingdom Treasury Smart Contract allows:

- **Citizens**: Any Ethereum address can become a citizen, deposit Ether into the treasury, and withdraw their funds.
- **King**: The contract owner (king) can perform special actions like declaring holidays.

## Features

- **Citizen Management**: Addresses can register as citizens, enabling them to deposit and withdraw Ether.
- **Deposit and Withdrawal**: Citizens can deposit Ether into the treasury and withdraw their funds.
- **Special Actions by the King**: The king can declare holidays and perform other special actions.
- **Events**: Key actions such as deposits, withdrawals, and holiday declarations are logged with events.

## Contract Structure

- **Contract Structure**: Defines the main blueprint for the contract.
- **Variables**: Stores essential information such as the king's address and the total funds.
- **Types**: Uses a struct to define citizen properties.
- **Functions**: Includes functions for citizen registration, deposit, withdrawal, and king's actions.
- **Visibility and Modifiers**: Ensures that only the king can perform certain actions and only citizens can deposit or withdraw.
- **Global Variables**: Demonstrates the use of global variables like block timestamp.
- **Operators and Conditionals**: Performs checks and balances for various operations.
- **Arrays and Mappings**: Manages lists of citizens and their information.
- **Events**: Logs important actions for transparency and tracking.

## Pseudo Code

I created a pseudo code version of the contract to design and understand this smart contract better,. The pseudo code helps in visualizing the structure and logic of the contract in a simplified manner. You can find the pseudo code in this repo to get a clear idea of how the contract is organized and functions before diving into the Solidity code.

## Usage

- **Become a Citizen**: Call the `becomeCitizen` function to register as a citizen.
- **Deposit Ether**: Use the `deposit` function to add funds to the treasury.
- **Withdraw Ether**: Use the `withdraw` function to retrieve your funds.
- **Declare Holiday**: If you are the king, call the `declareHoliday` function to declare a holiday.

## Smart Contract Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Contract Structure
contract KingdomTreasury {

    // Variables
    address public king;
    uint256 public totalFunds;

    // Types
    struct Citizen {
        uint256 balance;
        bool isCitizen;
    }

    // Mappings
    mapping(address => Citizen) public citizens;

    // Modifiers
    modifier onlyKing() {
        require(msg.sender == king, "Only the king can perform this action.");
        _;
    }

    // Custom Modifiers
    modifier onlyCitizen() {
        require(citizens[msg.sender].isCitizen, "Only citizens can perform this action.");
        _;
    }

    // Constructors
    constructor() {
        king = msg.sender;
    }

    // Functions
    function becomeCitizen() public {
        require(!citizens[msg.sender].isCitizen, "Already a citizen.");
        citizens[msg.sender] = Citizen(0, true);
    }

    function deposit() public payable onlyCitizen {
        citizens[msg.sender].balance += msg.value;
        totalFunds += msg.value;
        emit Deposit(msg.sender, msg.value);
    }

    function withdraw(uint256 amount) public onlyCitizen {
        require(citizens[msg.sender].balance >= amount, "Insufficient balance.");
        citizens[msg.sender].balance -= amount;
        totalFunds -= amount;
        payable(msg.sender).transfer(amount);
        emit Withdraw(msg.sender, amount);
    }

    function declareHoliday() public onlyKing {
        emit HolidayDeclared("A holiday has been declared by the king!");
    }

    // Global Variables
    function getBlockTimestamp() public view returns (uint256) {
        return block.timestamp;
    }

    // Operators and Conditionals
    function checkBalance(address citizen) public view returns (string memory) {
        if (citizens[citizen].balance > 1 ether) {
            return "Wealthy citizen";
        } else {
            return "Regular citizen";
        }
    }

    // Arrays
    address[] public citizenList;

    function addCitizenToList(address citizen) public onlyKing {
        citizenList.push(citizen);
    }

    // Structs
    function getCitizenInfo(address citizen) public view returns (uint256, bool) {
        Citizen memory c = citizens[citizen];
        return (c.balance, c.isCitizen);
    }

    // Events
    event Deposit(address indexed citizen, uint256 amount);
    event Withdraw(address indexed citizen, uint256 amount);
    event HolidayDeclared(string message);

    // Ether
    function kingdomBalance() public view returns (uint256) {
        return address(this).balance;
    }

    // Errors
    error InsufficientFunds(uint256 requested, uint256 available);

    // Inheritance
    // This contract could inherit from a more complex contract if needed

    // Calling Other Contracts
    function callAnotherContract(address otherContract) public {
        OtherContract(otherContract).receiveMessage("Hello from KingdomTreasury");
    }

    // Interfaces
    interface OtherContract {
        function receiveMessage(string memory message) external;
    }
}
```

## License

This project is licensed under the MIT License.
