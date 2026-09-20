# AurasPay Merchant MCP

[![Smithery](https://smithery.ai/badge/mazenalshareef33/auraspay)](https://smithery.ai/servers/mazenalshareef33/auraspay)
[![MCP Badge](https://lobehub.com/badge/mcp/auraspayofficial-auraspay-mcp)](https://lobehub.com/mcp/auraspayofficial-auraspay-mcp)

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

## Tools

Tool availability is permission-aware. The authenticated `tools/list` response is authoritative for the current release and the scopes granted by the merchant. A tool listed below appears only when its required scope was requested during consent, granted by the merchant and enabled by AurasPay.

### Account and payments

- `auraspay_account_get` — Read the authenticated merchant profile.
- `auraspay_account_balance` — Read legacy dashboard counters; this is not a wallet balance.
- `auraspay_supported_tokens` — List the assets and networks currently allowed for the account.
- `auraspay_payments_list` — List owned payment requests with pagination.
- `auraspay_payment_get` — Read one owned payment request.
- `auraspay_payment_qr` — Retrieve the original stored QR image without regenerating it.
- `auraspay_payment_invoice` — Retrieve a completed-payment receipt or platform-fee PDF when available.
- `auraspay_invoice_settings` — Read invoice issuer settings without creating default records.
- `auraspay_payments_export_csv` — Export a selected payment page as spreadsheet-safe CSV.
- `auraspay_payments_analyze` — Analyze a selected page of payment activity.
- `auraspay_payments_report` — Build a complete bounded report using creation-date and payment filters.
- `auraspay_dashboard_stats` — Read owned payment counts and completed totals.
- `auraspay_payment_create` — Prepare a payment link request for separate authenticated merchant approval.
- `auraspay_payment_verify` — Verify an owned pending payment after its transaction signature is reviewed.

### Merchant profile and preferences

- `auraspay_profile_update` — Review profile changes before approving them in AurasPay.
- `auraspay_merchant_qualify` — Review store and country details before recording merchant qualification.
- `auraspay_preferences_get` — Read persisted notification, language, currency, theme and animation choices.
- `auraspay_preferences_update` — Persist selected preferences after native review.
- `auraspay_referrals_open` — Review before opening or initializing the owned referral program.

### Wallets

- `auraspay_ecosystem_overview` — Review linked wallets, cached balances and service readiness.
- `auraspay_wallet_ownership_challenge` — Create a short-lived wallet ownership message to sign.
- `auraspay_wallet_ownership_verify` — Verify the signature and save the exact receiving address.
- `auraspay_wallet_disconnect` — Remove one verified receiving address from AurasPay.

### Support

- `auraspay_tickets_list` — List owned support tickets with pagination.
- `auraspay_ticket_get` — Read one owned ticket and up to its first 200 messages.
- `auraspay_assistant_conversation` — Read the latest open support conversation and its first 50 messages.
- `auraspay_assistant_config` — Read assistant configuration availability; this is not a provider health check.
- `auraspay_ticket_set_status` — Close or reopen one owned ticket after native review.
- `auraspay_ticket_create` — Review and send a new support ticket in AurasPay.
- `auraspay_ticket_reply` — Review and send a reply to an owned support ticket.
- `auraspay_assistant_message` — Review and send one message to the support assistant or provider.

### Integrations

- `auraspay_plugins_list` — List official store-plugin downloads and documentation.
- `auraspay_api_keys_list` — Read masked API-key metadata, never full keys or hashes.
- `auraspay_webhooks_list` — Read webhook endpoint and delivery metadata, never secrets or destination URLs.
- `auraspay_webhook_secret_info` — Check whether a legacy signing secret exists without exposing it.
- `auraspay_merchant_setup_status` — Read recorded setup events; these are not proof of a live installation.
- `auraspay_api_key_revoke` — Revoke one key after native review; integrations using it will stop.
- `auraspay_webhook_revoke` — Revoke one endpoint after native review; notifications to it will stop.
- `auraspay_api_key_create` — Approve one-time API-key creation and display the secret only inside AurasPay, never in AI output.
- `auraspay_webhook_create` — Review a public HTTPS destination before creating a webhook.
- `auraspay_webhook_test` — Review and send one signed test event without automatically retrying an uncertain delivery.

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
