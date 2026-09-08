# Deck agent plugins

Use [Deck](https://usedeck.ai) from your agent. Deck is a storytelling workspace: an infinite canvas of
artifacts (self-contained HTML documents on a 1920x1080 frame) that an agent can read and write
through Deck's hosted MCP server. Writes land on your open canvas live.

## Your API key

Every harness below needs your Deck API key in the `DECK_API_KEY` environment variable. Get it in
Deck under **Account, API key**, then:

```sh
export DECK_API_KEY=dk_...
```

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

## Point at a different Deck

`DECK_MCP_URL` overrides the server URL for Claude Code (staging: `https://dev.usedeck.ai/api/v1/mcp`).

## Layout

Same shape as [paper-design/agent-plugins](https://github.com/paper-design/agent-plugins): one
marketplace manifest per harness at the root, one plugin folder with a manifest per harness and its
MCP config, and the skill inside the plugin.
