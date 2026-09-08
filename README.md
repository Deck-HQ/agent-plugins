# Deck agent plugins

Use [Deck](https://usedeck.ai) from your agent. Deck is a storytelling workspace: an infinite canvas of
artifacts (self-contained HTML documents on a 1920x1080 frame) that an agent can read and write
through Deck's hosted MCP server. Writes land on your open canvas live.

## Your API key

Get it in Deck under **Account, API key**. Claude Code asks for it when you enable the plugin and keeps
it in your keychain; Cursor and Codex read it from the `DECK_API_KEY` environment variable.

## Claude Code

```sh
/plugin marketplace add Deck-HQ/agent-plugins
/plugin install deck@deck
```

You get the `deck` MCP server (58 tools) and six skills: `/deck` (orient and route), `/deck-story`, `/deck-artifact`, `/deck-edit`, `/deck-images`, `/deck-brand-kit`.

## Cursor

```sh
/add-plugin deck
```

(Marketplace listing pending; until then add the marketplace from this repo.)

## Codex

Point Codex at `plugins/deck/.codex-plugin/plugin.json`.

## Claude.ai and Cowork

Remote connectors there authenticate with OAuth, not an API key; Deck's OAuth login is on the way. Until
then the plugin works in Claude Code, Cursor and Codex.

## Point at a different Deck

The server is `https://usedeck.ai/api/v1/mcp`. For staging or a local backend, add the server yourself:
`claude mcp add --transport http deck-staging https://dev.usedeck.ai/api/v1/mcp --header "Authorization: Bearer dk_..."`.

## Layout

Same shape as [paper-design/agent-plugins](https://github.com/paper-design/agent-plugins): one
marketplace manifest per harness at the root, one plugin folder with a manifest per harness and its
MCP config, and the skill inside the plugin.
