# Getting Started with Blockchain

This is a simple Blockchain application build on flash server. Implemented through various basics learnt on web.

### 1) Basics
Blockchain is an immutable, sequential chain of records called Blocks. They can contain transactions, files or any data you like, really. But the important thing is that they’re chained together using hashes.

### 2) A block
Each Block has an index, a timestamp (in Unix time), a list of transactions, a proof (more on that later), and the hash of the previous Block.

### 3) Creating new Blocks
When our Blockchain is instantiated we’ll need to seed it with a genesis block—a block with no predecessors. We’ll also need to add a “proof” to our genesis block which is the result of mining (or proof of work). 

### 4) Proof of Work Algorithm (PoW)
A Proof of Work algorithm (PoW) is how new Blocks are created or mined on the blockchain. The goal of PoW is to discover a number which solves a problem. The number must be difficult to find but easy to verify—computationally speaking—by anyone on the network. This is the core idea behind Proof of Work.

Eg: Let’s decide that the hash of some integer x multiplied by another y must end in 0. So, hash(x * y) = ac23dc...0. And for this simplified example, let’s fix x = 5. Implementing this in Python:

~~~~
from hashlib import sha256
x = 5
y = 0  # We don't know what y should be yet...
while sha256(f'{x*y}'.encode()).hexdigest()[-1] != "0":
    y += 1
print(f'The solution is y = {y}')
~~~~

The solution here is ~~~~ y = 21 ~~~~. Since, the produced hash ends in 0:

~~~~
hash(5 * 21) = 1253e9373e...5e3600155e860
~~~~

In Bitcoin, the Proof of Work algorithm is called Hashcash. And it’s not too different from our basic example above. It’s the algorithm that miners race to solve in order to create a new block. In general, the difficulty is determined by the number of characters searched for in a string. The miners are then rewarded for their solution by receiving a coin—in a transaction.

The network is able to easily verify their solution.

### The Mining Endpoint
Our mining endpoint is where the magic happens, and it’s easy. It has to do three things:

1) Calculate the Proof of Work
2) Reward the miner (us) by adding a transaction granting us 1 coin
3) Forge the new Block by adding it to the chain