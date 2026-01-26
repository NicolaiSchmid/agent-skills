# Paperless Document Search

Search documents in Paperless-ngx via REST API.

Full-text search, tag/correspondent filtering, and direct links to view documents in browser.

## Quick Start

```bash
# Load config
PAPERLESS_URL=$(jq -r .url ~/.config/paperless-search/config.json)
PAPERLESS_TOKEN=$(jq -r .token ~/.config/paperless-search/config.json)

# Search documents
curl -s -H "Authorization: Token $PAPERLESS_TOKEN" \
  "$PAPERLESS_URL/api/documents/?query=invoice+2025" | jq '.results[] | {id, title}'

# Get document with full content
curl -s -H "Authorization: Token $PAPERLESS_TOKEN" \
  "$PAPERLESS_URL/api/documents/123/" | jq -r '.content'
```

## Requirements

- curl, jq
- Paperless-ngx instance with API access

## Documentation

See [SKILL.md](./SKILL.md) for full documentation, API reference, and troubleshooting.
