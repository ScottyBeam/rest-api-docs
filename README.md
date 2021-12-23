# Public Rest API for Scotty Beam 0.1

## General API Information
The base endpoint is: https://api.scottybeam.io.  
Current supported api version - `0.1`.  
Last update - `12.23.2021`.

## General Information on Endpoints
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, the parameters must be sent as a
  `request body` with `Content-Type`
  `application/json`.
* Parameters may be sent in any order.
* Do not rely on letter case for transaction hash, contract address or wallet address in response.

## Teleport flow
1) [Give approvements to the teleport agent.](nft_teleports_populate_approves_get.md)
2) [Start teleport.](nft_teleports_populate_start.md)
3) [Wait for confirmations on the transaction.](#supported-chains)
4) [Finish teleport.](nft_teleports_populate_finish.md)

## Teleport cancel flow
1) [Start cancel.](nft_teleports_populate_cancel_start.md)
2) [Wait for confirmations on the transaction.](#supported-chains)
3) [Finish cancel.](nft_teleports_populate_cancel_finish.md)

### Limitations
* Asset must implement ERC165, ERC721 and ERC721Metadata interfaces.
* Max number of assets per teleport - 5.
* Max number of tokens per asset - 10.
* Max tokenURI length - 2000.

## API Endpoints

### Ping
* [Ping](ping.md)

### Nft Teleports
* [Teleports - List](nft_teleports.md)
* [Teleports - Get](nft_teleports_get.md)
* [Teleport Statistic - Get](nft_teleports_statistic_get.md)
* [Teleport Approves - Get](nft_teleports_populate_approves_get.md)
* [Teleport Start - Populate](nft_teleports_populate_start.md)
* [Teleport Finish - Populate](nft_teleports_populate_finish.md)
* [Teleport Cancel Start - Populate](nft_teleports_populate_cancel_start.md)
* [Teleport Cancel Finish - Populate](nft_teleports_populate_cancel_finish.md)

## Errors
[Errors](errors.md) defines specific error codes and messages.

## Supported chains

ChainId | Name                           | Confirmation count
--------|--------------------------------|-----
1       | Ethereum                       | 12
56      | Binance Smart Chain            | 30
137     | Polygon                        | 30
4002    | Fantom                         | 30
43114   | Avalanche                      | 30
