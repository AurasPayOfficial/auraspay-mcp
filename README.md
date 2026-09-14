# AurasPay Merchant MCP

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

### Cline

```sh
cline mcp add --transport http --yes auraspay https://mcp.auraspay.com/api/mcp
```

Complete OAuth in the browser when Cline prompts you to authorize AurasPay.

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
