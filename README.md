# Jack & Jill plugin

This plugin connects Cowork and Claude Code to the Jack & Jill candidate network and teaches Claude how to work a hiring assignment from research through a reviewed shortlist and consent-gated introduction.

## What it includes

- The production Jack & Jill remote MCP server, connected through OAuth.
- Static skills for assignment setup, research, candidate search, calibration, reports, feedback, and introductions.
- No API keys, customer data, or executable hooks.

## Connect

Install and enable the plugin. Claude will prompt you to sign in to Jack & Jill when it first needs the connector. Choose the Jill organization whose assignments you want Claude to work.

If you already installed the Jack & Jill directory connector, the plugin points to the same server. Claude shows one set of tools rather than duplicates.

## Develop

From the repository root:

```bash
claude plugin validate . --strict
claude --plugin-dir .
```

After connecting, call `whoami` and confirm the returned organization before doing any work.

## Support

- Connector documentation: https://platform.jackandjill.ai/marketplace-quickstart.md
- Product help: https://jackandjill.ai/docs/faqs
- Email: support@jackandjill.ai
