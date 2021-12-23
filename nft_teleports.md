# Teleports - List

Get all teleports.

```
 GET /v0.1/nft/teleports
```

With optional parameters:

```
 GET /v0.1/nft/teleports?wallet={wallet}&only_interactable={only_interactable}&order={order}&limit={limit}&tx_hash_start={tx_hash_start}&chain_id_from={chain_id_from}&chain_id_to={chain_id_to}&include_asset={include_asset}
```

## Query Parameters

Name              | Required | Type | Description
------------------|-------| -------|-----
wallet            | False | String | Start transaction sender or recipient.
only_interactable | False | Boolean| Include only interactable teleports (claimable or cancellable). Default - false.
order             | False | Order  | List order. Default - asc.
limit             | False | Int    | Max length for returned list. Default - 10. Max - 100.
tx_hash_start     | False | String | Transaction hash in teleport start.
chain_id_from     | False | Int    | ChainId in teleport start.
chain_id_to       | False | Int    | ChainId in teleport finish.
include_asset     | False | Boolean| Include asset and token info. Default - false.

### Example
```
 GET /v0.1/nft/teleports?only_interactable=true&order=desc&limit=1&chain_id_start=1&chain_id_finish=56&include_asset=true
```

## Responses
Name | Type | Description
------|------|------
200 OK | Teleport[] |OK
400 Bad Request | Error | See the request requirements.

See also [Errors Codes](errors.md).

### Example
```json
[
   {
      "id":330,
      "wallet":"0x3617d8182b78e6298052034b499f75cf0d86b8ea",
      "chain_id_from":1,
      "chain_id_to":56,
      "tx_hash_start":"0x63d53c77bf2fd4cd1e9d90912352deaf142d935414e5f06d6ed3223314eb67d5",
      "tx_hash_finish":null,
      "tx_hash_cancel_start":null,
      "tx_hash_cancel_finish":null,
      "recipient":"0x3617d8182b78e6298052034b499f75cf0d86b8ea",
      "state":1,
      "assets":[
         {
            "chain_id_original":1,
            "asset_from":"0x4C153BFaD26628BdbaFECBCD160A0790b1b8F212",
            "asset_original":"0x4C153BFaD26628BdbaFECBCD160A0790b1b8F212",
            "tokens":[
               {
                  "id":"19885",
                  "uri":"https://ipfs.io/ipfs/bafybeifvwitulq6elvka2hoqhwixfhgb42l4aiukmtrw335osetikviuuu"
               }
            ]
         }
      ]
   }
]
```

## Definitions

`Teleport`

Name                  | Type    | Description
----------------------|---------|---------------------------------
id 					  | Int     | Unique teleport id.
wallet 				  | String  | A wallet that initiated a start.
chain_id_from 		  | Int     | Start transaction ChainId.
chain_id_to           | Int     | Finish transaction ChainId.
tx_hash_start         | String  | Start transaction hash.
tx_hash_finish        | String  | Finish transaction hash.
tx_hash_cancel_start  | String  | Cancel start transaction hash.
tx_hash_cancel_finish | String  | Cancel finish transaction hash.
recipient             | String  | Nft recipient.
state                 | TeleportState | Teleport state.
assets                | Asset[] | Assets.

`Order`

Value  | Description
-------|-------
'asc'  | Ascending order (sorts from the oldest teleport to newest).
'desc' | Descending order (sorts from the newest teleport to oldest).

`TeleportState`

Value | Name                         | Description
--|----------------------------------|-----
1 | STARTED                          | Teleport start done, confirmations received.
2 | WAIT_COMPLETE_CONFIRMATIONS      | Teleport finish requested, waiting for confirmations.
3 | COMPLETED                        | Teleport finish done, confirmations received.
4 | WAIT_CANCEL_START_CONFIRMATIONS  | Teleport cancel start requested, waiting for confirmations.
5 | CANCEL_STARTED                   | Teleport cancel start done, confirmations received.
6 | WAIT_CANCEL_FINISH_CONFIRMATIONS | Teleport cancel finish requested, waiting for confirmations.
7 | CANCEL_FINISHED                  | Teleport cancel finish done.

`Asset`

Name              | Type    | Description
------------------|---------|----------------------
chain_id_original | Int     | Original ChainId.
asset_from        | String  | Asset address on start transaction.
asset_original    | String  | Original asset address, equals to 'asset_from' for original asset.
tokens            | Token[] | List of NFT tokens.

`Token`

Name  | Type   | Description
------|--------|-----
id    | Int    | Nft id.
uri   | String | Nft token_uri.


