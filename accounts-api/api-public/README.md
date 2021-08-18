# Public API

The public API is used by <ins>clients</ins>.

### Base URL

The base path for all public API requests is `/api/v1`.

---

## Log In

Log in and get an access token.

| Method | Endpoint |
| --- | --- |
| `POST` | `/auth/token` |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Content-Type` | `application/json` |

As described in the `Content-Type` header, the request body should be a JSON string with the following structure:

```ts
{
  // The user's Polus.gg account email address
  "email": string,
  // The user's Polus.gg account password
  "password": string
}
```

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
    ],
    // The user's cosmetic options
    "cosmetics": {
        // ...
    }
  }
}
```

A `401 Unauthorized` response will be returned if authentication failed.

A `429 Too Many Requests` response will be returned if there were too many authentication attempts.

## Check an Access Token

Check that an access token is still valid.

| Method | Endpoint |
| --- | --- |
| `POST` | `/auth/check` |

#### Request

The request requires the following headers:

| Header | Value |
| --- | --- |
| `Accept` | `application/json` |
| `Client-ID` | The user's hyphenated UUID |
| `Authorization` | `Bearer <token>` where `<token>` is the user's access token |

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
    ],
    // The user's cosmetic options
    "cosmetics": {
        // ...
    }
  }
}
```

A `401 Unauthorized` response will be returned if authentication failed.

A `429 Too Many Requests` response will be returned if there were too many authentication attempts.
