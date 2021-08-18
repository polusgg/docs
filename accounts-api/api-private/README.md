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

## Get a User by their Discord ID

Get an user by its hyphenated UUID.

| Method | Endpoint |
| --- | --- |
| `GET` | `/users/discord/<diacord>` where `<diacord>` is the user's Discord Snowflake ID |

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

A `404 Not Found` response will be returned if no user with the given Discord ID exists.

## Get a User by their Display Name

Get an user by its hyphenated UUID.

| Method | Endpoint |
| --- | --- |
| `GET` | `/users/name/<name>` where `<name>` is the user's URL-encoded display name |

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

A `404 Not Found` response will be returned if no user with the given display name exists.

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

## Update Display Names

Update a user's display name.

| Method | Endpoint |
| --- | --- |
| `PATCH` | `/users/update/<uuid>/name` where `<uuid>` is the user's hyphenated UUID |

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
  // The user's new display name
  "display_name": string,
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

A `422 Unprocessable Entity` response will be returned if the body does not pass the validation check and will have the following structure:

```ts
{
  // A message describing the broader validation issue
  "message": string,
  // The error bag
  "errors": {
    // The errors for the `display_name` field
    "display_name": [
      // An array of strings describing one or more issues with the provided display name
    ]
  }
}
```

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
  // The hyphenated UUID of the lobby from which the player was kicked, or `null`
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
  // The hyphenated UUID of the lobby from which the player was banned, or `null`
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
  // The hyphenated UUID of the lobby in which the player was muted, or `null`
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

## Get Kicks From a User

