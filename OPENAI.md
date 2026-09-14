# Submit to OpenAI

OpenAI supports direct conversion of Claude Code plugins. This directory is the skills archive for a plugin backed by the existing Jack & Jill MCP server.

Official guide: https://developers.openai.com/plugins/guides/submit-claude-plugin

## Package the archive

This directory is the archive root. Hidden `.claude-plugin` must be included.

From `marketplace_plugin/` in ai-recruiter:

```bash
git archive --format=zip --output jack-and-jill-plugin.zip HEAD:marketplace_plugin
```

From a clone of [jack-and-jill-plugin](https://github.com/Jack-and-Jill-AI/jack-and-jill-plugin):

```bash
git archive --format=zip --output jack-and-jill-plugin.zip HEAD
```

The archive root contains:

- `.claude-plugin/plugin.json` with a non-empty description;
- `skills/<skill-name>/SKILL.md` for each provider-neutral skill;
- no local MCP server, hooks, subagents, credentials, or local package dependencies.

## Submit with MCP

1. Open https://platform.openai.com/plugins and select **Create plugin**.
2. Choose **With MCP**.
3. Submit this production Streamable HTTP endpoint:

   ```text
   https://platform.jackandjill.ai/mcp/marketplace/v1/
   ```

4. Configure OAuth 2.1 and complete the normal Jack & Jill sign-in flow.
5. Upload `jack-and-jill-plugin.zip` as the skills bundle in the same draft.
6. Review the generated `.codex-plugin/plugin.json`. OpenAI converts the Claude manifest and adds its interface defaults.
7. Run **Scan Tools**, resolve every scan finding, and test the skills in a clean ChatGPT and Codex environment.
8. Complete the listing, starter prompts, five positive cases, three negative cases, country availability, policy attestations, and release notes.

Submit the MCP endpoint as a new server-backed plugin. Do not reference an Anthropic connector listing or rely on `.mcp.json` to register the server with OpenAI.

## Compatibility rules

Keep skill instructions provider-neutral. Do not add behavior that depends on:

- Claude-only live artifacts;
- Claude installation prompts or `userConfig` expansion;
- local `stdio` MCP servers;
- prompt, agent, or other hooks required for the core ChatGPT workflow;
- undeclared local files, packages, credentials, or executables.

Credentials and persistent organization access stay in the remote MCP server's OAuth flow.
