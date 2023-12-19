# Token Smart Contract 

## Overview

This Solidity smart contract implements a basic ERC-20 token with additional functionalities, such as minting, burning, and ownership management. The contract is named "Token" with the symbol "TK."

## Features

1. **Minting Tokens:**
   - The contract allows the owner (creator) to mint new tokens and assign them to a specified address (cashier).
   - This feature is restricted to the owner for control over token supply.

2. **Burning Tokens:**
   - Token holders can burn a certain amount of their own tokens, effectively reducing the total supply.
   - Burning tokens is initiated by the token holder, enhancing flexibility in managing token balances.

3. **Transferring Tokens:**
   - The standard ERC-20 `transfer` function is extended to provide additional details through the `TokensTransferred` event.
   - Token transfers can be executed between any two addresses.

4. **Ownership:**
   - The contract is inherited from the OpenZeppelin `Ownable` contract, ensuring that certain functions are restricted to the contract owner.

## Deployment

The contract is deployed with initial token supply and ownership. The owner address is provided during deployment, and 150 tokens are minted to the owner's address.

## Usage

### Minting Tokens

The owner can mint new tokens by calling the `mintTokens` function, providing the address of the recipient (cashier) and the number of tokens to be minted.

```solidity
function mintTokens(address cashier, uint256 sentTokens) external onlyOwner {
    _mint(cashier, sentTokens);
    emit TokensMinted(cashier, sentTokens);
}
```

### Burning Tokens

Token holders can burn their own tokens by calling the `burnTokens` function, specifying the amount of tokens to be burned.

```solidity
function burnTokens(uint256 Burned_tokens) external {
    _burn(_msgSender(), Burned_tokens);
    emit TokensBurned(_msgSender(), Burned_tokens);
}
```

### Transferring Tokens

Token transfers between addresses can be initiated using the standard ERC-20 `transfer` function, which has been extended to emit the `TokensTransferred` event.

```solidity
function transferTokens(address Cashier, uint256 Transfered_tokens) public returns (bool) {
    _transfer(_msgSender(), Cashier, Transfered_tokens);
    emit TokensTransferred(_msgSender(), Cashier, Transfered_tokens);
    return true;
}
```

## Events

The contract emits three events:

1. `TokensMinted`: Triggered when new tokens are minted.

2. `TokensBurned`: Triggered when tokens are burned.

3. `TokensTransferred`: Triggered when tokens are transferred between addresses.

 ## Author 

Syed Owaiz

## License

This smart contract is released under the MIT License. See the [LICENSE](LICENSE) file for details.
