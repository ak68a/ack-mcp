# ack-mcp

MCP server for the [Agent Commerce Kit](https://github.com/agentcommercekit/ack) — exposes ACK-ID and ACK-Pay operations as tools for AI agents via the [Model Context Protocol](https://modelcontextprotocol.io/).

## Tools

| Tool | Description |
|------|-------------|
| `ack_generate_keypair` | Generate a cryptographic keypair with a `did:key` DID |
| `ack_create_did_web` | Create a `did:web` DID URI from a URL |
| `ack_create_did_pkh` | Create a `did:pkh` DID URI from a chain ID and wallet address |
| `ack_resolve_did` | Resolve a DID URI to its DID Document |
| `ack_create_controller_credential` | Create an unsigned controller credential (W3C VC) |
| `ack_sign_credential` | Sign a credential, returning a JWT |
| `ack_verify_credential` | Verify a signed credential JWT |
| `ack_create_jwt` | Create a signed JWT with an arbitrary payload |
| `ack_verify_jwt` | Verify a signed JWT and return its payload |
| `ack_create_payment_request` | Create a signed payment request token |
| `ack_verify_payment_request` | Verify and parse a payment request JWT |
| `ack_create_payment_receipt` | Create an unsigned payment receipt (W3C VC) |
| `ack_verify_payment_receipt` | Verify a signed payment receipt JWT |

## Quick start

### With Claude Code

```json
{
  "mcpServers": {
    "ack": {
      "command": "npx",
      "args": ["ack-mcp"]
    }
  }
}
```

### With Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "ack": {
      "command": "npx",
      "args": ["ack-mcp"]
    }
  }
}
```

### From source

```bash
git clone https://github.com/ak68a/ack-mcp.git
cd ack-mcp
npm install
npm start
```

## Development

```bash
npm install
npm test        # Run tests
npm run build   # Build for distribution
npm start       # Run the server (dev mode via tsx)
```

## How it works

The server uses stdio transport and registers 13 tools that wrap the [`agentcommercekit`](https://www.npmjs.com/package/agentcommercekit) SDK. An AI agent can:

1. **Generate identities** — create DIDs and keypairs
2. **Issue credentials** — create and sign W3C Verifiable Credentials proving agent-owner relationships
3. **Verify identities** — verify credentials and resolve DIDs
4. **Create payment requests** — issue signed payment request tokens for HTTP 402 flows
5. **Verify payments** — verify payment request tokens and payment receipts

All cryptographic operations use the ACK SDK's key management — keys are passed as JWK JSON strings between tool calls, and DIDs are used as identifiers throughout.

## License

MIT
