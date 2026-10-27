# LoreKeeper MCP server

**The official MCP connector from LoreKeeper Ltd ([www.lorekeeper.com](https://www.lorekeeper.com/mcp)).**

**Mess in. Magic out.** Pour in your D&D and tabletop RPG notes and documents, however messy, and LoreKeeper organises them into a safe, private store for your world: session recaps, setting notes, and characters with their portraits. Then open Claude, ChatGPT or any MCP app and ask about your world, or have it build you a sourcebook, all from what you wrote. It never changes a word of your lore.

[![LoreKeeper MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.lorekeeper/lorekeeper/badges/score.svg)](https://glama.ai/mcp/connectors/com.lorekeeper/lorekeeper)

> This repository holds the documentation and registry metadata for the hosted server. The server itself runs at `api.lorekeeper.com`; there is nothing to install or run.

## Connect

| | |
|---|---|
| **Address** | `https://api.lorekeeper.com/mcp` |
| **Transport** | Streamable HTTP |
| **Sign-in** | OAuth 2.1 with dynamic client registration and PKCE (S256). You sign in with your LoreKeeper account and press **Allow** |
| **Registry name** | `com.lorekeeper/lorekeeper` ([MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=lorekeeper)) |

Every LoreKeeper plan can connect. You need a LoreKeeper account with at least one world ([sign up free](https://www.lorekeeper.com)).

### Claude (web, desktop, phone)

[**Add LoreKeeper to Claude**](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=LoreKeeper&connectorUrl=https%3A%2F%2Fapi.lorekeeper.com%2Fmcp) opens Claude with the form already filled in.

To add it by hand:
1. In Claude, open **Customize** → **Connectors**.
2. Press **Add**, then **Add custom connector**.
3. Name it **LoreKeeper**, paste `https://api.lorekeeper.com/mcp`, press **Continue**, then **Add**.
4. Press **Connect**, sign in if asked, then press **Allow**.

**Tip:** to stop Claude asking before every lookup, go to **Customize** → **Connectors** → **Yours** → **LoreKeeper** and set **Read-only tools** to **Always allow**.

### ChatGPT (web, phone)

1. In ChatGPT, open **Plugins** in the sidebar.
2. Press **Add**, then **Add custom MCP server**.
3. Name it **LoreKeeper** and paste `https://api.lorekeeper.com/mcp`.
4. Tick **I understand and want to continue** and press **Create as a plugin**.
5. Open the plugin, press **Connect**, sign in if asked, then press **Allow**.

### Claude Code

```sh
claude mcp add --transport http --scope user lorekeeper https://api.lorekeeper.com/mcp
claude mcp login lorekeeper
```

### Cursor and other MCP apps

```json
{
  "mcpServers": {
    "lorekeeper": { "url": "https://api.lorekeeper.com/mcp" }
  }
}
```

Apps that can't sign in can use a personal token instead: create one in LoreKeeper under **Account → Connections → For developers**, and send it as `Authorization: Bearer <token>`.

## Try asking

Name LoreKeeper in the prompt, so the assistant doesn't reach for its own memory first.

- "Using my LoreKeeper world, build me a sourcebook for the city of Varnholt: its history, factions, key NPCs and three adventure hooks, all from my notes."
- "Using LoreKeeper, what did the party promise the mayor of Varnholt, and which session recap says so?"
- "From my LoreKeeper world, give me a previously-on, the open threads and the NPCs likely to come back next session."
- "Pull Captain Vela from LoreKeeper, show me her portrait, and draft three lines she would say about the missing ship."
- "Check this twist against my LoreKeeper lore and point out anything it contradicts, with the document it comes from."
- "List my LoreKeeper worlds."

## Tools

| Tool | What it does |
|---|---|
| `list_worlds` | Lists your worlds and their ids |
| `search_lore` | Finds the passages in a world's Lore Library that answer a question, naming the source document |
| `list_lore` | Lists a world's documents, by folder |
| `read_lore` | Reads a whole document, in pages |
| `find_characters` | Finds characters in a world by name |
| `get_character` | A character's look, personality, voice, backstory and sheet |
| `get_character_images` | The portraits and reference sheets you saved for a character |
| `check_credits` | Your LoreKeeper credit balance |
| `make_character_picture` | Makes a new picture of a character. **Spends credits**, and only if you allowed spending when you connected |
| `make_world_picture` | Makes a new picture for a world. **Spends credits**, and only if you allowed spending when you connected |

The first seven tools only read; they cannot add, change or delete anything in your account. A picture costs 150 credits, with a limit of 1,500 credits a day across all your connected apps.

**Read-only address:** `https://api.lorekeeper.com/mcp/read` is the same server with the first seven tools only. It never makes pictures, whatever you allow.

## Privacy and security

- A connection reads only the worlds in the LoreKeeper account that signed in.
- Spending credits on pictures is off unless you tick it on the sign-in page. You can switch it on or off later.
- To end a connection, remove LoreKeeper from your app, or revoke it in LoreKeeper under **Account → Connections**. Revoking works at once.
- LoreKeeper never uses your lore for AI training. What the assistant reads becomes part of your chat with that app, so the app's own data settings apply.
- Privacy policy: https://www.lorekeeper.com/privacy-policy

## Support

- Email: support@lorekeeper.co.uk
- Guide and FAQ: https://www.lorekeeper.com/mcp

Not to be confused with the other projects called "LoreKeeper" or "lorekeeper-mcp": this connector is made by LoreKeeper Ltd and connects to your account at www.lorekeeper.com.
