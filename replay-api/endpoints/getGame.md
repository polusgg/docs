# Public
this endpoint is internal-use only.

## Request

| Method |     Endpoint      |
|--------|-------------------|
| `POST` | `/api/v1/getGame` | 

the request requires the following headers:

|     Header      |                                                     Value                                                     |
|-----------------|---------------------------------------------------------------------------------------------------------------|
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token, or the token of a moderator/member of the game |
| `Accept`        | `application/json`                                                                                            |

the post body must follow the below format:
```ts
type RequestStructure = {
  gameId: string;
  websocketToken: string;
}
```

## Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
type ResponseStructure = {
  success: true,
  data: {
    players: {
      // the UUID of the player, hyphenated
      userId: string;
      playerId: number;
      connectionId: number;
      isHost: boolean;
      cosmetics: {
        type: number;
        content: any;
      }[];
    }[];
    connections: {
      // these two fields are only returned if a requester has the correct permissions
      ip: string;
      port: number;
      //
      id: number;
      name: string;
    }[];
    gameOptions: {
      name: string;
      category: string;
      priority: number;
      value: {
        type: 0;
        value: number;
        step: number;
        lower: number;
        upper: number;
        zeroIsInfinity: boolean;
        suffix: string;
      } | {
        type: 1;
        value: boolean;
      } | {
        value: 2;
        index: number;
        options: string[];
      };
    };
    gameCode: string;
    createdAt: number;
    gameTags: { key: number; value: any }[];
  }
}
```

A `401 Unauthorized` response will be returned if the server access token is invalid.
