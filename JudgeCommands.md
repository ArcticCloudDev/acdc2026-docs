# ACDC Judge Commands

These commands require the **BADGE_JUDGE** role.

## Command Structure

All commands use the `acdc:` prefix (e.g., `acdc:menu`, `acdc:judge`).

> **Note:** The `acdc:` prefix is only required if the command name conflicts with another addon's commands. If there are no conflicts, you can omit it (e.g., just use `menu` instead of `acdc:menu`).

---

## Menu Access

### `menu`

**Permission:** BADGE_JUDGE  
**Parameters:** `[action: Enum]`

| Action  | Use                          |
| ------- | ---------------------------- |
| (none)  | Open the main menu (default) |
| `judge` | Open the judge menu          |

---

## Judge Operations

### `judge`

**Permission:** BADGE_JUDGE  
**Parameters:** `action: Enum`, `[badgeId: Integer]`

| Action      | BadgeId  | Use                                        |
| ----------- | -------- | ------------------------------------------ |
| `claims`    | -        | List all pending badge claims with indices |
| `claimsfor` | Required | List pending claims for a specific badge   |

---

### `judge_claim`

**Permission:** BADGE_JUDGE  
**Parameters:** `action: Enum`, `claimIndex: Integer`, `[message: String]`

| Action    | ClaimIndex | Message  | Use                                                    |
| --------- | ---------- | -------- | ------------------------------------------------------ |
| `approve` | Required   | Optional | Approve a claim by index (uses badge's default points) |
| `reject`  | Required   | Optional | Reject a claim by index (message strongly recommended) |

---

### `judge_award`

**Permission:** BADGE_JUDGE  
**Parameters:** `badgeId: Integer`, `teamName: String`, `[points: Integer]`, `[message: String]`

**Use:** Award a badge directly to a team (optional custom points)

---

## Category Ranking Management

### `ranking`

**Permission:** BADGE_JUDGE  
**Parameters:** `action: Enum`, `[isFinal: Boolean]`

| Action    | IsFinal  | Use                                                             |
| --------- | -------- | --------------------------------------------------------------- |
| `start`   | Optional | Start a ranking session for the next day (auto-incremented)     |
| `status`  | -        | Show current ranking session status                             |
| `cancel`  | -        | Cancel the judging session (operator only)                      |
| `reset`   | -        | Reset the last published day back to draft (operator only)      |
| `undo`    | -        | Completely delete all rankings for the last day (operator only) |
| `preview` | -        | Preview draft rankings for current session day                  |
| `publish` | Optional | Publish rankings and end session (use menu for final day)       |
| `list`    | -        | Show all published rankings grouped by badge                    |

**Examples:**

- `/ranking start` - Start judging for the next day
- `/ranking start true` - Start judging for the final day
- `/ranking status` - Check session status
- `/ranking preview` - Preview draft rankings for current session
- `/ranking publish` - Publish current day's rankings and end session
- `/ranking list` - Show all published rankings grouped by badge
- `/ranking reset` - Reset the last published day to draft state (requires double confirmation)
- `/ranking undo` - Completely delete the last day's session and cancel any active session (requires double confirmation)

**Note:**

- Publishing rankings automatically ends the session
- For final day rankings, use the menu system to publish with proper confirmation dialogs
- Both `reset` and `undo` require you to run the command twice within 1 minute to confirm
- `undo` will also cancel any active ranking session if one exists

---
