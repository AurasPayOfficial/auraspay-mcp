# Install AurasPay Merchant MCP in Cline

## Connection

- Name: `auraspay`
- Transport: Streamable HTTP
- MCP URL: `https://mcp.auraspay.com/api/mcp`
- Authentication: OAuth 2.0 authorization code with PKCE S256 and Dynamic Client Registration

Install from Cline CLI:

```sh
cline mcp add --transport http --yes auraspay https://mcp.auraspay.com/api/mcp
```

When Cline opens the browser, sign in to the AurasPay merchant account, review
the requested scopes, and approve or deny access. Do not paste an AurasPay
password, OAuth token, wallet recovery phrase, private key, or API secret into
Cline or into a public issue.

## Validation

1. Check `https://mcp.auraspay.com/health`. A reachable gateway returns HTTP
   `200` with `{"live":true}`.
2. Connect to `https://mcp.auraspay.com/api/mcp` using Streamable HTTP.
3. Before OAuth, expect HTTP `401 Unauthorized` with a `WWW-Authenticate`
   challenge containing `resource_metadata`. This is the expected protected
   server response, not an unhealthy status.
4. Complete OAuth in the browser and let Cline reconnect.
5. Confirm that Cline can list the AurasPay tools. Tool access depends on the
   scopes granted by the merchant.

Creating a payment link prepares a payment request for separate authenticated
human review in AurasPay. It does not transfer money and is not proof that a
customer paid.

## Troubleshooting

- If Cline reports `Unauthorized`, reconnect and finish the browser OAuth flow.
- If no browser opens, remove the incomplete Cline MCP entry, add it again, and
  allow Cline to open its loopback OAuth callback.
- If the health URL does not return HTTP `200`, contact `support@auraspay.com`
  with the UTC time and the non-sensitive error text.
