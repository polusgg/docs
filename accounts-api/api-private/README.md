# Private API

The private API is used by <ins>server nodes</ins>.

### Base URL

The base path for all private API requests is `/api-private/v1`.

---

## Get a User

Get an user by its hyphenated UUID.

| Method | Endpoint |
| --- | --- |
| `GET` | `/users/<uuid>` where `<uuid>` is the user's hyphenated UUID |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token |

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true,
  // Response data
  "data": {
    // The user's hyphenated UUID
    "client_id": string,
    // The user's access token
    "client_token": string,
    // The user's Discord ID
    "discord_id": string | null,
    // The user's display name
    "display_name": string,
    // - If the user is currently banned then this will be an ISO 8601
    //   timestamp describing the time at which their ban will expire
    //   (e.g. 2021-04-20T00:03:41.000000Z)
    // - If the user is not currently banned then this will be null
    "banned_until": string | null,
    // A list of all perks that the user has access to
    // This example lists all possible perks
    "perks": [
      // Custom 4 or 6 letter lobby codes
      "lobby.code.custom",
      // Ability to host lobbies with up to 25 players
      "lobby.size.25",
      // Ability to host lobbies with up to 50 players
      "lobby.size.50",
      // Ability to host lobbies with up to 100 players
      "lobby.size.100",
      // Among Us player name is colored gold (can be turned off)
      "name.color.gold",
      // Among Us player name color matches your player color (can be turned off)
      "name.color.match",
      // Custom player color using an RGB color picker
      "player.color.rgb",
      // Access to development servers
      "server.access.dev",
      // Access to beta testing servers
      "server.access.beta",
      // Access to Creator-only servers
      "server.access.creator",
      // Manage the Creator status of other users
      "creator.manage",
      // Kick players from a game
      "mod.kick",
      // Ban players from a game
      "mod.ban"
    ],
    // The user's settings--these values should only be read after checking
    // to see if the user has the relevant perk
    "settings": {
      // An optional 4 or 6 letter string in all-caps
      "lobby.code.custom": string | null,
      // Whether or not the user chose a gold player name
      "name.color.gold": boolean,
      // Whether or not the user chose a player name matching their character color
      "name.color.match": boolean
    },
    // The user's game options
    "options": [
        // ...
    ]
  }
}
```

A `401 Unauthorized` response will be returned if the server access token is invalid.

A `404 Not Found` response will be returned if no user with the given hyphenated UUID exists.

## Update Game Options

Update a user's game options.

| Method | Endpoint |
| --- | --- |
| `PUT` | `/users/<uuid>/options` where `<uuid>` is the user's hyphenated UUID |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Content-Type` | `application/json` |
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token |

As described in the `Content-Type` header, the request body should be a JSON string with the following structure:

```ts
{
  "value": {
    // Numbers
    "value": number,
    "step": number,
    "lower": number,
    "upper": number,
    "zeroIsInfinity": boolean,
    "suffix": string,
  } | {
    // Booleans
    "value": boolean
  } | {
    // Enums
    "index": number,
    "options": string[],
  },
  "category": string,
  "priority": number,
  "key": string,
}
```

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true
}
```

A `401 Unauthorized` response will be returned if the login failed.

A `400 Bad Request` response will be returned if the body has any missing or malformed fields.

## Kick a User

Store a log entry of a user being kicked from a lobby.

| Method | Endpoint |
| --- | --- |
| `PUT` | `/logs/kick` |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Content-Type` | `application/json` |
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token |

As described in the `Content-Type` header, the request body should be a JSON string with the following structure:

```ts
{
  // The hyphenated UUID of the lobby that the player was kicked from
  "game_uuid": string,
  // The hyphenated UUID of the kicking user
  "actor_uuid": string,
  // The hyphenated UUID of the user that was kicked
  "target_uuid": string,
  // The reason for why the user was kicked
  "reason": string
}
```

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true
}
```

A `401 Unauthorized` response will be returned if the login failed.

A `400 Bad Request` response will be returned if the body has any missing or malformed fields.

## Ban a User

Ban a user and store an associated log entry.

| Method | Endpoint |
| --- | --- |
| `PUT` | `/logs/ban` |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Content-Type` | `application/json` |
| `Authorization` | `Bearer <token>` where `<token>` is the server's access token |

As described in the `Content-Type` header, the request body should be a JSON string with the following structure:

```ts
{
  // The hyphenated UUID of the lobby that the player was kicked from
  "game_uuid": string,
  // The hyphenated UUID of the kicking user
  "actor_uuid": string,
  // The hyphenated UUID of the user that was kicked
  "target_uuid": string,
  // The reason for why the user was kicked
  "reason": string,
  // The length of the ban
  // - One or more numbers followed immediately by one of either 'w', 'd', or 'h'
  // - '1w' would ban the user for 1 week, '2d' for 2 days, and '10h' for 10 hours
  "duration": string
}
```

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true,
  "data": {
    // The duration, in hours, of the user's ban
    "duration_hours": number
  }
}
```

A `401 Unauthorized` response will be returned if the login failed.

A `400 Bad Request` response will be returned if the body has any missing or malformed fields.
