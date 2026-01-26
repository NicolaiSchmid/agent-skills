# Apple Mail Search

Search Apple Mail messages on macOS via direct SQLite queries. Sub-second search across all configured mail accounts without launching Mail.app.

```bash
npx skills add nicolaischmid/agent-skills/skills/apple-mail-search
```

## Quick Start

```bash
# List accounts
mail-search accounts

# Search by subject
mail-search search --subject "invoice"

# Search by sender
mail-search search --sender "amazon.com"

# Get recent messages
mail-search recent --limit 10
```

## Requirements

- macOS
- Apple Mail (configured with at least one account)
- Python 3

## Documentation

See [SKILL.md](./SKILL.md) for full documentation, all commands, and troubleshooting.
