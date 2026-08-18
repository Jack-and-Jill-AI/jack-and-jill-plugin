# Jack & Jill plugin

This plugin connects ChatGPT, Codex, Cowork, and Claude Code to the Jack & Jill candidate network. Its skills teach the model how to work a hiring assignment from research through a reviewed shortlist and consent-gated introduction.

## What it includes

- The production Jack & Jill remote MCP server, connected through OAuth.
- Static, provider-neutral skills for assignment setup, research, candidate search, calibration, reports, feedback, and introductions.
- No API keys, customer data, executable hooks, subagents, or local software dependencies.

## Connect

Install and enable the plugin. The host prompts you to sign in to Jack & Jill when it first needs the connector. Choose the Jill organization whose assignments you want the model to work.

If the same Jack & Jill MCP server is already connected, the plugin and existing connection point to one tool surface rather than creating a second server implementation.

After connecting, call `whoami` and confirm the returned organization before doing any work.

## Anthropic

Anthropic accepts this repository directly for Cowork and Claude Code. The bundled `.mcp.json` points to the production remote connector.

Validate it with:

```bash
claude plugin validate . --strict
claude --plugin-dir .
```

## OpenAI

OpenAI accepts Claude Code plugin archives and converts `.claude-plugin/plugin.json` to `.codex-plugin/plugin.json`. Use a **With MCP** submission so the same skills are available in ChatGPT and Codex.

The OpenAI submission registers and scans the production MCP endpoint separately. It does not rely on this repository's `.mcp.json` as the server registration.

See [OPENAI.md](OPENAI.md) for the packaging and submission steps.

## Support

- Connector documentation: https://platform.jackandjill.ai/marketplace-quickstart.md
- Product help: https://jackandjill.ai/docs/faqs
- Email: support@jackandjill.ai
