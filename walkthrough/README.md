#### Start a private chain on geth

```sh
geth --dev
```
![start_geth_with_dev_option](https://user-images.githubusercontent.com/10276811/26889691-8c803ed6-4bcc-11e7-8d23-9f1508e3a105.png)
---

### Open another terminal to execute the following commands:

#### Create 4 accountsand unlock them to allow transactions

```javascript
// Create four accounts and unlock them
// Choose a strong password if you're working with real ETH
personal.newAccount('pw')
personal.newAccount('pw')
personal.newAccount('pw')
personal.newAccount('pw')

// DO NOT DO THIS WHEN YOU'RE WORKING WITH REAL ETH
personal.unlockAccount(eth.accounts[0], 'pw', 0)
personal.unlockAccount(eth.accounts[1], 'pw', 0)
personal.unlockAccount(eth.accounts[2], 'pw', 0)
personal.unlockAccount(eth.accounts[3], 'pw', 0)
```
![create_new_accounts](https://user-images.githubusercontent.com/10276811/26889682-8c483298-4bcc-11e7-939a-7684add86d75.png)
![unlock_accounts](https://user-images.githubusercontent.com/10276811/26889694-8ca5efc8-4bcc-11e7-9248-20c068f21334.png)
---

#### Start mining

```javascript
miner.start(1)
```
![start_mining](https://user-images.githubusercontent.com/10276811/26889692-8c879d70-4bcc-11e7-8811-c867562a274d.png)

Output in the first terminal:
![mining_output](https://user-images.githubusercontent.com/10276811/26889685-8c4f780a-4bcc-11e7-94db-4a272dd16150.png)

#### Initialize some variables

```javascript
// For our reference
var initiator = eth.accounts[1];
var intermediary = eth.accounts[2];
var receiver = eth.accounts[3];
var one_eth = web3.toWei(1, 'ether');

// Helper function to display balance of each account in the contract triple
function getBalances() {
    console.log('Initiator: ', web3.fromWei(eth.getBalance(initiator), 'ether'));
    console.log('Intermediary: ', web3.fromWei(eth.getBalance(intermediary), 'ether'));
    console.log('Receiver: ', web3.fromWei(eth.getBalance(receiver), 'ether'));
}
getBalances();
```
![initialize_variables](https://user-images.githubusercontent.com/10276811/26889684-8c49fa2e-4bcc-11e7-9d79-85a1a28809f2.png)
---

#### Deploy the contract

Wait till you see the message "Contract mined........"

```javascript
var cocoon_sol_cocoonContract = web3.eth.contract([{"constant":false,"inputs":[{"name":"intermediary","type":"address"},{"name":"receiver","type":"address"}],"name":"storeInContract","outputs":[],"payable":true,"type":"function"},{"constant":false,"inputs":[{"name":"initiator","type":"address"},{"name":"receiver","type":"address"},{"name":"amount","type":"uint256"}],"name":"moveToInitiator","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"initiator","type":"address"},{"name":"intermediary","type":"address"},{"name":"receiver","type":"address"}],"name":"getValue","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"intermediary","type":"address"},{"name":"receiver","type":"address"},{"name":"amount","type":"uint256"}],"name":"sendToReceiver","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"initiator","type":"address"},{"name":"receiver","type":"address"},{"name":"amount","type":"uint256"}],"name":"moveToReceiver","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"initiator","type":"address"},{"name":"intermediary","type":"address"},{"name":"receiver","type":"address"},{"name":"target","type":"address"},{"name":"amount","type":"uint256"}],"name":"sendToTarget","outputs":[],"payable":false,"type":"function"}]);
var cocoon_sol_cocoon = cocoon_sol_cocoonContract.new(
   {
     from: web3.eth.accounts[0], 
     data: '0x6060604052341561000c57fe5b5b6106d68061001c6000396000f30060606040523615610076576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680632c0e385014610078578063a2a746e1146100c5578063b709df1114610123578063bca6e8ec146101ab578063dac84ee414610209578063dd47fe1514610267575bfe5b6100c3600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff16906020019091905050610303565b005b34156100cd57fe5b610121600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff169060200190919080359060200190919050506103cf565b005b341561012b57fe5b610195600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff169060200190919050506103e2565b6040518082815260200191505060405180910390f35b34156101b357fe5b610207600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff169060200190919080359060200190919050506104a8565b005b341561021157fe5b610265600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff169060200190919080359060200190919050506104bb565b005b341561026f57fe5b610301600480803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff1690602001909190803573ffffffffffffffffffffffffffffffffffffffff169060200190919080359060200190919050506104ce565b005b34600060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825401925050819055505b5050565b6103dc83338486856104ce565b5b505050565b6000600060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205490505b9392505050565b6104b533848485856104ce565b5b505050565b6104c883338485856104ce565b5b505050565b80600060008773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410151561069c5780600060008773ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825403925050819055508173ffffffffffffffffffffffffffffffffffffffff166108fc829081150290604051809050600060405180830381858888f19350505050151561069757fe5b6106a2565b60006000fd5b5b50505050505600a165627a7a723058200d68074b074e81e469f8704851969044edce3b889e14c8a6dac03f5290bc5b480029', 
     gas: '4700000'
   }, function (e, contract){
    console.log(e, contract);
    if (typeof contract.address !== 'undefined') {
         console.log('Contract mined! address: ' + contract.address + ' transactionHash: ' + contract.transactionHash);
    }
 })
```
![deploy_contract](https://user-images.githubusercontent.com/10276811/26889683-8c49da9e-4bcc-11e7-962a-36634c060fc9.png)
---

#### Send some ETH to the initiator to get started

```javascript
// Transfer 5 ETH from the cionbase to the initiator
// The coinbase account (where the mined coins are present) is used to seed the initiator with 5 ETH
eth.sendTransaction({from: eth.coinbase, to: initiator, value: one_eth * 5});

var l = cocoon_sol_cocoon;
```
![seed_initiator](https://user-images.githubusercontent.com/10276811/26889690-8c7ae936-4bcc-11e7-927b-780600f9bca5.png)
---

#### Store ETH in the contract

```javascript
l.storeInContract(intermediary, receiver, {from: initiator, value: one_eth * 5});
l.getValue(initiator, intermediary, receiver);
getBalances();
```
![store_in_contract](https://user-images.githubusercontent.com/10276811/26889693-8c8df27e-4bcc-11e7-912b-1e55f5ad3da6.png)
---

#### Send ETH to `receiver` -- called by the `initiator`

```javascript
l.sendToReceiver(intermediary, receiver, one_eth, {from: initiator});
l.getValue(initiator, intermediary, receiver);
getBalances();
```
![send_to_receiver](https://user-images.githubusercontent.com/10276811/26889689-8c79a602-4bcc-11e7-9cb0-0c8817f44d41.png)
---

#### Send ETH to `receiver` -- called by the `intermediary`

```js
l.moveToReceiver(initiator, receiver, one_eth, {from: intermediary});
l.getValue(initiator, intermediary, receiver);
getBalances();
```
![move_to_receiver](https://user-images.githubusercontent.com/10276811/26889687-8c57ee0e-4bcc-11e7-9f34-446dfc68595c.png)
---

#### Send ETH to `initiator` -- called by the `intermediary`

```js
l.moveToInitiator(initiator, receiver, one_eth, {from: intermediary});
l.getValue(initiator, intermediary, receiver);
getBalances();
```
![move_to_initiator](https://user-images.githubusercontent.com/10276811/26889686-8c54a9a6-4bcc-11e7-8289-86cf9d7e0962.png)
