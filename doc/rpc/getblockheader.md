# `getblockheader`

Returns the block header for the given block hash. A header contains the block's version, previous block hash, Merkle root, timestamp, difficulty target, and nonce.

## Usage

### Synopsis

```bash
floresta-cli getblockheader <hash>
```

### Examples

```bash
floresta-cli getblockheader 00000000000000000001a2f0b80b5eeb24fd80984e97869ad25b6abb4ff8a025
```

## Arguments

`hash` - (string, required) The hash of the block to retrieve the header for, in hex format.

## Returns

### Ok Response

- `version` - (numeric) The block version number.
- `prev_blockhash` - (string) The hash of the previous block in the chain.
- `merkle_root` - (string) The merkle root of all transactions in the block.
- `time` - (numeric) The block timestamp as a UNIX epoch time.
- `bits` - (numeric) The compressed difficulty target for the block.
- `nonce` - (numeric) The nonce used to generate this block.

### Error Response

* `BlockNotFound` - The block hash provided does not match any known block.
* `InvalidParameterType` - The hash parameter is not a valid block hash.