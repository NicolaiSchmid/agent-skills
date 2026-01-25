# Agent Inbox Tools

Inbox-centric skills for coding agents. This bundle focuses on searching and triaging encrypted or private conversations right from the CLI so an agent can answer questions about your communications without manual exporting.

## Skills

- `signal-history-search` — macOS-only skill that uses `sigexport` to stream-search Signal Desktop history from a temporary export. Supports chat selection, literal/regex search, and match context.
- `imap-search` *(coming soon)* — generic IMAP mailbox search for wasc.me and other accounts.
- `whatsapp-history-search` *(coming soon)* — WhatsApp Desktop chat scraping.

## Installation

```bash
npx add-skill NicolaiSchmid/agent-inbox-tools
```

## Why a dedicated bundle?

1. Messaging data is sensitive. Keeping Signal/IMAP workflows together makes it clear which skills require trusted environments.
2. Future skills (send actions, summarizers, webhook forwards) can share configuration and documentation.
3. Keeps your main skills repo lean: install inbox tooling only when you need it.

## Contributing

Pull requests welcome! Please include usage notes, macOS checks, and temporary file cleanup in any new skill scripts.
