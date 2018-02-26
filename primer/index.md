**Bitcoin Technology Primer for Developers**

The lifecyle of a Bitcoin transaction begins with a Bitcoin wallet, which has a cryptographic key pair. When the wallet's owner wants to send Bitcoin to another Bitcoin wallet, a transaction record is digitally signed with the wallet's private key. This transaction record includes the amount, plus input and output information. The inputs include references to unspent Bitcoins from previous transactions, or Unspent Transaction Output (UXTO), while the transaction output references the reciever of the amount. When the input amount is larger than the transaction amount, the output can also include a reference to another wallet to send any leftover change to. 

This record is then submitted to a transaction pool within the Bitcoin network for validation, to ensure that the keys used to sign each transaction message match those of the sender, and who therefore owns the coins being transferred. The network consists of distributed computers around the world, called miners, whose job is prioritise and include one or more valid transactions inside larger, fixed size data blocks, which are themselves in turn validated before being added to the network (see Proof of Work). 

Every block has a fixed, maximum size, placing a limit on how many transactions can be included in a block. Miners are incentivised to prioritise and include transactions in blocks by transaction fees, which are calculated as the difference between the inputs less the sum of the transaction amount and returned change. The transaction fee, together with the transaction byte size, will determine how long it will take before a transaction will be included inside a block. If the fee is too small the transaction might not be accepted at all, while bigger fees will provide an incentive for miners to place a higher priority on the transaction.

The structure of a block includes a magic number (always 0xD9B4BEF9), the blocksize, a "body" of transactions, a transaction counter, and a block header. Information from the block header is what is used to validate the block on the network, and contains the following items (data type in brackets): 

* Version number (int32_t)
* Value of the previous block header hash (char[32]), which links the collective linear series of valid blocks in a "blockchain"
* Reference to the Merkle tree of previous transactions (char[32])
* Creation timestamp (int32_t), based on the number of seconds since the generation of the first block in the current set of 2016 blocks
* A difficulty target (int32_t), the threshold below which the hashed block header will be considered valid
* Nonce used to create the block (int32_t)
* [verify: Transaction count, which is always 0 (var_int)].

The acceptance process for adding new blocks to the blockchain ledger involves miners computing hash values of the block header plus an integer value (nonce), until a specific value is found. That value needs to start with a number of zeros, and be lower than or equal to a 256 publically known target that changes over time. This measure is given the name "difficulty", because of the low probability of success using the brute force method to determine the correct answer. The first miner that succeeds in this Proof of Work (PoW) is rewarded with a bounty for "discovering" the block, as well as any related transaction fees associated with its transactions.





