# Agent Inbox Tools

Inbox-centric skills for coding agents. This bundle focuses on searching encrypted or private messages right from the CLI so an agent can answer questions about your communications without manual exporting.

## Skills

- **`signal-history-search`** — Direct SQL search against Signal Desktop's encrypted database on macOS. Sub-second queries using SQLCipher, no export required.
- **`apple-mail-search`** — Search Apple Mail via direct SQLite queries. Sub-second search across all configured accounts without launching Mail.app.

## Installation

```bash
npx add-skill NicolaiSchmid/agent-inbox-tools
```

## Why a dedicated bundle?

1. Messaging data is sensitive. Keeping Signal/Mail workflows together makes it clear which skills require trusted environments.
2. Future skills (send actions, summarizers, webhook forwards) can share configuration and documentation.
3. Keeps your main skills repo lean: install inbox tooling only when you need it.

## Contributing

Pull requests welcome! Please include usage notes, macOS checks, and appropriate security considerations in any new skill scripts.
