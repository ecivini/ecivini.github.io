+++
author = "Emanuele Civini" 
title = "GasBad - Comparing gas efficiency of Solidity libraries" 
date = 2023-06-03
tags = ["solidty", "gas", "evm"]
+++

GasBad is a project aimed at comparing the gas efficiency of various Solidity libraries. It focuses on analyzing and measuring the gas consumption of popular Solidity libraries to identify which ones offer the most efficient gas usage.

## Why GasBad?

Gas consumption is a critical factor in Ethereum smart contract development. Efficient gas usage not only helps optimize transaction costs but also contributes to scalability and overall contract performance. GasBad aims to provide developers with insights into the gas efficiency of different Solidity libraries, allowing them to make informed decisions when choosing libraries for their projects.

## What did you test?

Currently, GasBad focuses on testing (**only**) the gas usage of the following Solidity libraries:

- OpenZeppelin: A widely-used library for secure and community-audited smart contract development.
- Solady: A Solidity library known for its gas optimization techniques and efficiency enhancements.
- Solmate: A library specifically designed to provide gas-efficient implementations of common Solidity operations.

## How did you test?

GasBad conducts gas efficiency tests using Forge 0.2.0 with via-IR optimizations and Solidity 0.8.20. The Forge framework allows for precise gas measurement and analysis of Solidity code.

## What are the results?

