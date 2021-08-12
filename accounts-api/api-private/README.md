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
    // The timestamp at which the user's account was created
    "created_at": string,
    // The timestamp after which the user will be able to change their name
    "name_change_available_at": string
    // Whether or not the user is currently banned
    "banned": boolean,
    // The timestamp at which the user's ban will expire
    // If the user is banned and this is null, then the user is banned indefinitely
    "banned_until": string | null,
    // Whether or not the user is currently muted
    "muted": boolean,
    // The timestamp at which the user's mute will expire
    // If the user is muted and this is null, then the user is muted indefinitely
    "muted_until": string | null,
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
  // The hyphenated UUID of the lobby from which the player was kicked
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
  // The hyphenated UUID of the lobby from which the player was banned
  "game_uuid": string,
  // The hyphenated UUID of the banning user
  "actor_uuid": string,
  // The hyphenated UUID of the user that was banned
  "target_uuid": string,
  // The reason for why the user was banned
  "reason": string,
  // The length of the ban
  // - One or more numbers followed immediately by either 'w', 'd', or 'h'
  //   e.g., '1w' for 1 week, '2d' for 2 days, and '10h' for 10 hours
  // - Set to `null` for an indefinite ban
  "duration": string
}
```

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true,
  "data": {
    // The duration, in hours, of the user's ban.
    // - `-1` if the ban is indefinite
    "duration_hours": number
  }
}
```

A `401 Unauthorized` response will be returned if the login failed.

A `400 Bad Request` response will be returned if the body has any missing or malformed fields.

## Mute a User

Mute a user and store an associated log entry.

| Method | Endpoint |
| --- | --- |
| `PUT` | `/logs/mute` |

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
  // The hyphenated UUID of the lobby in which the player was muted
  "game_uuid": string,
  // The hyphenated UUID of the muting user
  "actor_uuid": string,
  // The hyphenated UUID of the user that was muted
  "target_uuid": string,
  // The reason for why the user was muted
  "reason": string,
  // The length of the mute
  // - One or more numbers followed immediately by either 'w', 'd', or 'h'
  //   e.g., '1w' for 1 week, '2d' for 2 days, and '10h' for 10 hours
  // - Set to `null` for an indefinite mute
  "duration": string
}
```

#### Response

A successful response (`200 OK`) will return a JSON string with the following structure:

```ts
{
  "success": true,
  "data": {
    // The duration, in hours, of the user's mute.
    // - `-1` if the mute is indefinite
    "duration_hours": number
  }
}
```

A `401 Unauthorized` response will be returned if the login failed.

A `400 Bad Request` response will be returned if the body has any missing or malformed fields.
