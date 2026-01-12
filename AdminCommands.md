# ACDC Admin Commands

These commands require **Operator** permissions or specific admin roles (GameDirectors).

## Command Structure

All commands use the `acdc:` prefix (e.g., `acdc:menu`, `acdc:team_admin`).

> **Note:** The `acdc:` prefix is only required if the command name conflicts with another addon's commands. If there are no conflicts, you can omit it (e.g., just use `menu` instead of `acdc:menu`).

---

## Menu Access

### `menu`

**Permission:** [OP]  
**Parameters:** `action: Enum`

| Action        | Use                            |
| ------------- | ------------------------------ |
| `admin_badge` | Open the badge management menu |

---

## Team Administration

### `team_admin`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[teamName: String]`, `[param: String]`

| Action         | TeamName | Param        | Use                                                |
| -------------- | -------- | ------------ | -------------------------------------------------- |
| `rename`       | Required | `newName`    | Rename any team                                    |
| `addmember`    | Required | `playerName` | Add a player to any team (even with no members)    |
| `removemember` | Required | `playerName` | Remove a player from any team                      |
| `removeregion` | Required | -            | Remove a land region from any team                 |
| `listmembers`  | Required | -            | List members for a team                            |
| `delete`       | Required | -            | Delete a team (removes land claim and all members) |

---

### `team_password`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[password: String]`

| Action | Password | Use                        |
| ------ | -------- | -------------------------- |
| `get`  | -        | Get team creation password |
| `set`  | Required | Set team creation password |

---

## Protection Regions

### `region`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[name: String]`

| Action   | Name     | Use                                                    |
| -------- | -------- | ------------------------------------------------------ |
| `list`   | -        | List all your protection regions                       |
| `info`   | Required | Show detailed info about a region                      |
| `debug`  | -        | Show debug info about protection regions and detection |
| `remove` | Required | Remove one of your protection regions                  |

---

### `region_create`

**Permission:** [OP] GameDirectors  
**Parameters:** `name: String`, `shape: Enum`, `size: Integer`, `[gameMode: Enum]`, `[showInMenu: Boolean]`

**Shape Values:** square, circle  
**GameMode Values:** default, creative, survival, adventure

**Use:** Create a protection region at your current location

---

### `region_member`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `regionName: String`, `playerName: String`

| Action   | RegionName | PlayerName | Use                                        |
| -------- | ---------- | ---------- | ------------------------------------------ |
| `add`    | Required   | Required   | Add a player to region's allowed list      |
| `remove` | Required   | Required   | Remove a player from region's allowed list |

---

### `region_config`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `regionName: String`, `[gameMode: Enum]`

| Action                | RegionName | GameMode | Use                                                  |
| --------------------- | ---------- | -------- | ---------------------------------------------------- |
| `toggleboundary`      | Required   | -        | Toggle boundary visibility for a region              |
| `setgamemode`         | Required   | Required | Set game mode for non-owners in a region             |
| `togglemenu`          | Required   | -        | Toggle region appearance in teleport menu            |
| `toggleownergamemode` | Required   | -        | Toggle if owner is affected by the game mode setting |
| `setspawn`            | Required   | -        | Set custom spawn point for region at your location   |

**GameMode Values:** default, creative, survival, adventure

**Note:** By default, region owners are always in Creative mode when in their region, regardless of the `setgamemode` setting. Use `toggleownergamemode` to make the owner also be affected by the game mode restriction (e.g., to create a survival region where even you are in survival mode).

---

### `region_setsortorder`

**Permission:** [OP] GameDirectors  
**Parameters:** `regionName: String`, `sortOrder: Integer`

**Use:** Set the sort order for a region in the teleport menu. Lower numbers appear first (default is 0).

**Example:** `/region_setsortorder ParkourMinigame 5`

---

## Role Management

### `role`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[playerName: String]`, `[role: Enum]`

| Action   | PlayerName | Role     | Use                         |
| -------- | ---------- | -------- | --------------------------- |
| `add`    | Required   | Required | Add a role to a player      |
| `remove` | Required   | Required | Remove a role from a player |
| `list`   | -          | -        | List all players with roles |

**Role Values:** operator, badge_admin, badge_judge, team_admin

---

## System Configuration

### `logmode`

**Permission:** [OP] GameDirectors  
**Parameters:** `mode: Enum`

**Mode Values:** console, chat, both

**Use:** Set log output mode

---

### `loglevel`

**Permission:** [OP] GameDirectors  
**Parameters:** `level: Enum`

**Level Values:** debug, info, warn, error

**Use:** Set minimum log level

---

### `logstatus`

**Permission:** [OP] GameDirectors  
**Parameters:** None

**Use:** Show current log settings

---

## Data Management

