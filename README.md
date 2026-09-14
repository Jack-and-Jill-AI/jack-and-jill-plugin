# Jack & Jill marketplace plugin

Skills archive for hosts that connect to `https://platform.jackandjill.ai/mcp/marketplace/v1/`. Zip this directory for ChatGPT and Codex. Claude Code and Cowork can load it with `--plugin-dir marketplace_plugin`.

The public copy is [jack-and-jill-plugin](https://github.com/Jack-and-Jill-AI/jack-and-jill-plugin). Turret's sandbox still curls that repo (`PLATFORM_PLUGIN_COMMIT` in `turret/worker/src/sandbox/lifecycle/platform-plugin.ts`). Publish this tree there before bumping the pin.

Marketplace MCP ships tools only. These files are how ChatGPT, Claude, and Cursor learn the workflow. They teach the marketplace contract (`hard_filters`, `review_matches`, `list_notifications`) and stay off the legacy `/mcp/` handbook and v2 surfaces.

## What it includes

- The production Jack & Jill remote MCP server, connected through OAuth.
- Static, provider-neutral skills for assignment setup, research, hard-filtered candidate search, calibration, in-host review, the daily pass, and consent-gated introductions.
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

From ai-recruiter, point `--plugin-dir` at this directory (`marketplace_plugin`).

## OpenAI

OpenAI accepts Claude Code plugin archives and converts `.claude-plugin/plugin.json` to `.codex-plugin/plugin.json`. Use a **With MCP** submission so the same skills are available in ChatGPT and Codex.

The OpenAI submission registers and scans the production MCP endpoint separately. It does not rely on this repository's `.mcp.json` as the server registration.

See [OPENAI.md](OPENAI.md) for the packaging and submission steps.

## Check the contract

```bash
./scripts/check-skills.sh
```

## Support

- Connector documentation: https://platform.jackandjill.ai/marketplace-quickstart.md
- Product help: https://jackandjill.ai/docs/faqs
- Email: support@jackandjill.ai
