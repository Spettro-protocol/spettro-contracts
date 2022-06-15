# spettro-contracts
Smart contracts for Spettro protocol.

## Install Dependencies

1.  Copy `.env.example` file and change its name to `.env` in the project folder
2.  Create `/typechain` folder in root folder and place there emplty `.ts` file
3.  Run `yarn` to install all dependencies

## Compile Contracts

`yarn compile`

## Test Vault.sol Contract

Run `yarn test:pancakev202mcv2` and `yarn test:pancakev202mcv2:cake-vault` test

## Deployment

Make sure you [funded](https://testnet.binance.org/faucet-smart) your deployer address on BSC testnet

### Vault.sol

First you need to deploy dependencies, Timelock.sol `yarn deploy:testnet:timelock:deploy:timelock` and WNativeRelayer.sol `yarn deploy:testnet:005`, note deployed addresses and edit corresponding values Timelock and WNativeRelayer addresses in [.testnet.json](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/.testnet.json) file.
Finally run `yarn deploy:testnet:vault:deploy:vault` to deploy Vault.sol

### AutomatedVaultController.sol

Run `yarn deploy:testnet:AVController`

## BSC Scan verification

Make sure you filled out your API key in .env file.
Run `npx hardhat verify --network testnet --contract solidity/contracts/6/Timelock.sol:Timelock 0x0A0CC5340b22e810028e2c64e319Ec9cef22042d 0xAc0b88472AFF494870678ef09046DD90214E987c 8640` for each contract you wish to verify with correspondent values.
--contract is fully qualified name of the contract, then goes the address and last arguements is array of constructor parameters (if there are any)

## Deployment && Testnet BSC Scan links to verified contracts

### [Vault.sol](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/solidity/contracts/6/protocol/Vault.sol)

- [Vault](https://testnet.bscscan.com/address/0x065c0393933d40a7546da0e9fc9f9398376e4645#code) (TransparentUpgradeableProxy), [Logic](https://testnet.bscscan.com/address/0xd28c4ecdfcd00dbd6e7871a8f212393012ad1b86#code)

#### Dependencies

- [Timelock](https://testnet.bscscan.com/address/0x0A0CC5340b22e810028e2c64e319Ec9cef22042d#code)
- [WNativeRelayer](https://testnet.bscscan.com/address/0x33daa992F8aaBd57a67669d673c939d067A9ABd5#code)
- [debtibWBNB_V2](https://testnet.bscscan.com/token/0xC76B4C3147D855241e8EFeDaf0750F3b16490242) (TransparentUpgradeableProxy), [Logic](https://testnet.bscscan.com/address/0xbb6ea04d8960415ace0324846c1481b38e434dbd#code)

### [AutomatedVaultController.sol](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/solidity/contracts/8.13/AutomatedVaultController.sol)

- [AutomatedVaultController](https://testnet.bscscan.com/address/0xa2f1f86e6836e4c08eb1e61f3ca4c79725d9fcee#code) (TransparentUpgradeableProxy), [Logic](https://testnet.bscscan.com/address/0xfb7eaab26b1307265d83dfdcb578471eeb5f18da#code)

## Vault smart contract tests in forked network

### [Vault_PancakeswapV2MCV2Worker02.test.ts](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts)

```
yarn test:pancakev202mcv2
```

#### References to requested methods to test

- [deposit](https://github.com/mnusurov/bsc-alpaca-contract/blob/ed0502cc30e8bf4a308093d703a8327c9d0f6355/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts#L460)
- [withdraw](https://github.com/mnusurov/bsc-alpaca-contract/blob/ed0502cc30e8bf4a308093d703a8327c9d0f6355/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts#L1674)
- [addCollateral](https://github.com/mnusurov/bsc-alpaca-contract/blob/ed0502cc30e8bf4a308093d703a8327c9d0f6355/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts#L2377)
- [work](https://github.com/mnusurov/bsc-alpaca-contract/blob/ed0502cc30e8bf4a308093d703a8327c9d0f6355/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts#L523)
- [kill](https://github.com/mnusurov/bsc-alpaca-contract/blob/ed0502cc30e8bf4a308093d703a8327c9d0f6355/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02.test.ts#L1356)

![alt text](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/pancakev202mcv2.png?raw=true)

### [Vault_PancakeswapV2MCV2Worker02.test.ts](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/test/integrations/protocol/workers/pcs/Vault_PancakeswapV2MCV2Worker02_Cake.test.ts)

```
yarn test:pancakev202mcv2:cake-vault
```

![alt text](https://github.com/mnusurov/bsc-alpaca-contract/blob/main/pancakev202mcv2-cake-vault.png?raw=true)

# Alpaca Contract

**Leveraged yield farming on BNB Chain and Fantom chain**

## Local Development

The following assumes the use of `node@>=14`.

### Install Dependencies

1.  Copy `.env.example` file and change its name to `.env` in the project folder
2.  Run `yarn` to install all dependencies

### Compile Contracts

`yarn compile`

Note: There will be a new folder called `typechain` generated in your project workspace. You will need to navigate to `typechain/index.ts` and delete duplicated lines inside this file in order to proceed.

### Run Tests with hardhat

`yarn test`

## Testing with Forge

### Install Forge

```
$ curl -L https://foundry.paradigm.xyz | bash # install foundryup
$ foundryup # install forge and cast
```

### Test

```
$ forge test
```

## Licensing

The primary license for Alpaca Protocol is the MIT License, see [MIT LICENSE](https://github.com/alpaca-finance/bsc-alpaca-contract/blob/main/LICENSE).

Exceptions

- Single Asset LYF: `solidity/contracts/6/protocol/workers/CakeMaxiWorker.sol` and all files in `solidity/contracts/6/protocol/strategies/pancakeswapV2-restricted-single-asset` are licensed under Business Source License 1.1 (`BUSL-1.1`) (as indicated in their SPDX headers), see [BUSL-1.1](https://github.com/alpaca-finance/bsc-alpaca-contract/blob/main/LICENSE_BUSL-1.1)
- Delta Neutral Vault: All files that match `DeltaNeutral*.sol` and `solidity/contracts/8.13/protocol/AutomatedVaultController.sol`, `solidity/contracts/8.13/protocol/xALPACACreditor.sol` are licensed under Business Source License 1.1 (`BUSL-1.1`) (as indicated in their SPDX headers), see [BUSL-1.1](https://github.com/alpaca-finance/bsc-alpaca-contract/blob/main/LICENSE_BUSL-1.1)
- All files in `tests` remain unlicensed.
