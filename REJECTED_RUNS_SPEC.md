# Rejected Runs Data Specification

This document defines the schema and fetching logic for "rejected" or manual runs within the leaderboard application.

## 1. Overview
"Rejected" runs are manually added entries (typically from a GitHub-hosted JSON file) that represent runs that are not verified on the official speedrun.com (SRC) leaderboard but are trusted and recognized by the local community.

## 2. Fetching Logic
The application fetches these runs from a remote JSON file on GitHub:
- **URL:** `https://raw.githubusercontent.com/Aeroshide/mcsrindo-leaderboard-meta/main/rejected.json`
- **Hook:** `hooks/useLeaderboard.js` (passes `topCategory` and active `splits`)
- **Helper:** `utils/leaderboardHelper.js` (`fetchRejected` function)

The fetch process involves:
1.  Retrieving the JSON from the URL.
2.  Filtering for entries where `country_code === 'ID'`.
3.  Determining the `category` key based on the UI selection (see Section 5).
4.  Filtering for entries matching the game `version`.
5.  Transforming the JSON into the **Common Run Object** format.

## 3. JSON Template (JSONC)
The `rejected.json` file should follow this structure:

```jsonc
[
  {
    "id": "manually_added_001",    // Required: Unique string for React keys
    "player": "PlayerName",         // Required: Runner's display name
    "time_ms": 123456,              // Required: Total time in milliseconds
    "country_code": "ID",           // Required: Must be "ID" to show up
    "category": "rsg",              // Required: See Category Mapping below
    "version": "1.16.1",            // Optional: Version label (e.g., "1.16.1")
    "video": "https://youtu.be/...",// Optional: Link to the proof video
    "submitted": "2024-03-28T12:00:00Z", // Optional: ISO date string for sorting
    "seed": "1234567890"            // Optional: The world seed
  }
]
```

## 4. Common Run Object Specification
All runs (Verified, Pending, and Rejected) are converted into this uniform format for the UI:

| Property | Type | Description |
| :--- | :--- | :--- |
| `id` | `string` | Unique identifier (SRC ID or manual ID) |
| `player` | `string` | The runner's display name |
| `playerLink` | `string\|null` | URL to SRC profile (null for manual runs) |
| `time_ms` | `number` | Real-time in milliseconds |
| `time_igt_ms` | `number` | In-game time in milliseconds (falls back to `time_ms`) |
| `video` | `string\|null` | URL to the proof video |
| `date` | `string\|null` | YYYY-MM-DD formatted date |
| `status` | `string` | **`'rejected'`**, `'verified'`, or `'pending'` |
| `rank` | `number\|null` | Calculated placement |
| `tags` | `string[]` | Array of labels (e.g., `["1.16.1"]`) |
| `seed` | `string\|null` | The world seed |

## 5. Category Mapping (Exact)
The `category` field in `rejected.json` must match these specific keys based on the UI selection:

### Any% Glitchless
- **rsg**: Random Seed
- **ssg**: Set Seed

### Any% (Glitched)
- **rsi**: Random Seed + Internal
- **rse**: Random Seed + External
- **ssi**: Set Seed + Internal
- **sse**: Set Seed + External

### All Advancements (AA)
- **aarsg**: RSG
- **aassg**: SSG
- **aars**: RS
- **aass**: SS
