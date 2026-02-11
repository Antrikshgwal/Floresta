# `gettransaction`

Returns a transaction cached by the watch-only wallet. Depending on the verbosity flag, the result is either a raw hex-encoded string or a detailed JSON object.

## Usage

### Synopsis

```bash
floresta-cli gettransaction <txid> [<verbose>]
```

### Examples

```bash
floresta-cli gettransaction 4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b

# Returns a detailed JSON object.
floresta-cli gettransaction 4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b true
```

## Arguments

`txid` - (string, required) The transaction ID to look up. The transaction must be cached by the watch-only wallet.

`verbose` - (boolean, optional) Controls the response format. When `true`, the transaction is returned as a detailed JSON object. When `false` a 64-character hex-encoded string is returned.

## Returns

### Ok Response

When `verbose` is `true`, returns a JSON object with the following fields:

- `in_active_chain` - (boolean) Whether the transaction is in the active chain (i.e. has been confirmed).
- `hex` - (string) The raw transaction as a hex-encoded string.
- `txid` - (string) The transaction ID.
- `hash` - (string) The witness transaction ID (wtxid).
- `size` - (numeric) The serialized transaction size in bytes.
- `vsize` - (numeric) The virtual transaction size in vbytes.
- `weight` - (numeric) The transaction weight in weight units.
- `version` - (numeric) The transaction version number.
- `locktime` - (numeric) The transaction lock time.
- `vin` - (array) An array of transaction inputs, each containing:
  - `txid` - (string) The previous output transaction ID.
  - `vout` - (numeric) The previous output index.
  - `script_sig` - (object) The input script, with `asm` and `hex` fields.
  - `sequence` - (numeric) The input sequence number.
  - `witness` - (array) An array of hex-encoded witness data strings.
- `vout` - (array) An array of transaction outputs, each containing:
  - `value` - (numeric) The output value in satoshis.
  - `n` - (numeric) The output index.
  - `script_pub_key` - (object) The output script, with `asm`, `hex`, `req_sigs`, `type`, and `address` fields.
- `blockhash` - (string) The hash of the block containing the transaction.
- `confirmations` - (numeric) The number of confirmations (0 if unconfirmed).
- `blocktime` - (numeric) The block timestamp as a UNIX epoch time.
- `time` - (numeric) The transaction time as a UNIX epoch time (same as `blocktime`).

When `verbose` is `false`, returns a 64-character hex-encoded string representing the raw transaction.


### Error Enum `JsonRpcError`

* `TxNotFound` - The transaction was not found in the watch-only wallet cache.

## Notes

- Only transactions cached by the watch-only wallet can be retrieved. You must first load descriptors with `loaddescriptor` so the wallet knows which addresses to track.
- The CLI always requests verbose output regardless of the `verbose` argument passed.