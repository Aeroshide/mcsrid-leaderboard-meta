# mcsrindo-leaderboard-meta

Metadata repository for the **Indonesian Minecraft Java Edition Speedrun Leaderboard** at [mcsrid-leaderboard.aeroshide.com](https://mcsrid-leaderboard.aeroshide.com).

This repo holds manual-curated run data that lives outside the official [speedrun.com](https://speedrun.com/mc) leaderboard - typically runs that are trusted and recognized by the Indonesian MCSR community but couldn't be verified through the normal SRC process.

## Contributing

PRs are welcome! If you have a run that you *think* belongs here, open a pull request adding your entry to `rejected.json`. Before submitting, please read **[REJECTED_RUNS_SPEC.md](./REJECTED_RUNS_SPEC.md)** as it covers the full JSON schema, category keys, and how the data gets consumed by the leaderboard.

A few ground rules:
- `country_code` must be `"ID"`, this is a leftover backend check and the key MUST be `"ID"` for it to show up on the leaderboard
- `id` must be unique, use a descriptive string like `[category]_[playername]_[incrementalnumber]` for example `rsg_hasbi_001`
- Video proof is required, even if backend techincally accepts no video. (`video` field)
- Before this, you should build up reputation in the Discord first: [discord.gg/ctqTXu3UYD](https://discord.gg/ctqTXu3UYD)

## Community

This leaderboard is part of the Indonesian MCSR infrastructure as i think this is the only one that exists as of now. If you want to get involved beyond just submitting runs, come say hi on our [Discord](https://discord.gg/ctqTXu3UYD).