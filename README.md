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

## Usage

- **Become a Citizen**: Call the `becomeCitizen` function to register as a citizen.
- **Deposit Ether**: Use the `deposit` function to add funds to the treasury.
- **Withdraw Ether**: Use the `withdraw` function to retrieve your funds.
- **Declare Holiday**: If you are the king, call the `declareHoliday` function to declare a holiday.
