---
name: jack-and-jill-setup
description: Connect the Jack & Jill plugin to the right Jill organization and verify access before starting recruiting work.
---

# Set up Jack & Jill

The plugin includes the Jack & Jill remote MCP server. It uses OAuth, so never ask the user to paste an API key or access token.

1. Enable the plugin and open its **jack-and-jill** connector.
2. Choose **Connect** or **Sign in** when Claude asks.
3. Sign in to Jill and approve the organization that owns the hiring work.
4. Call `whoami`.
5. Show the returned organization name and ask the user to confirm it if their request did not already identify the organization.

Stop if `whoami` returns the wrong organization. The user can revoke or reconnect the connection from Jill's Connections page.

Once the organization is confirmed, use the `start-jack-and-jill` skill to orient to its assignments and notifications.
