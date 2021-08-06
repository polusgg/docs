# Private
this endpoint is internal-use only. It's intended use is to generate upload tokens from Game Servers only.

## Request

| Method |        Endpoint         |
|--------|-------------------------|
| `POST` | `/api/v1/requestUpload` | 

the request requires the following headers:

|     Header      |                             Value                             |
|-----------------|---------------------------------------------------------------|
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token |
| `Accept`        | `application/json`                                            |

the post body must follow the below format:
```ts
type RequestStructure = {
  // the UUID of the current game, hyphenated
  gameId: string;

  // the UUID of the uploader, hyphenated
  userId: string;
}
```

## Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
type ResponseStructure = {
  success: true,
  data: {
    uploadToken: string;
    // an ISO 8601 timestamp
    expireTime: string;
  }
}
```

A `401 Unauthorized` response will be returned if the server access token is invalid.
