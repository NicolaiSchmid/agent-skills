---
name: paperless-search
description: Search documents in Paperless-ngx via REST API. Full-text search, tag/correspondent filtering, and direct links to documents.
license: MIT
metadata:
  author: Nicolai Schmid
  version: 1.0.0
  requires:
    - bash
    - curl
    - jq
    - Paperless-ngx instance with API access
scripts:
  search: ./scripts/paperless-search
---

# Paperless Document Search

Search your Paperless-ngx document archive via the REST API. Fast queries with full-text search, filtering by tags/correspondents/dates, and clickable links to view documents in the browser.

## When to use

- You need to find a specific document (invoice, receipt, contract, etc.)
- You want to search document content (OCR text) without opening the web UI
- You need to filter documents by tags, correspondents, or date ranges
- You want quick access to document metadata and direct links

## How it works

1. Authenticates with your Paperless-ngx instance via API token
2. Sends search queries to the `/api/documents/` endpoint
3. Returns document metadata, OCR snippets, and clickable URLs
4. All operations are read-only; nothing is modified

## Configuration

Set these environment variables:

```bash
export PAPERLESS_URL="https://paperless.example.com"
export PAPERLESS_TOKEN="your-api-token-here"
```

To get an API token:

1. Log into your Paperless web UI
2. Click your username (top right) -> "My Profile"
3. Click the circular arrow button to generate/regenerate a token

Alternatively, create `~/.config/paperless-search/config.json`:

```json
{
  "url": "https://paperless.example.com",
  "token": "your-api-token-here"
}
```

Environment variables take precedence over the config file.

## Usage

```bash
# Full-text search across all documents
paperless-search search --query "invoice january 2025"

# Search with tag filter
paperless-search search --query "payment" --tag "expenses"

# Filter by correspondent
paperless-search search --correspondent "ACME Corp"

# Filter by document type
paperless-search search --type "Invoice"

# Date range search
paperless-search search --query "contract" --after "2025-01-01" --before "2025-06-30"

# Combine filters
paperless-search search --tag "tax" --correspondent "IRS" --after "2024-01-01"

# List all tags
paperless-search tags

# List all correspondents
paperless-search correspondents

# List all document types
paperless-search types

# Get recent documents
paperless-search recent --limit 20

# Read full metadata and OCR content for a document
paperless-search read --id 1234
```

### Commands

| Command          | Description                                    |
| ---------------- | ---------------------------------------------- |
| `search`         | Search documents with optional filters         |
| `tags`           | List all available tags                        |
| `correspondents` | List all correspondents                        |
| `types`          | List all document types                        |
| `recent`         | Get most recent documents                      |
| `read`           | Show full metadata and OCR text for a document |

### Search Flags

| Flag                     | Short | Description                                |
| ------------------------ | ----- | ------------------------------------------ |
| `--query <text>`         | `-q`  | Full-text search query                     |
| `--tag <name>`           | `-t`  | Filter by tag (can be used multiple times) |
| `--correspondent <name>` | `-c`  | Filter by correspondent                    |
| `--type <name>`          | `-T`  | Filter by document type                    |
| `--after <YYYY-MM-DD>`   |       | Documents created after this date          |
| `--before <YYYY-MM-DD>`  |       | Documents created before this date         |
| `--limit <n>`            | `-n`  | Maximum results (default: 25)              |

### Output Format

```
[1234] 2025-01-15 | Invoice - ACME Corp - January 2025
       Correspondent: ACME Corp | Type: Invoice
       Tags: tax, 2025, expenses
       https://paperless.example.com/documents/1234/details

[1235] 2025-01-10 | Receipt - Office Supplies
       Correspondent: Staples | Type: Receipt
       Tags: expenses, office
       https://paperless.example.com/documents/1235/details
```

- First line: Document ID, date, title
- Second line: Correspondent and document type
- Third line: Tags
- Fourth line: Direct link to document in web UI

When using `--query`, search highlights are included:

```
[1234] 2025-01-15 | Invoice - ACME Corp - January 2025
       ...payment of <match>$500</match> received for <match>January</match>...
       https://paperless.example.com/documents/1234/details
```

## Performance

| Operation                | Time  |
| ------------------------ | ----- |
| Full-text search         | <1s   |
| List tags/correspondents | <0.5s |
| Read document details    | <0.5s |

## Security Considerations

- API token is stored locally (env var or config file)
- All requests use HTTPS (assuming your Paperless instance is configured with TLS)
- Read-only operations; the skill cannot modify documents
- Nothing is cached or written to disk beyond configuration

## Troubleshooting

- **"Connection refused"**: Check that PAPERLESS_URL is correct and the server is running
- **"401 Unauthorized"**: Verify your API token is valid (regenerate in web UI if needed)
- **"No results"**: Try broader search terms; Paperless uses AND for multiple words by default
- **Slow responses**: Check network connectivity to your Paperless server
- **Missing documents**: Ensure the API user has permission to view the documents

## Limitations

- Search syntax follows Paperless-ngx conventions (see their docs for advanced queries)
- Cannot modify, upload, or delete documents (by design)
- Requires network access to the Paperless instance
