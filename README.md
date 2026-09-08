# Deck agent plugins

Use [Deck](https://usedeck.ai) from your agent. Deck is a storytelling workspace: an infinite canvas of
artifacts (self-contained HTML documents on a 1920x1080 frame) that an agent can read and write
through Deck's hosted MCP server. Writes land on your open canvas live.

No API key. The server signs you in with your Deck account (OAuth): the first time an agent
connects, a browser tab opens on Deck, you click Allow, and that agent is connected for 30 days.

The server is `https://dev.usedeck.ai/api/v1/mcp`. Make your Deck account there first:
sign in at https://dev.usedeck.ai, then connect an agent.

## Claude.ai, Claude Desktop and Cowork

One connector serves all three, they share your claude.ai account.

1. claude.ai, Settings, Connectors, **Add custom connector**.
2. Name `deck`, URL `https://dev.usedeck.ai/api/v1/mcp`.
3. Authentication: **Always required**. OAuth client: **No client ID, register one automatically**.
   No headers. Add.
4. Press **Connect**. Deck opens, sign in if asked, press **Allow**.
5. In a chat, open the tools menu and switch `deck` on. In Cowork the connector is already listed.

## Claude Code

```sh
/plugin marketplace add Deck-HQ/agent-plugins
/plugin install deck@deck
```

Then `/mcp`, pick `deck`, **Authenticate**: Deck opens in the browser, press Allow. You get the `deck`
MCP server (58 tools) and six skills: `/deck` (orient and route), `/deck-story`, `/deck-artifact`,
`/deck-edit`, `/deck-images`, `/deck-brand-kit`.

## Cursor

Until Deck is listed on the Cursor Marketplace, install from this repo:

1. cursor.com/dashboard, **Plugins**, **Add Marketplace**, **Import from Repo**: `Deck-HQ/agent-plugins`.
2. In Cursor, **Customize** in the sidebar, find **deck**, **Install**, user scope.
3. Cursor Settings, **MCP**, `deck`, **Login**. Deck opens, press Allow.

No dashboard access? Add the server and the skills by hand: put
`{"mcpServers":{"deck":{"url":"https://dev.usedeck.ai/api/v1/mcp"}}}` in `~/.cursor/mcp.json` and copy
`plugins/deck/skills/*` into `~/.cursor/skills/`. Same result: the `deck` server plus `/deck`,
`/deck-story`, `/deck-artifact`, `/deck-edit`, `/deck-images`, `/deck-brand-kit`.

## Codex

```sh
codex plugin marketplace add Deck-HQ/agent-plugins
codex plugin add deck@deck
codex mcp login deck
```

The last line opens Deck in your browser, press Allow. In Codex, `$deck` (or `/skills`) starts the
skill; the Codex app opens the deck in its browser beside the chat while it works. Later:
`codex plugin marketplace upgrade` picks up new versions.

## Point at a different Deck

For a local backend add the server yourself with an API key (Deck, Account, API key):
`claude mcp add --transport http deck-local http://localhost:8080/v1/mcp --header "Authorization: Bearer dk_..."`.

## Layout

Same shape as [paper-design/agent-plugins](https://github.com/paper-design/agent-plugins): one
marketplace manifest per harness at the root, one plugin folder with a manifest per harness and its
MCP config, and the skills inside the plugin.
