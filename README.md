# NEMO x402 Micro-Services (AgentX Gateway)

Twelve **pay-per-call agent micro-services** served over the x402 protocol (USDC on Base + Solana), exposed as a remote **Streamable-HTTP MCP server** plus plain x402 HTTP endpoints.

- **MCP endpoint:** `https://agentx.sale/x402/mcp` (Streamable HTTP)
- **Machine catalogue (free):** `https://agentx.sale/x402/catalogue`
- **Health (free):** `https://agentx.sale/x402/health`
- **llms.txt:** `https://agentx.sale/llms.txt`

## Services

| Route | Price | What it does |
|---|---|---|
| `GET /x402/weather?city=` | $0.01 | Current weather for any city (Open-Meteo) |
| `GET /x402/site-health?host=` | $0.01 | DNS / TLS certificate / HTTP status + latency snapshot |
| `GET /x402/x402-check?url=` | $0.02 | **x402 Doctor** — is a URL a valid agent-payable paid resource? Reads both x402 v1 (body) and v2 (PAYMENT-REQUIRED header) specs; grade A–F |
| `GET /x402/seo-audit?host=` | $0.10 | Rules-based SEO + agent-readiness audit with score |
| `GET /x402/agent-card?host=` | $0.02 | Site Agent-Readiness Verdict Card — llms.txt, A2A card, MCP card, OpenAPI, TLS, headers, AI-crawler policy |
| `GET /x402/protocol-lint?url=` | $0.02 | A2A / MCP protocol card lint with drop-in patched JSON fixes |
| `GET /x402/crawler-policy?host=` | $0.02 | TLS + security headers + AI-crawler policy matrix (GPTBot, ClaudeBot, Google-Extended, PerplexityBot…) |
| `GET /x402/webmcp-check?host=` | $0.10 | WebMCP agent-compatibility check |
| `POST /x402/webmcp-upgrade` | $4.00 | Generated webmcp.js tool file with publish instructions |
| `POST /x402/classify` | $1.75 | AI topic classification of supplied text |
| `POST /x402/keywords` | $0.90 | AI keyword extraction |
| `GET or POST /x402/gtm-roast` | $0.02 | New Landing Page Roast — five persona critiques plus a shareable SVG card |

## Example MCP client config

```json
{
  "mcpServers": {
    "nemo-x402": {
      "url": "https://agentx.sale/x402/mcp",
      "transport": "streamable-http"
    }
  }
}
```

Free via MCP: `nemo_x402_catalogue` (full service menu with prices + settlement details) and `agentx_x402_doctor` (the x402 Doctor, free over MCP).

## Payments

x402 protocol v2. Every paid endpoint returns HTTP 402 with a `PAYMENT-REQUIRED` challenge; agents pay USDC (Base first, Solana also accepted) and receive the result in the same call. No accounts, no API keys.

## Provider

NEMO AI Solutions — [nemoai.uk](https://nemoai.uk) · marketplace storefront: [agentx.sale](https://agentx.sale)

---
This public repo is the catalogue/metadata twin of the gateway (the gateway's source code lives in a private repo). `server.json` here matches the entry published to the official MCP Registry.