GasBad evaluates the gas efficiency of libraries across different contracts.
This is a snapshot of what has been tested as of March 2024, in the [Github repository](https://github.com/ecivini/gas-bad) you'll always find the updated results.

### ERC20

Gas consumption evaluation of ERC20 token-related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for ERC20 functionality.

| Function Name | Solmate | Solady | OpenZeppelin | Gas Efficiency |
|---------------|--------------|-------------|------------------|-----------|
| allowance     | 808          | 768         | 788              | Solady    |
| approve       | 24310        | 24268       | 24387            | Solady    |
| decimals      | 265          | 257         | 262              | Solady    |
| name          | 2901         | 529         | 2823             | Solady    |
| symbol        | 3083         | 738         | 2985             | Solady    |
| totalSupply   | 2321         | 2319        | 2324             | Solady    |
| transfer      | 29567        | 29541       | 29666            | Solady    |
| transferFrom  | 20234        | 20021       | 21828            | Solady    |

### ERC721

Gas consumption evaluation of ERC721 token-related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for ERC721 functionality.

| Function Name   | Solmate | Solady | OpenZeppelin | Gas Efficiency |
|-----------------|---------|--------|--------------|----------------|
| approve         | 22667   | 22444  | 23030        | Solady         |
| balanceOf       | 2663    | 2618   | 2663         | Solady         |
| burn            | 4234    | 4181   | 4511         | Solady         |
| getApproved     | 412     | 545    | 699          | Solmate        |
| isApprovedForAll| 2915    | 2807   | 2915         | Solady         |
| mint            | 46894   | 46678  | 47149        | Solady         |
| name            | 2928    | 549    | 565          | Solady         |
| setApprovalForAll| 24602  | 24477  | 24626        | Solady         |
| symbol          | 3134    | 747    | 768          | Solady         |
| tokenURI        | 850     | 835    | 850          | Solady         |
| transferFrom    | 22515   | 20319  | 23352        | Solady         |

### ERC1155

Gas consumption evaluation of ERC1155 token-related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for ERC1155 functionality.

| Function Name   | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|-----------------|-----------|---------------|----------------|----------------|
| balanceOf       | 2547      | 2407          | 2485           | Solady  |
| balanceOfBatch  | 16106     | 12566         | 14317          | Solady  |
| burn            | 8784      | 8064          | 8156           | Solady  |
| burnBatch       | 36684     | 33635         | 35648          | Solady  |
| isApprovedForAll| 778       | 681           | 783            | Solady  |
| mint            | 28155     | 27712         | 27871          | Solady  |
| mintBatch       | 124178    | 121891        | 124104         | Solady  |
| safeBatchTransferFrom | 151145 | 146637    | 148209         | Solady  |
| safeTransferFrom | 34027    | 33141         | 33458          | Solady  |
| setApprovalForAll | 24506   | 24367         | 24487          | Solady  |
| uri             | 2945      | 540           | 566            | Solady  |

### ERC4626

Gas consumption evaluation of ERC4626 vault-related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for ERC4626 functionality.

| Function Name   | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|-----------------|-----------|---------------|----------------|----------------|
| balanceOf       | 756       | 705           | 707            | Solady |
| convertToAssets | 1544      | 1286          | 361 - 1424     | Solmate if totalSupply is zero else Solady |
| deposit         | 62699     | 60093         | 59628          | Solmate        |
| mint            | 62802     | 60199         | 59652          | Solmate        |
| name            | 2886      | 2840          | 2922           | Solady         |
| previewDeposit  | 2119      | 1875          | 1972           | Solady         |
| previewWithdraw | 1666      | 1396          | 1497           | Solady         |
| redeem          | 24849     | 23901         | 23944          | Solady         |
| symbol          | 3226      | 3195          | 3252           | Solady         |
| totalAssets     | 1139      | 912           | 1133           | Solady         |
| totalSupply     | 383       | 380           | 380            | Solmate/Solady | 
| withdraw        | 25958     | 24792         | 23922          | Solmate        |

### Ownable

Gas consumption evaluation of Ownable related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for this functionality.

| Function Name     | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|-------------------|---------------|------------------|--------------------|----------------|
| owner             | 2298          | 2355             | 2279               | Solmate      |
| renounceOwnership | 5486          | 5472             | -                  | Solady  |
| transferOwnership | 6955          | 7002             | 6785               | Solmate |

### RoleBasedAccess

Gas consumption evaluation of RoleBasedAccess contracts related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for this functionality.

> Note: *In order to be specific, it uses the following contracts for comparisons:*
> 1. **AccessControl.sol** from Openzeppelin
> 2. **OwnableRoles** from Solady
> 3. **RolesAuthority** from Solmate
> 

| Function Name     | OpenZeppelin | Solady            | Solmate            | Gas Efficiency |
|-------------------|---------------|------------------|--------------------|----------------|
| owner             | 2363          | 2546             | 2444               | OpenZeppelin   |
| grantRole         | 29178         | 26096            | 18915              | Solmate        |
| revokeRole        | 7146          | 6323             | 18915              | Solady         |

### ECDSA

Gas consumption evaluation of ECDSA related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for this functionalities.

| Function Name   | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|-----------------|-----------|---------------|----------------|----------------|
| recover       | 3935      | 3741          | -           | Solady  |
| toEthSignedMessage  | 252     | 255         | -          | OpenZeppelin  |

### MerkleProof

Gas consumption evaluation of  contracts related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for this functionality.

> Note: *As gas consumption of **verify** function depends on proof size there are several tests for each function with different amounts of elements in proof and corresponding amount of leaves (elements in tree)*
> 1. 5 elements in the proof = 32 leaves in tree
> 2. 10 elements in the proof = 1024 leaves in tree
> 3. 15 elements in the proof = 32668 leaves in tree

| Function Name              | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|----------------------------|-----------|---------------|----------------|----------------|
| verify_5_elements          | 2554      | 1783          | -              | Solady         |
| verify_10_elements         | 4444      | 2863          | -              | Solady         |
| verify_15_elements         | 6340      | 3943          | -              | Solady         |
| verifyCalldata_5_elements  | 1685      | 1204          | 1095           | Solmate        |
| verifyCalldata_10_elements | 2916      | 1929          | 1820           | Solmate        |
| verifyCalldata_15_elements | 4159      | 2654          | 2545           | Solmate        |

### Base64

Gas consumption evaluation of Base64 related operations provided by the tested libraries. By comparing gas usage, developers can make informed decisions about the most efficient library for this functionality.

| Function Name     | OpenZeppelin | Solady | Solmate | Gas Efficiency |
|-------------------|---------------|------------------|--------------------|----------------|
| encode             | 2599          | 1925             | -               | Solady      |
| decode             | -          | 1786             | -                  | Solady  |

## Can I add other tests?

Yes, of course! You can create an issue in the [Github repository](http://localhost:1313/post/gas-bad/) and explain what you'd like to see. I'll be more than happy to add it to this collection and perform the necessary tests.

Alternatively, if you have already conducted gas efficiency tests and want to share your results, you can create a pull request (PR) on the repository. Once your PR is submitted, I will review and integrate it into the project, making it accessible to everyone.
