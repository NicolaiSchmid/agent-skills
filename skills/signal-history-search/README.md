# Signal History Search

Search Signal Desktop message history on macOS with sub-second query times. Queries the encrypted SQLite database directly using SQLCipher - no export required.

```bash
npx skills add nicolaischmid/agent-skills/skills/signal-history-search
```

## Quick Start

```bash
# List all chats
signal-search list

# Search messages
signal-search search --query "meeting" --chat "John"

# Dump messages from a specific day
signal-search dump --date "2025-01-25"
```

## Requirements

- macOS
- Signal Desktop (logged in)
- nix-shell

## Documentation

See [SKILL.md](./SKILL.md) for full documentation, all commands, and troubleshooting.
