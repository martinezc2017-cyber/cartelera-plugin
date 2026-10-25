# Cartelera — AI video studio plugin

Turn an idea into a finished video from your AI assistant: animate a photo or a painting, make a commercial for your business,
a short series or story, a house tour, or a music video with an original song.

- **Plans for free**: script, scene photos and music.
- **Exact quote before spending**: animating scenes uses tokens and only runs after you approve, with a one-time code and a
  daily limit you choose.
- **Spanish and English.**

Website: https://cartelera.party · How to connect: https://cartelera.party/conecta-tu-ia

## Install

| Client | How |
|---|---|
| Claude | Settings → Plugins → search **Cartelera** → Add, then open its **Connectors** tab and sign in. Or add this repository as a marketplace. |
| Claude Code | `/plugin marketplace add martinezc2017-cyber/cartelera-plugin` then `/plugin install cartelera@cartelera-marketplace`, then `/mcp` to sign in. |
| Codex | Add this repository as a plugin marketplace (`.agents/plugins/marketplace.json`). |
| Cursor | Add this repository as a plugin marketplace (`.cursor-plugin/marketplace.json`). |
| ChatGPT | Package in [`openai/`](openai/) (ChatGPT plugin directory). |
| Any MCP client | Remote server `https://cartelera.party/mcp` (streamable HTTP, OAuth 2.1 with PKCE, dynamic client registration and client ID metadata documents). Listed in the official MCP Registry as `party.cartelera/cartelera`. |

## What's inside

- `plugins/cartelera/.mcp.json` — the hosted MCP server (`https://cartelera.party/mcp`). No local code, no API keys: you sign
  in with your Cartelera account through OAuth.
- `plugins/cartelera/skills/cartelera-videos/` — how the assistant should use the 18 tools (plan, quote, approve, deliver).

## Support

support@cartelera.party · Privacy: https://cartelera.party/privacidad · Terms: https://cartelera.party/terminos

Made by Toro Technology (Mexico).
