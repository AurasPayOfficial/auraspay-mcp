# AurasPay Merchant MCP

[![Smithery](https://smithery.ai/badge/mazenalshareef33/auraspay)](https://smithery.ai/servers/mazenalshareef33/auraspay)

AurasPay Merchant MCP connects compatible AI applications to an AurasPay merchant account through a hosted, OAuth-protected Model Context Protocol server.

It can read scoped merchant and payment information, export or analyze bounded payment data, and prepare supported merchant actions. Creating a payment link or changing merchant data requires a separate authenticated review in AurasPay.

## Connect

Remote MCP URL:

```text
https://mcp.auraspay.com/api/mcp
```

### Codex

```sh
codex mcp add auraspay --url https://mcp.auraspay.com/api/mcp
codex mcp login auraspay
```

Restart the Codex desktop app or IDE extension after adding the server. Use `/mcp` to confirm the connection.

### Claude Code

```sh
claude mcp add --transport http --scope user auraspay https://mcp.auraspay.com/api/mcp
```

Open `/mcp` inside Claude Code and complete authentication in the browser.

### Gemini CLI

Install the AurasPay extension directly from the official public repository:

```sh
gemini extensions install https://github.com/AurasPayOfficial/auraspay-mcp
```

Restart Gemini CLI, run `/mcp auth auraspay`, and complete OAuth in the browser.

### Visual Studio Code

[Install AurasPay in VS Code](https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%257B%2522name%2522%253A%2522auraspay%2522%252C%2522type%2522%253A%2522http%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fmcp.auraspay.com%252Fapi%252Fmcp%2522%257D)

You can also install it from a terminal:

```sh
code --add-mcp '{"name":"auraspay","type":"http","url":"https://mcp.auraspay.com/api/mcp"}'
```

For a workspace installation, copy [`.vscode/mcp.json`](.vscode/mcp.json) into your project. Run **MCP: List Servers**, start `auraspay`, trust the server, and complete OAuth in the browser.

### GitHub Copilot CLI

```sh
copilot mcp add --transport http auraspay https://mcp.auraspay.com/api/mcp
copilot mcp list
```

Complete OAuth when prompted. To configure it manually for your user account, merge [`examples/github-copilot-mcp-config.json`](examples/github-copilot-mcp-config.json) into `~/.copilot/mcp-config.json`. The root [`.mcp.json`](.mcp.json) is also ready for project-level Copilot CLI use after folder trust is confirmed.

### Devin

For Devin Local, which is the default agent in new Devin Desktop tabs:

```sh
devin mcp add --scope user auraspay https://mcp.auraspay.com/api/mcp
devin mcp login auraspay
devin mcp get auraspay
```

Complete OAuth in the browser when prompted. A copy-ready configuration for `~/.config/devin/mcp_config.json` is available at [`examples/devin-mcp_config.json`](examples/devin-mcp_config.json).

Legacy Cascade uses the Windsurf configuration described below. Team administrators can also add AurasPay through **Settings > MCP Marketplace > Add Your Own**, select **HTTP** and **OAuth**, enter the remote MCP URL, save it, and run **Test listing tools**.

### Cursor

[Add AurasPay to Cursor](https://cursor.com/link/mcp/install?name=auraspay&config=eyJ1cmwiOiJodHRwczovL21jcC5hdXJhc3BheS5jb20vYXBpL21jcCJ9)

For a manual installation, merge this entry into `~/.cursor/mcp.json` for all projects, or into `.cursor/mcp.json` inside one project:

```json
{
  "mcpServers": {
    "auraspay": {
      "url": "https://mcp.auraspay.com/api/mcp"
    }
  }
}
```

Open **Cursor > Customize > MCPs**, connect `auraspay`, and complete OAuth in the browser. Cursor Agent CLI users can run `cursor-agent mcp login auraspay` after saving the configuration.

### Windsurf / legacy Devin Desktop Cascade

Merge this entry into `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "auraspay": {
      "serverUrl": "https://mcp.auraspay.com/api/mcp"
    }
  }
}
```

In Windsurf or legacy Cascade, open the **MCPs** menu (or **Settings > Cascade > MCP Servers**), select `auraspay`, and complete OAuth in the browser. A copy-ready configuration is available at [`examples/windsurf-mcp_config.json`](examples/windsurf-mcp_config.json).

### Cline

```sh
cline mcp add --transport http --yes auraspay https://mcp.auraspay.com/api/mcp
```

Complete OAuth in the browser when Cline prompts you to authorize AurasPay. The
unauthenticated MCP endpoint intentionally returns `401 Unauthorized` together
with OAuth discovery metadata; that response means the protected server is
reachable and authentication must be completed, not that the service is down.

For automated availability checks that do not complete OAuth, use:

```text
https://mcp.auraspay.com/health
```

It returns HTTP `200` with `{"live":true}` while the MCP gateway is available.
See [`llms-install.md`](llms-install.md) for the complete Cline validation flow.

### Other clients

Choose Streamable HTTP, paste the remote MCP URL, and select OAuth when prompted. The client must support remote Streamable HTTP MCP, OAuth with PKCE, and Dynamic Client Registration.

## Safety model

- OAuth permissions are scoped and controlled by the merchant.
- Supported changes require a separate human review in AurasPay.
- A payment link is a payment request, not a transfer or proof that funds were received.
- Only authoritative `COMPLETED` status with matching payment details supports reconciliation.
- AurasPay never asks an MCP client for a wallet recovery phrase or private key.
- Test mode is metadata; it does not select a sandbox or testnet.

## Documentation and support

- Product guide: https://auraspay.com/mcp
- Arabic guide: https://auraspay.com/ar/mcp
- Privacy: https://auraspay.com/privacy-policy
- Terms: https://auraspay.com/terms-of-use
- Legal entities: https://auraspay.com/legal-entities
- Support: support@auraspay.com

## Scope of this repository

This public repository contains distribution metadata, client configuration and documentation for the hosted AurasPay Merchant MCP service. It does not contain production server source, credentials or merchant data.

## Regulatory boundary

AurasPay provides non-custodial software and technical infrastructure. AurasPay is not a bank, issuer, custodian or investment adviser. Availability can depend on jurisdiction and independent providers. Review the current legal pages above for details.
