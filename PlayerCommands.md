# ACDC Player Commands

These commands are available to all players in the game.

## Command Structure

All commands use the `acdc:` prefix (e.g., `acdc:menu`, `acdc:team`).

> **Note:** The `acdc:` prefix is only required if the command name conflicts with another addon's commands. If there are no conflicts, you can omit it (e.g., just use `menu` instead of `acdc:menu`).

---

## General Commands

### `menu`

**Permission:** Any  
**Parameters:** `action: Enum`

| Action  | Use                     |
| ------- | ----------------------- |
| `main`  | Open the main menu      |
| `team`  | Open the main team menu |
| `badge` | Open the badges menu    |

---

## Team Management

### `team`

**Permission:** Any  
**Parameters:** `action: Enum`, `[teamName: String]`, `[password: String]`

| Action   | TeamName | Password | Use                                |
| -------- | -------- | -------- | ---------------------------------- |
| `create` | Required | Required | Create a new team and become owner |
| `join`   | Required | -        | Join a team you've been invited to |
| `leave`  | -        | -        | Leave your current team            |
| `list`   | -        | -        | List all teams and their scores    |

---

### `team_member`

**Permission:** Any (owner only)  
**Parameters:** `action: Enum`, `[playerName: String]`

| Action     | PlayerName | Use                                |
| ---------- | ---------- | ---------------------------------- |
| `invite`   | Required   | Invite a player to your team       |
| `uninvite` | Required   | Cancel a pending invite            |
| `invites`  | -          | List pending invites for your team |
| `remove`   | Required   | Remove a member from your team     |
| `promote`  | Required   | Promote a team member to owner     |
| `demote`   | Required   | Demote an owner to regular member  |

---

## Land Claims

### `land`

**Permission:** Any (owner only)  
**Parameters:** `action: Enum`

| Action    | Use                                       |
| --------- | ----------------------------------------- |
| `claim`   | Claim land for your team at your location |
| `unclaim` | Remove the land claim you're standing in  |

---

## Teleportation

### `tp`

**Permission:** Any  
**Parameters:** `action: Enum`, `[name: String]`

| Action        | Name     | Use                                             |
| ------------- | -------- | ----------------------------------------------- |
| `to`          | Required | Teleport to another player                      |
| `team`        | Required | Teleport to a team's land claim                 |
| `region`      | Required | Teleport to a protection region                 |
| `list`        | -        | List players you can teleport to                |
| `listregions` | -        | List all available regions for teleportation    |
| `toggle`      | -        | Toggle if others can teleport to you            |
| `toggleteam`  | -        | Toggle if non-members can teleport to team area |

---

## Badge Management

### `badge`

**Permission:** Any  
**Parameters:** `action: Enum`, `[badgeId: Integer]`, `[webUrl: String]`, `[comment: String]`

| Action  | BadgeId  | WebUrl   | Comment  | Use                         |
| ------- | -------- | -------- | -------- | --------------------------- |
| `list`  | -        | -        | -        | View team badge status      |
| `claim` | Required | Required | Optional | Claim a badge for your team |

---
