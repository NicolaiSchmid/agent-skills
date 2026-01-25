---
name: signal-history-search
description: Search Signal Desktop message history on macOS without keeping exported files. Streams sigexport output into ripgrep with chat filters, literal/regex modes, and context options.
license: MIT
metadata:
  author: Nicolai Schmid
  version: 0.2.0
  requires:
    - macOS
    - Signal Desktop (logged in)
    - nix-shell
scripts:
  search: skills/signal-history-search/scripts/signal-history-search
---

# Signal History Search

Use `sigexport` from `signal-export` (via nix-shell) to pull a temporary copy of the target chat, then run `rg` across the export. Files live in `/tmp/signal-search.*` and are deleted automatically unless `--keep-temp` is passed.

## When to use

- You need to quote or summarize prior Signal conversations during coding tasks.
- You already have Signal Desktop installed on macOS.
- You prefer not to leave exported chats on disk.

## Skill behaviour

1. Validates macOS and Signal Desktop presence.
2. Creates a temp directory (`mktemp -d`).
3. Runs `nix-shell -p signal-export ripgrep --command "sigexport … && rg …"`.
4. Cleans up the temp directory.

## Usage

```bash
# List chats (filter after the fact)

# Full-text search within a chat
signal-history-search search --chat "Dariush Wahdany" --query "wire transfer" --context 2

# Literal, case-sensitive search across all chats, keep export for inspection
signal-history-search search --query "acct_123" --literal --case-sensitive --keep-temp
```

### Flags

| Flag | Description |
| ---- | ----------- |
| `--chat <name>` | Restrict export to a named chat (exact match per sigexport). |
| `--query <pattern>` | Required search pattern (regex by default, literal with `--literal`). |
| `--before/--after/--context` | Provide ripgrep context lines. |
| `--max-count <n>` | Stop after _n_ matches. |
| `--keep-temp` | Leave export in `/tmp` for debugging. |
| `list --filter <pattern>` | List available chats before exporting. |

## Security considerations

- Temporary exports live under `/tmp/signal-search.*`. They’re deleted on exit; inspect with `--keep-temp` if necessary.
- Running `sigexport` unlocks your local Signal database using macOS keychain keys. The process inherits your local permissions only.
- Searches happen locally; nothing leaves your machine.

## Troubleshooting

- `nix-shell: command not found` → install Nix or adjust the script to call another package manager providing `signal-export`.
- `Signal Desktop directory not found` → ensure the desktop app ran at least once (creates `~/Library/Application Support/Signal`).
- No matches? Use `--literal` for raw string search or `--keep-temp` to inspect exported JSON structure.
