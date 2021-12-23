# Errors

Errors consist of two parts: an error code and a message.  
Codes are universal while messages vary.  
Body response example.
```js
{
  "code":-290,
  "message":"Forbidden action for teleport."
}
```

## HTTP Return Codes
* HTTP `4XX` return codes are used for malformed requests;
  the issue is on the sender side.
* HTTP `5XX` return codes are used for internal errors; 
  the issue is on the server side.

## Error Codes  

* `-499` to -`200` - client errors.
* `-1XX` - server errors.

Code     | Http Code | Message                        | Description
---------|-----------|--------------------------------|-----
-290     | 403       | Forbidden action for teleport. | The sender of the finish teleport transaction must be the recipient of the first transaction to complete the teleportation (start teleport); either the sender or the recipient can initiate start teleport cancel or finish teleport cancel.
-280     | 404       | Teleport was not found.        | Teleport with the requested data was not found, or teleport awaits start teleport transaction confirmations.
-270     | 422       | Unsupported token.             | Token must support ERC165, ERC721 and ERC721Metadata interfaces.
-250     | 409       | Teleport state conflict.       | Due to the teleport state, the operation cannot be completed. Example: teleport already completed.
-221     | 400       | Unsupported api version...     | See the supported versions field in the response.
-220     | 400       | Invalid api version.           | Route must start with the `v` prefix and the version must be a parseable float.
-201     | 400       | 'chain_id_from' can't be equal to 'chain_id_to'. | See the supported chains.
-200     | 400       | One or more validation errors occurred. | See the `errors` field in the response.
-100     | 500       | Server internal error.         | Contact technical support service.
