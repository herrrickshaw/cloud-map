# Cloud map — Dropbox and Google Drive storage inventory

A static inventory of the owner's two cloud storage accounts: file and byte counts per top-level
folder, size by file extension, and the largest files, for Dropbox (725,088 files, 517.0 GB) and
Google Drive (1,986 files, 9.6 GB). It exists so that clean-up and backup decisions (what to
archive, what is duplicated, where the market-data backups live) can be made from a table instead
of by browsing. The output is three Markdown files; there is no code in this repository.

> Status: archived snapshot. Generated once (initial commit 2026-08-31) by a script that is not in
> this repo; the numbers are not refreshed. Personal inventory, published for reference only.

> **New here?** See [How to use this repo with AI (Claude, Gemini, ChatGPT)](HOW_TO_USE_WITH_AI.md).

## What it contains
- `00_CLOUD_FILE_INDEX.md` — for each provider: the 15 largest top-level folders by size, the 15 heaviest
  file extensions, and the 15 largest individual files.
- `dropbox_folders.md` — all 185 top-level Dropbox folders with file count, size and the five dominant
  extensions in each.
- `gdrive_folders.md` — the same for all 67 top-level Google Drive folders.

## Quick start
Nothing to install. Read `00_CLOUD_FILE_INDEX.md` first, then the per-provider folder maps.

```bash
git clone https://github.com/herrrickshaw/cloud-map.git
cd cloud-map
```

## Headline figures (as of the snapshot)

| Provider | Files | Size | Largest folders |
|---|--:|--:|---|
| Dropbox | 725,088 | 517.0 GB | `market-data-backup` 88.8 GB · `backup of backups` 73.7 GB · `drive` 51.9 GB · `market-pipeline-cache` 28.5 GB · `market-data-archive` 24.1 GB |
| Google Drive | 1,986 | 9.6 GB | root 6.1 GB · `Claude` 765 MB · `Market-Data-Archive` 415 MB · `market-data-ec2` 337 MB |

Observations the tables support directly:
- Seven `.hds` virtual-disk images account for 69.4 GB of Dropbox; the same two Windows VM disks appear
  four times under different backup roots (`sonstiges`, `My Mac …`, `backup of backups/Horatio`).
- Parquet is the most numerous type on Dropbox (177,320 files, 34.5 GB), almost all under the
  market-data backup/archive folders.
- `backup of backups` is a copy of other backups (286,694 files, 73.7 GB).

## Repository layout
| Path | Purpose |
|---|---|
| `00_CLOUD_FILE_INDEX.md` | Summary tables for both providers |
| `dropbox_folders.md` | Per-folder Dropbox map |
| `gdrive_folders.md` | Per-folder Google Drive map |
| `HOW_TO_USE_WITH_AI.md` | How to hand this repo to an AI assistant |
| `CLAUDE.md` | Guidance for Claude Code sessions (source-fetching rules) |
| `.github/workflows/quality-gates.yml` | gitleaks secret scan on push / PR |

## Data sources
| Source | What is taken | Access route | Caveat |
|---|---|---|---|
| Owner's Dropbox account | File listing with sizes | Generated outside this repo (listing script not committed) | Point-in-time; counts drift as files move |
| Owner's Google Drive account | File listing with sizes | Same | Same |

No file contents are included — only paths, counts and sizes.

## Limitations and known issues
- The generating script is not in the repo, so the inventory cannot be regenerated from here.
- Some paths in the "largest files" tables are truncated at ~90 characters.
- Folder names reveal personal directory structure; nothing here is sensitive, but it is not a general-purpose tool.
- A few Google Drive folders show negative or near-zero sizes (e.g. `Meet Recordings` at −3.0 B), an artefact of how the listing summed Google-native documents.

## Related repositories
- Market-data backup folders listed here (`market-data-backup`, `market-data-archive`, `market-pipeline-cache`) are written by the owner's market-data pipeline repositories in this account.

## Licence
No licence file yet — all rights reserved.
