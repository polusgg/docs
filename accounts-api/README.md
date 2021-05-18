# Accounts System REST API

Interact with the Polus.gg accounts system.

### Base URL

The base URL for all API requests is `https://account.polus.gg`.

### Error Checking

All successful responses (`200 OK`) will return a JSON string that includes a `successful` field with the value set to `true`.

If this field is missing, or if it is present and the value is `false`, then an error has occured and a message might be provided inside an optional `message` field in the response JSON. Below is an example of a `401 Unauthorized` response:

```ts
{
  "message": "Unauthenticated."
}
```
