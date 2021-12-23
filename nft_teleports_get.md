# Teleports - Get

Get teleport by id.

```
 GET /v0.1/nft/teleport/{teleportId}
```

With optional parameters:

```
 GET /v0.1/nft/teleport/{teleportId}?include_asset={include_asset}
```

## Route Parameters

Name           | Required | Type  | Description
---------------|----------|-------|-----
teleportId     | true     | Int   | Teleport id.

## Query Parameters

Name              | Required | Type | Description
------------------|-------| -------|-----
include_asset     | False | Boolean| Include asset and token info. Default - false.

### Example
```
 GET /v0.1/nft/teleports/197?include_asset=true
```

## Responses
Name            | Type     | Description
----------------|----------|------
200 OK          | Teleport | OK
400 Bad Request | Error    | See the request requirements.
404 Not Found   | Error    | Teleport was not found.

See also [Errors Codes](errors.md).

### Example
```json
{
   "id":197,
   "wallet":"0xdf48f4004b73ce3f954bf243a76bd789e435642d",
   "chain_id_from":1,
   "chain_id_to":56,
   "tx_hash_start":"0x11dcb4caeb4e18af3f5ef58e5fab2a4eeb97b5a8126eee259ddaa05e2ef85183",
   "tx_hash_finish":"0x669637a5271f7c0fa778b634d33379e58f0b8ed0b62a8491d10855ee6f7c0b25",
   "tx_hash_cancel_start":null,
   "tx_hash_cancel_finish":null,
   "recipient":"0xdf48f4004b73ce3f954bf243a76bd789e435642d",
   "state":3,
   "assets":[
      {
         "chain_id_original":1,
         "asset_from":"0xf5de760f2e916647fd766B4AD9E85ff943cE3A2b",
         "asset_original":"0xf5de760f2e916647fd766B4AD9E85ff943cE3A2b",
         "tokens":[
            {
               "id":"19016",
               "uri":"https://ipfs.io/ipfs/bafybeiezeds576kygarlq672cnjtimbsrspx5b3tr3gct2lhqud6abjgiu"
            },
            {
               "id":"19018",
               "uri":"https://ipfs.io/ipfs/bafybeiezeds576kygarlq672cnjtimbsrspx5b3tr3gct2lhqud6abjgiu"
            }
         ]
      }
   ]
}
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
