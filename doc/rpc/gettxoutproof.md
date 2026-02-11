# `gettxoutproof`

Returns the Merkle proof that one or more transactions were included in a block. The proof is returned as a hex-encoded serialized `MerkleBlock`.

## Usage

### Synopsis

```bash
floresta-cli gettxoutproof <txids> [<blockhash>]
```

### Examples

```bash
# Get proof for a single transaction (block is looked up via the watch-only wallet)
floresta-cli gettxoutproof '["4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b"]'

# Get proof for multiple transactions in the same block
floresta-cli gettxoutproof '["txid1", "txid2"]' 000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f
```

## Arguments

`txids` - (JSON array of strings, required) A JSON array of transaction IDs to prove. All transactions must exist in the same block. The value must be a valid JSON array of 64-character hexadecimal transaction hashes.

`blockhash` - (string, optional) The hash of the block to search for the transactions. If omitted, the node uses the first transaction ID to look up the block via the watch-only wallet cache.

## Returns

### Ok Response

- (string) A hex-encoded serialized `MerkleBlock` containing the Merkle proof that the specified transactions were included in the block.

### Error Enum `JsonRpcError`

* `TxNotFound` - One or more of the specified transactions were not found in the block. This also occurs when `blockhash` is omitted and the first transaction is not cached in the watch-only wallet.
* `BlockNotFound` - The specified block hash does not match any known block, or the block containing the transaction could not be retrieved.

## Notes

- All specified transactions must exist in the same block; there is no way to build a common Merkle proof across multiple blocks.
- When `blockhash` is omitted, the node uses the first txid to find the block through the watch-only wallet. This requires the transaction to have been previously cached (e.g. via `loaddescriptor`).
