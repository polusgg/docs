# Public
this endpoint is public. It's intended use is to upload replays from the client.

## Request

| Method |     Endpoint     |
|--------|------------------|
| `POST` | `/api/v1/upload` | 

the request requires the following headers:

|     Header      |                                                        Value                                                        |
|-----------------|---------------------------------------------------------------------------------------------------------------------|
| `Authorization` | `Bearer <token>+<uploadToken>` where `<token>` is the client's access token, and `<uploadToken>` is the uploadToken |
| `Accept`        | `application/json`                                                                                                  |

the post body must follow the below format:
```ts
// the contents of the buffer should be the serialized replay
type RequestStructure = Buffer
```

## Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
type ResponseStructure = {
  success: true
}
```

A `401 Unauthorized` response will be returned if the client access token is invalid, the upload token is invalid, or the upload token has expired.

the vagueness of the 401 unauthorized response is intended, as someone attempting to abuse our API should be given as little information as possible.
