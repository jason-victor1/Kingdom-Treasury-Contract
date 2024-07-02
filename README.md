# Kingdom Treasury Smart Contracts

This contract suite is designed to manage a simple kingdom's treasury, where citizens can deposit and withdraw Ether, and the king can perform special actions. These contracts are ideal for managing a treasury system in a blockchain environment, potentially for a game or a decentralized organization.

## Contracts Overview

### 1. `iReceiver.sol`

**Purpose:**
- Defines an interface for a contract that can receive messages. This interface ensures that any contract implementing it will have a `receiveMessage` function.

**Functionality:**
- The `IReceiver` interface specifies a single function `receiveMessage` that takes a `string` as an input.

### 2. `MessageReceiver.sol`

**Purpose:**
- Implements the `IReceiver` interface. This contract can receive messages from other contracts, specifically from the `KingdomTreasury` contract.

**Functionality:**
- The `MessageReceiver` contract logs received messages using an event.
- It contains the `receiveMessage` function that emits the `MessageReceived` event when called.

### 3. `BaseTreasury.sol`

**Purpose:**
- Provides basic treasury functionalities that can be inherited by other contracts, such as `KingdomTreasury`.

**Functionality:**
- Contains a function `transferFunds` for transferring Ether from the contract to a specified recipient.
- Includes a function `getTreasuryBalance` to check the contract's balance.
- Emits a `FundTransfer` event whenever funds are transferred.

### 4. `KingdomTreasury.sol`

**Purpose:**
- Manages a treasury for a kingdom-like system where users can become citizens, deposit funds, and withdraw funds. It also allows interaction with other contracts through the `IReceiver` interface.

**Functionality:**
- **Variables:**
  - `king`: The address of the king who has special privileges.
  - `totalFunds`: The total amount of funds in the treasury.
- **Structures:**
  - `Citizen`: Defines a citizen with a balance and a boolean indicating if they are a citizen.
- **Mappings:**
  - `citizens`: Maps addresses to `Citizen` structures.
- **Modifiers:**
  - `onlyKing`: Restricts certain functions to be called only by the king.
  - `onlyCitizen`: Restricts certain functions to be called only by citizens.
- **Constructor:**
  - Sets the deploying address as the king.
- **Functions:**
  - `becomeCitizen`: Allows a user to become a citizen.
  - `deposit`: Allows citizens to deposit funds into the treasury.
  - `withdraw`: Allows citizens to withdraw funds from the treasury.
  - `declareHoliday`: Allows the king to declare a holiday.
  - `getBlockTimestamp`: Returns the current block timestamp.
  - `checkBalance`: Checks the balance of a citizen and categorizes them as "Wealthy" or "Regular".
  - `addCitizenToList`: Adds a citizen to a list, restricted to the king.
  - `getCitizenInfo`: Retrieves the balance and citizenship status of a citizen.
  - `kingdomBalance`: Returns the total balance of the treasury.
  - `callAnotherContract`: Interacts with another contract implementing the `IReceiver` interface to send a message.

## Summary of the System

- **Treasury Management:** The `KingdomTreasury` contract manages funds deposited by citizens, allowing them to deposit and withdraw Ether.
- **Hierarchy and Roles:** The concept of a "king" is implemented, providing special privileges to the deploying address.
- **Inter-contract Communication:** The `KingdomTreasury` contract can send messages to other contracts that implement the `IReceiver` interface, demonstrating inter-contract communication.
- **Modular Design:** The use of interfaces and base contracts (`BaseTreasury`) promotes modularity and reusability of code.

## Use Case Scenarios

1. **Decentralized Organization:** This setup can be used to manage funds in a decentralized organization where members can deposit and withdraw funds, and certain privileged actions are restricted to a leader or a committee.
2. **Game Development:** In a blockchain-based game, this system can manage in-game currency, allowing players to deposit, withdraw, and interact with other game contracts.
3. **DAO Treasury:** It can be used in a Decentralized Autonomous Organization (DAO) where members contribute funds, and the contract ensures fair and transparent management of the treasury.

These contracts demonstrate a simple yet effective system for managing a treasury with roles and inter-contract communication capabilities, suitable for various blockchain applications.
