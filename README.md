# Trader.AI plugin

Build, backtest and research trading strategies on [Trader.AI](https://trader.ai) from your AI assistant. You can also browse published strategies and the AI Trader leaderboard, and export strategies to MetaTrader 5.

The plugin has two parts:

- **The Trader.AI MCP server** (`https://trader.ai/api/mcp`) runs every action: building strategies, running backtests, listing published strategies and so on.
- **Agent skills** (`skills/`) tell the assistant when to use those tools, in what order, and how to present the results. They follow the open [Agent Skills](https://agentskills.io) format.

Installing the plugin gives you both parts. If you install only the skills, add the MCP server yourself (see [Connect the MCP server manually](#connect-the-mcp-server-manually)).

## Skills

| Skill | Use it to |
|---|---|
| `trader-ai-strategy-builder` | Get a strategy recommended, written or edited from plain-language entry, exit and risk rules |
| `trader-ai-backtest-research` | Backtest a strategy, judge whether the result is reliable, find out why it loses, compare versions, tune parameters, export to MetaTrader 5 |
| `trader-ai-strategy-discovery` | Browse top strategies and the AI Trader leaderboard, look up a creator, copy a strategy, publish or unpublish your own |

## Example prompts

- "Build a trend-following strategy for gold on the 1-hour chart with a 2x ATR stop."
- "Backtest my strategy on EURUSD for the last two years. Can I trust the result?"
- "Why does this strategy lose money in sideways markets, and what would you change?"
- "Show me the top published strategies for gold and copy one as my own."

## Install

**Claude Code**

```
/plugin marketplace add traderai-official/skills
/plugin install trader-ai@trader-ai
```

Then run `/mcp` and sign in to Trader.AI.

**Gemini CLI**

```
gemini extensions install https://github.com/traderai-official/skills
```

Then run `/mcp auth trader-ai` to sign in. Gemini CLI is no longer available to every Google account; if yours cannot use it, connect the MCP server in your current client instead (see below).

**ChatGPT**: install Trader.AI from the ChatGPT plugin directory. The ChatGPT version currently includes the MCP tools only, not these skills.

**Claude directory, Cursor Marketplace and Grok Build**: listings are coming soon. Until then, connect the MCP server manually as shown below.

## Connect the MCP server manually

If your client has no Trader.AI listing yet, or installed only the skills, add the server yourself:

| Client | How to add it |
|---|---|
| Claude Code | `claude mcp add --transport http trader-ai https://trader.ai/api/mcp` |
| Cursor (`mcp.json`) | `{ "mcpServers": { "trader-ai": { "url": "https://trader.ai/api/mcp" } } }` |
| Gemini CLI (`settings.json`) | `{ "mcpServers": { "trader-ai": { "httpUrl": "https://trader.ai/api/mcp" } } }` |
| Claude.ai | Settings → Connectors → Add custom connector → `https://trader.ai/api/mcp` |

## Network access and credentials

- **Endpoint**: the plugin connects only to trader.ai: the MCP server at `https://trader.ai/api/mcp` and sign-in at `https://trader.ai/connect/`. The skills contain no scripts and make no other network calls.
- **Sign-in**: OAuth through your Trader.AI account, handled by `https://trader.ai/connect/`. You never paste an API key or password into the assistant.
- **What is sent**: the requests you make, such as strategy rules, a short summary of what you asked for when a strategy is saved, and backtest settings. They are stored in your Trader.AI account as described in the privacy policy.
- **Account and plan**: you need a Trader.AI account. Backtests and other actions count toward your plan's limits, and some features, such as MetaTrader 5 export, may require a paid plan.

## Scope

The plugin builds, tests and researches strategies. It does not place orders, quote live prices or give personal investment advice. Backtest results describe the past and do not predict future returns. Trading involves risk; read the [Risk Disclosure](https://trader.ai/legal/risk-disclosure) before trading.

## Privacy and support

- Privacy policy: <https://trader.ai/legal/privacy-policy>
- Terms of service: <https://trader.ai/legal/terms-of-service>
- Risk disclosure: <https://trader.ai/legal/risk-disclosure>
- Support: <https://trader.ai/contact> · support@trader.ai

## License

[MIT](LICENSE)
