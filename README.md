# betting-app

> Bet on a sport event without loosing your stake and get rewarded if you win.
 
## Features

- Sport event betting app 
- No-loss: Players can choose to withdraw their stake whatever the outcome (whether they win or loose)
- Winners rewards comes from part of the accrued interests invested in DeFi (pro-rated) 
- Ethereum Blockchain based

## Description

- Period 1  (Bet)
Players bet on a sport event.
- Period 2 (Earn)
    - The total amount of bets (all players included) is then staked in DeFi.  
    - The sport event occurs
    - The oracle makes the event outcome available.
- Period 3 (Distribution)
    - betting-app withdraws the interests accrued in DeFi, substracts the platform fees.
    - The remaining can be split between winners according to their share in the total deposit value.

Each winner can then withdraw his/her interests proportionally to his/her initial stake.  
Each player can also withdraw his/her stake.

## Architecture

betting-app software is composed of 2 parts:
- **Back-End**:  
The **Ethereum smart-contracts** deployed on the testnets. They are written in Solidity.
- **Front-End** (DApp):  
A **ReactJS client app** written in ReactJS and deployed on Heroku. 
It  provides the User Interface to interact with the contracts.

This Github **repository** is a **monorepo** that entails **both** the **back-end and** the **front-end** code.

### Back-End

The back-end is composed of the following Ethereum **smart-contracts**:

- [`DAI`](contracts/DAI.sol) 
- [`Bet`](contracts/Bet.sol) The betting contract in charge of:
    - handling the bets: deposit/withdrawal
    - getting the list of events from *Oracle*
    - sending all deposits for a given bet to *DeFi* to earn
    - withdraw and get accrued interests from `DeFiPool`
    - Allow winners to withdraw their prizes
    - Allow all players to withdraw their stake
- [`BetOracle`](contracts/BetOracle.sol) A *simulated* smart-contract that:
    - registers events
    - provides the events list
    - Get the outcome of registered events
    - provides the outcome of an event when asked for
- [`DefiPool`](contracts/DefiPool.sol) A smart-contract in charge of simulating a DeFi protocol that accepts deposits and allow withdrawal with accrued interests.

### Front-End

Our **DApp** is a **Front-End** application written in **ReactJS** and deployed on Heroku.


# Compile

```
npx truffle compile
```

# Test

[This page](doc/tests_explication.md) explains **what we test and how**.

```
# Run ganache on port 9545 beforehand
npx truffle deploy --network ganache

npx truffle test # Run the unit and integration tests
```

# Gas Report

To get a report of the gas consumed by the smart-contracts while running the tests.
```
npm run gas
```

Read more about the [eth-gas-reporter](https://github.com/cgewecke/eth-gas-reporter) npm package we use to generate gas reports.


# Deploy 

You need to deploy both the smart-contracts (back-end) and the ReactJS app - DApp (front-end).

## Deploy Back-End

The **smart-contracts** are deployed in the following order:  
1. `DAI`
2. `Bet`
3. `BetOracle`
4. `DeFiPool`


### Deploy Dev
```
# Local Deploy
npx truffle deploy --network=ganache
```

### Deploy on a Test Network
```
# Deploy the contracts on the ropsten test network
npx truffle deploy --network=ropsten
```

# Run

- Run the **local** DApp:  
In order to run the Front-End application on your local machine:
    ```
    cd client 
    npm start
    ```

# Open the App

- Open the **local** DApp: https://localhost:3000/ 
