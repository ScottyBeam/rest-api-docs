# Populate teleport approves

Get transaction data that is necessary to make teleport transactions.  
Transactions are executed on a source chain.  
Returns `[]`, if no approve required.

```
 POST /v0.1/nft/teleports/populate/approves
```

## Request Body

Name              | Required | Type     | Description
------------------|----------|----------|-----------------
wallet            | True     | String   | The wallet address that signs the transaction.
chain_id          | True     | Int      | The ChainId this transaction is authorized on.
assets            | True     | string[] | Unique Nft contract addresses. Max length - 5.

### Example
```
 POST /v0.1/nft/teleports/populate/approves
```

```json
{
    "chain_id": 1,
    "wallet": "0xD9761da7e6d79274D9495F2B1686A652E4104F15",
    "assets": ["0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b"]
}
```

## Responses
Name            | Type           | Description
----------------|----------------|------
200 OK          | AssetApprove[] | OK
400 Bad Request | Error          | See the request requirements.
422 Unprocessable Entity | Error | Unsupported token.

See also [Errors Codes](errors.md).

### Example
```json
[
   {
      "asset":"0xf5de760f2e916647fd766b4ad9e85ff943ce3a2b",
      "tx":{
         "data":"0xa22cb4650000000000000000000000006653113789c42430163e20318624ef12b137f4660000000000000000000000000000000000000000000000000000000000000001",
         "to":"0xf5de760f2e916647fd766B4AD9E85ff943cE3A2b",
         "from":"0xd9761da7e6d79274d9495f2b1686a652e4104f15",
         "value":"0"
      }
   }
]
```

## Definitions

`AssetApprove`

Name  | Type        | Description
------|-------------|-----------------------
asset | String      | An asset.
tx    | Transaction | A transaction request.

`Transaction`

Name  | Type   | Description
------|--------|-----
from  | String | The transaction from.
to    | String | The transaction to (Nft asset).
data  | String | The transaction data.
value | String | The amount (in wei) this transaction is sending.
