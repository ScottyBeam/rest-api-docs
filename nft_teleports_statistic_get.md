# Teleport Statistic - Get

Get overall statistics info. Update time - 5 min.

```
 GET /v0.1/nft/teleports/statistic
```

### Example
```
 GET /v0.1/nft/teleports/statistic
```

## Responses

Name   | Type      | Description
-------|-----------|------
200 OK | Statistic | OK

### Example
```json
{
   "started":186,
   "completed":100,
   "cancel_started":72,
   "cancel_completed":69
}
```

## Definitions

`Statistic`

Name  | Type | Description
------|-------|-----
started | Int | Started teleporters number.
completed | Int | Finished teleports number.
cancel_started | Int | Started teleports cancel number.
cancel_completed | Int | Finished  teleports cancel number.
