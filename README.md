# cocoon

Contract to store your ETH on chain.

### Disclaimer: This hasn't been audited, and has only undergone happy path testing. Consider this a proof of concept.

### Note: A multisig wallet might be a better fit for your needs.

#### Introduction

Storing your ETH on an exchange is considered risky because the exchange could get hacked or lock you out of your own account at any point of time. The use of hardware wallets or paper wallets is recommended to store ETH or other cryptocurrencies. Paper and HW wallets come with their own risks as they could be stolen, lost, burned etc. and protecting them takes quite effort.

Cocoon is a contract that helps you store your ETH on the blockchain and requires you to control 2 of 3 addresses associated with the contract to be able to withdraw funds. If one of your private keys is stolen the thief cannot get access to your funds. In the meantime you can withdraw your funds using the other two private keys.

#### How it works

- `storeInContract(address intermediary, address receiver) payable`

When you store ETH in the contract you pass two addresses `intermediary` and `receiver`. The address from where you sent the ETH is the `initiator`. These three address together form a triple of (initiator, intermediary, receiver).

`initiator` can be a hardware wallet that you own. You will use this to add more ETH to the contract.

- `sendToReceiver(address intermediary, address receiver, uint amount)`

This function is to move your ETH from the contract to the `receiver` and has to be called from the `initiator`. You can get your ETH out of the contract using this function even if the intermediary is compromised.

- `moveToReceiver(address initiator, address receiver, uint amount)`
- `moveToInitiator(address initiator, address receiver, uint amount)`

These can be called from the intermediary to move ETH to the `initiator` or `receiver` if one of them is compromised.
