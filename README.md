# Naivecoin

The repository for the naivecoin tutorial: https://lhartikk.github.io/

```
npm install
npm start
```

##### Get blockchain
```
curl http://localhost:3001/blocks
```

##### Mine a block
```
curl -X POST http://localhost:3001/mineBlock
``` 

##### Send transaction
```
curl -H "Content-type: application/json" --data '{"address": "04bfcab8722991ae774db48f934ca79cfb7dd991229153b9f732ba5334aafcd8e7266e47076996b55a14bf9913ee3145ce0cfc1372ada8ada74bd287450313534b", "amount" : 35}' http://localhost:3001/sendTransaction
```

##### Query transaction pool
```
curl http://localhost:3001/transactionPool
```

##### Mine transaction
```
curl -H "Content-type: application/json" --data '{"address": "04bfcab8722991ae774db48f934ca79cfb7dd991229153b9f732ba5334aafcd8e7266e47076996b55a14bf9913ee3145ce0cfc1372ada8ada74bd287450313534b", "amount" : 35}' http://localhost:3001/mineTransaction
```

##### Get balance
```
curl http://localhost:3001/balance
```

#### Query information about a specific address
```
curl http://localhost:3001/address/04f72a4541275aeb4344a8b049bfe2734b49fe25c08d56918f033507b96a61f9e3c330c4fcd46d0854a712dc878b9c280abe90c788c47497e06df78b25bf60ae64
```

##### Add peer
```
curl -H "Content-type:application/json" --data '{"peer" : "ws://localhost:6001"}' http://localhost:3001/addPeer
```
#### Query connected peers
```
curl http://localhost:3001/peers
```


# Notes 

### 1.  Minimal working blockchain
The basic concept of blockchain is a distributed database that maintains a continuously growing list of ordered records with:
* A defined block and blockchain structure
* Methods to add new blocks to the blockchain with arbitrary data
* Blockchain nodes that communicate and sync the blockchain with other nodes
* A simple HTTP API to control the node

#### Block structure
Essential properties include:
* index : The height of the block in the blockchain
* data: Any data that is included in the block.
* timestamp: A timestamp
* hash: A sha256 hash taken from the content of the block.
It is like a unique identifier of the block. We use block hashes to preserve integrity of the block and to explicitly reference the previous block. The deeper the block is in the blockchain, the harder it is to modify it, since it would require modifications to every consecutive block.
* previousHash: A reference to the hash of the previous block. This value explicitly defines the previous block.

### 2.  Proof of Work Algorithm (Mining)
With Proof-of-work we introduce a computational puzzle that needs to be solved, before a block can be added to the blockchain. Trying to solve this puzzle is commonly known as “mining”. Generally in cryptocurrencies, the miner is rewarded for finding a block. The Proof-of-work puzzle is to find a block hash, that has a specific number of zeros prefixing it.
