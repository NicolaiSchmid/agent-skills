# Paperless Document Search

Search documents in Paperless-ngx via REST API.

Full-text search, tag/correspondent filtering, and direct links to view documents in browser.

## Quick Start

```bash
# Configure (one-time)
export PAPERLESS_URL="https://paperless.example.com"
export PAPERLESS_TOKEN="your-token"

# Search documents
paperless-search search --query "invoice 2025"

# Filter by tag
paperless-search search --tag "tax"

# List all tags
paperless-search tags

# Get recent documents
paperless-search recent --limit 10
```

## Requirements

- bash, curl, jq
- Paperless-ngx instance with API access

## Documentation

See [SKILL.md](./SKILL.md) for full documentation, all commands, and troubleshooting.
