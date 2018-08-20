# Plasma Cash - ERC721 Version

## Architecture

Client connects to the Child Chain Service, the Root Chain Plasma Contract and the Root Chain Token Contract

Send tx:
Client -> Child Chain Service sendtx -> Child Chain server listens to that request and calls child chain sendtransaction, tx gets added to the block

Child Chain ALWAYS listens for events on the RootChain contract and acts on them accordingly

## Installation

1. In root folder


```
docker-compose build
docker-compose up
```


## Demos

To run demo, execute the integration test script:
```
./integration_test.sh
```

Under `demos/` there are various scenarios which can occur. You should have initialized both the smart contracts from the `server/` directory, and launched a Plasma Chain instance, as described in the corresponding READMEs.

### Demo 1
1. Alice registers and is given coins 1-5
2. Alice deposits `Coin 1`, `Coin 2`, `Coin 3` in the plasma chain
3. 3 Deposit Blocks have been generated in the child chain, each one having 1 UTXO at slots 0,1,2 repsectively
4. Alice sends a Coin 1 to Bob, adding a transaction to the current block.
5. Operator calls submitBlock, checkpointing the block merkle root which includes the transaction that gives ownership to charlie. At this point, both the child chain and the root chain, have checkpointed alice's transaction at block number 1000.
6. Bob transfers the previous UTXO to Charlie and the operator submits that block as well
5. Charlie tries to exit coin 1, Alice & Bob do not challenge
6. After challenge period passes, charlie should be able to withdraw his coin

## Loom SDK integration

To see the integrations run againist the Loom SDK instead of the prototype server


```
cd server
npm install
cd .. 

cd loom_test
make clean
make deps
make

cd ..
./go_integration_test.sh
```

Under the `loom_test` directory there is all the samples in Go, that directly interact with Loom SDK. Usually the SDK is behind our latest research prototypes. As we only move stable Plasma features into the Loom SDK.

## For Developers

### Using monkeypatched web3.py 4.2.1 version for ganache issues
https://github.com/jordanjambazov/web3.py/commit/a61b382dd5c11de1102779868d377408c7590839
Also https://github.com/ethereum/web3.py/pull/827

### Signing locally
http://web3py.readthedocs.io/en/latest/web3.eth.account.html#prepare-message-for-ecrecover-in-solidity


## License info 

Please note different directories have different licenses. Please see license file in each folder respectively

* server directory -> GPLv2 [License](plasma_cash/License.md)
* plasma_cash directory  -> GPLv2 [License](plasma_cash/License.md)
* loom_test directory  -> Loom Public License [License](loom_test/License.md)