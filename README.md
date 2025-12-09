# 1mg MCP Server

An MCP server to bring essential 1mg experiences—medicine search, ordering, and recent order history—directly into your AI tools.

> **Tested with:** Claude Desktop, ChatGPT (Plus/Pro), and DeputyDev (VSCode)

> **Disclaimer:**
> This integration is for internal/testing purposes only. 1mg disclaims any liabilities arising from incorrect functionality, incomplete features, or erroneous MCP interactions.

---

## Supported Features

- 🔎 **Medicine Search** – Search medicines by name, salt, or brand.
- 🛒 **Cart Management** – Add, remove, update, or review items in your cart.
- 🧾 **End-to-End Ordering** – Place orders directly from chat; heavy operations run in the background.
- 💳 **Integrated Payments** – Supports UPI payments in-chat and online payment links.
- ❌ **Order Cancellation** – Cancel eligible orders quickly via conversation.
- 📜 **Recent Order History** – View recent orders and their statuses.
- 🔐 **OAuth 2.1 Modular Identity Component** – 1mg acts as an Identity Provider (IdP) for SSO use cases across tools.

---

## Installation Guide

Add the following configuration to your `mcp.json` file for Claude Desktop, VSCode MCP clients, DeputyDev, GitHub Copilot, or other MCP-enabled tools.

### Standard Configuration (Mac/Linux via Zsh)
```json
{
  "servers": {
    "1mg-mcp": {
      "command": "/bin/zsh",
      "args": [
        "-lc",
        "npx -y mcp-remote https://mcp.1mg.com/mcp"
      ],
      "connection_timeout": 4000,
      "read_timeout": 400
    }
  }
}
```

## NOTE - Please use equivalent timeouts as some tools will monitor for specific flows and return in a slightly longer amount of time. Example, polling for UPI transactions.

### Alternative Configurations

You can adapt the configuration depending on your environment or if you prefer running `npx` directly without a shell wrapper.

**Option 1: Running `npx` directly (Cross-Platform)**
Useful if you want to skip the shell wrapper or are on an environment where `npx` is in the path.
```json
{
  "servers": {
    "1mg-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mcp.1mg.com/mcp"
      ]
    }
  }
}
```

**Option 2: Different Shells**
You can replace `/bin/zsh` with your preferred shell, such as `/bin/bash` or `powershell`.
```json
{
  "servers": {
    "1mg-mcp": {
      "command": "/bin/bash",
      "args": [
        "-c",
        "npx -y mcp-remote https://mcp.1mg.com/mcp"
      ]
    }
  }
}
```

Make sure **Node.js** and **npx** are installed and updated regardless of the method chosen.

---

### Notes

**Claude Desktop Free users:** Enable custom MCP connectors using: `Connect Local Servers`

**ChatGPT Plus & Pro Users:** Connect directly via `https://mcp.1mg.com/mcp`  
Follow OpenAI’s guide: **Connectors in ChatGPT**

After configuring and restarting your client, you will be guided to authorize your 1mg account. This enables access to cart actions, order history, and payments.

### Troubleshooting Tips

* Clear cookies or local storage if experiencing connection issues in browser clients.
* Some older MCP clients may not support the required protocol specification.
* ChatGPT requires OAuth mode; no client ID or secret is needed.