Get all instances of the user kicking another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/kick/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the kick
      "id": number,
      // The hyphenated UUID of the lobby in which the kick occurred, or `null`
      "game_uuid": string
      // The internal ID of the kicking user
      "acting_user_id": number.
      // The internal ID of the user that was kicked
      "target_user_id": number.
      // The reason for why the user was kicked
      "reason": string
      // The kicking user
      "acting_user": {
        // The internal ID of the kicking user
        "id": number,
        // The hyphenated UUID of the kicking user
        "uuid": string,
        // The kicking user's display name
        "display_name": string
      },
      // The user that was kicked
      "target_user": {
        // The internal ID of the user that was kicked
        "id": number,
        // The hyphenated UUID of the user that was kicked
        "uuid": string,
        // The kicked user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.

## Get Kicks Against a User

Get all instances of the user being kicked by another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/kick/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the kick
      "id": number,
      // The hyphenated UUID of the lobby in which the kick occurred, or `null`
      "game_uuid": string
      // The internal ID of the kicking user
      "acting_user_id": number.
      // The internal ID of the user that was kicked
      "target_user_id": number.
      // The reason for why the user was kicked
      "reason": string
      // The kicking user
      "acting_user": {
        // The internal ID of the kicking user
        "id": number,
        // The hyphenated UUID of the kicking user
        "uuid": string,
        // The kicking user's display name
        "display_name": string
      },
      // The user that was kicked
      "target_user": {
        // The internal ID of the user that was kicked
        "id": number,
        // The hyphenated UUID of the user that was kicked
        "uuid": string,
        // The kicked user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.

## Get Bans From a User

Get all instances of the user banning another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/ban/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the ban
      "id": number,
      // The hyphenated UUID of the lobby in which the ban occurred, or `null` if it happened outside of a game
      "game_uuid": string
      // The timestamp at which the user's ban will expire
      // If this is null then the user is banned indefinitely
      "banned_until": string
      // The internal ID of the banning user
      "acting_user_id": number.
      // The internal ID of the user that was banned
      "target_user_id": number.
      // The reason for why the user was banned
      "reason": string
      // The banning user
      "acting_user": {
        // The internal ID of the banning user
        "id": number,
        // The hyphenated UUID of the banning user
        "uuid": string,
        // The banning user's display name
        "display_name": string
      },
      // The user that was banned
      "target_user": {
        // The internal ID of the user that was banned
        "id": number,
        // The hyphenated UUID of the user that was banned
        "uuid": string,
        // The banned user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.

## Get Bans Against a User

Get all instances of the user being banned by another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/ban/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the ban
      "id": number,
      // The hyphenated UUID of the lobby in which the ban occurred, or `null` if it happened outside of a game
      "game_uuid": string
      // The timestamp at which the user's ban will expire
      // If this is null then the user is banned indefinitely
      "banned_until": string
      // The internal ID of the banning user
      "acting_user_id": number.
      // The internal ID of the user that was banned
      "target_user_id": number.
      // The reason for why the user was banned
      "reason": string
      // The banning user
      "acting_user": {
        // The internal ID of the banning user
        "id": number,
        // The hyphenated UUID of the banning user
        "uuid": string,
        // The banning user's display name
        "display_name": string
      },
      // The user that was banned
      "target_user": {
        // The internal ID of the user that was banned
        "id": number,
        // The hyphenated UUID of the user that was banned
        "uuid": string,
        // The banned user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.

## Get Mutes From a User

Get all instances of the user muting another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/mute/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the mute
      "id": number,
      // The hyphenated UUID of the lobby in which the mute occurred, or `null` if it happened outside of a game
      "game_uuid": string
      // The timestamp at which the user's mute will expire
      // If this is null then the user is muted indefinitely
      "muted_until": string
      // The internal ID of the muting user
      "acting_user_id": number.
      // The internal ID of the user that was muted
      "target_user_id": number.
      // The reason for why the user was muted
      "reason": string
      // The muting user
      "acting_user": {
        // The internal ID of the muting user
        "id": number,
        // The hyphenated UUID of the muting user
        "uuid": string,
        // The muting user's display name
        "display_name": string
      },
      // The user that was muted
      "target_user": {
        // The internal ID of the user that was muted
        "id": number,
        // The hyphenated UUID of the user that was muted
        "uuid": string,
        // The muted user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.

## Get Mutes Against a User

Get all instances of the user being muted by another user.

| Method | Endpoint |
| --- | --- |
| `GET` | `/logs/mute/<uuid>/from` where `<uuid>` is the user's hyphenated UUID |

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
  // The total number of results
  "total": number,
  // The current page of results
  "current_page": number,
  // The number of results per page
  "per_page": number,
  // The offset number of the first item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `3`
  "from": number,
  // The offset number of the last item on the current page
  // If `per_page` is `2` and `current_page` is `2` then this would be `4`
  "to": number,
  // The request URL
  "path": string,
  // The link to the previous page, or `null` if on the first page
  "prev_page_url": string,
  // The link to the next page, or `null` if on the last page
  "next_page_url": string,
  // The first page number
  "first_page": number,
  // The link to the first page
  "first_page_url": string,
  // The last page number
  "last_page": number,
  // The link to the last page
  "last_page_url": string,
    // Zero or more ban entries
  "data": [
    {
      // The ID of the mute
      "id": number,
      // The hyphenated UUID of the lobby in which the mute occurred, or `null` if it happened outside of a game
      "game_uuid": string
      // The timestamp at which the user's mute will expire
      // If this is null then the user is muted indefinitely
      "muted_until": string
      // The internal ID of the muting user
      "acting_user_id": number.
      // The internal ID of the user that was muted
      "target_user_id": number.
      // The reason for why the user was muted
      "reason": string
      // The muting user
      "acting_user": {
        // The internal ID of the muting user
        "id": number,
        // The hyphenated UUID of the muting user
        "uuid": string,
        // The muting user's display name
        "display_name": string
      },
      // The user that was muted
      "target_user": {
        // The internal ID of the user that was muted
        "id": number,
        // The hyphenated UUID of the user that was muted
        "uuid": string,
        // The muted user's display name
        "display_name": string
      }
    }
  ]
}
```

A `401 Unauthorized` response will be returned if the login failed.