### `data`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[subAction: String]`, `[pageNumber: Integer]`

| Action        | SubAction           | PageNumber | Use                                                     |
| ------------- | ------------------- | ---------- | ------------------------------------------------------- |
| `status`      | -                   | -          | Show database storage statistics and shard info         |
| `dump`        | -                   | -          | Export core data as JSON (excludes paginated datasets)  |
| `dump`        | `claims`            | Optional   | Export badge claims with pagination (25 per page)       |
| `dump`        | `teams`             | Optional   | Export teams with pagination (25 per page)              |
| `dump`        | `badges`            | Optional   | Export badges with pagination (25 per page)             |
| `dump`        | `protectionregions` | Optional   | Export protection regions with pagination (25 per page) |
| `dump`        | `dailyrankings`     | Optional   | Export daily rankings with pagination (25 per page)     |
| `cleanup`     | -                   | -          | Remove orphaned score displays                          |
| `resetbadges` | -                   | -          | Clear all badges and claims, reload from badges.json    |
| `recalculate` | -                   | -          | Recalculate all team scores from approved badge claims  |

**Examples:**

- `/data dump` - Export core database (player prefs, roles, judging session, etc.)
- `/data dump claims` - Export first page of claims (claims 1-25)
- `/data dump claims 2` - Export second page of claims (claims 26-50)
- `/data dump teams 3` - Export third page of teams (teams 51-75)
- `/data dump badges` - Export first page of badges
- `/data dump protectionregions 2` - Export second page of protection regions
- `/data dump dailyrankings` - Export first page of daily rankings
- `/data recalculate` - Recalculate all team scores from approved claims

---

### `data_delete`

**Permission:** [OP] GameDirectors  
**Parameters:** `tableName: Enum`, `id: String`

**Table Names:** claims, teams, protectionregions, judgingsessions

**Use:** Delete a record by ID from the specified table

**Examples:**

- `/data_delete claims abc123` - Delete claim with ID "abc123"
- `/data_delete teams team_001` - Delete team with ID "team_001"
- `/data_delete protectionregions spawn_region` - Delete protection region with ID "spawn_region"
- `/data_delete judgingsessions session_001` - Delete judging session with ID "session_001"

---

### `data_update`

**Permission:** [OP] GameDirectors  
**Parameters:** `tableName: Enum`, `jsonData: String`

**Table Names:** claims, teams, protectionregions, judgingsessions

**Use:** Update a record with partial or full JSON data (must include 'id' field)

**Examples:**

- `/data_update claims {"id":"abc123","status":"approved"}` - Update claim status
- `/data_update teams {"id":"team_001","score":100}` - Update team score
- `/data_update protectionregions {"id":"spawn","showInMenu":true}` - Update region visibility
- `/data_update judgingsessions {"id":"session_001","currentDay":2}` - Update judging session day

---

## Webhook Management

### `webhook`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[param1: String]`, `[param2: String]`

| Action         | Param1         | Param2             | Use                                          |
| -------------- | -------------- | ------------------ | -------------------------------------------- |
| `config`       | endpoint (URL) | interval (seconds) | Configure webhook endpoint and dump interval |
| `start`        | -              | -                  | Start webhook processing (preserves queue)   |
| `stop`         | -              | -                  | Pause webhook processing (preserves queue)   |
| `status`       | -              | -                  | Show webhook configuration and queue status  |
| `events`       | on/off         | -                  | Enable/disable event webhook queuing         |
| `dump`         | on/off         | interval (seconds) | Enable/disable scheduled data dumps          |
| `force-dump`   | -              | -                  | Immediately trigger a chunked data dump      |
| `queue`        | -              | -                  | Show current webhook queue status            |
| `clear`        | -              | -                  | Clear the webhook queue                      |
| `failed`       | -              | -                  | Show failed webhooks (dead letter queue)     |
| `clear-failed` | -              | -                  | Clear the dead letter queue                  |

**Examples:**

- `/webhook config https://api.example.com/webhook 3600` - Set endpoint with 1-hour dump interval
- `/webhook events off` - Disable event queuing (useful during testing)
- `/webhook dump on 7200` - Enable data dumps every 2 hours
- `/webhook force-dump` - Trigger immediate data dump

---

## Impersonation & Dummy Management

### `impersonate`

**Permission:** [OP] GameDirectors  
**Parameters:** `action: Enum`, `[identity: String]`

| Action   | Identity | Use                                   |
| -------- | -------- | ------------------------------------- |
| `create` | Required | Create a dummy player identity        |
| `list`   | -        | List dummy player identities          |
| `start`  | Required | Start impersonating a player or dummy |
| `stop`   | -        | Stop impersonating                    |
| `status` | -        | Show current impersonation status     |

---
