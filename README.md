# Agent Skills

Skills for coding agents to search private data sources. Each skill provides direct access to encrypted or local databases without manual exporting.

## Skills

| Skill | Description |
|-------|-------------|
| [signal-history-search](./skills/signal-history-search/) | Search Signal Desktop messages via SQLCipher. Sub-second queries on macOS. |
| [apple-mail-search](./skills/apple-mail-search/) | Search Apple Mail via SQLite. Fast search across all accounts without launching Mail.app. |
| [paperless-search](./skills/paperless-search/) | Search Paperless-ngx documents via REST API. Full-text search with tag/correspondent filtering. |

## Installation

Copy the desired skill folder to your agent's skills directory, or symlink it.

## Structure

Each skill contains:

- `SKILL.md` — Full documentation loaded by the agent
- `README.md` — Quick start for humans
- `scripts/` — Helper scripts (if any)

## Security

These skills access sensitive data:

- **Signal**: Decrypts local SQLite database using SQLCipher
- **Apple Mail**: Reads local SQLite mail index
- **Paperless**: Uses API token for authenticated requests

Only use in trusted environments.

## Contributing

Pull requests welcome. Please include:

- Clear usage examples
- Platform requirements
- Security considerations
