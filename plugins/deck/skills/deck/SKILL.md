---
name: deck
description: Work on a Deck presentation from this session through Deck's hosted MCP server. Start here for "make me a deck about X", "add an artifact", "change artifact 2", "put this picture in", "apply my brand kit", or any usedeck.ai ask; it orients, opens the deck in the browser pane beside the chat, then hands the craft to deck-story, deck-artifact, deck-edit, deck-images and deck-brand-kit.
allowed-tools: mcp__deck__list_decks, mcp__deck__create_deck, mcp__deck__get_deck, mcp__deck__get_guide, mcp__deck__get_design_system, mcp__deck__get_brand_kit, mcp__deck__list_brand_kits, mcp__deck__get_deck_theme, mcp__deck__list_artifacts, mcp__deck__get_artifact_text, mcp__deck__begin_work, mcp__deck__end_work, mcp__deck__reorder_items, mcp__deck__set_artifact_presentation, mcp__deck__duplicate_artifact, mcp__deck__delete_artifacts, mcp__deck__list_documents, mcp__deck__get_document, mcp__deck__create_document, mcp__deck__write_document, mcp__Claude_Browser__navigate, mcp__Claude_Browser__preview_start, mcp__Claude_Browser__read_page, mcp__Claude_Browser__get_page_text, mcp__Claude_Browser__computer
---

# Deck

A deck is an infinite canvas of **artifacts**: complete, self-contained HTML documents on a 1920x1080
frame. Deck validates what you write, bakes it in the user's browser, and the canvas updates in about
150 ms. You are the agent; the in-app one is not needed.

## First run

The `deck` MCP server signs you in with the user's Deck account (OAuth). If a call answers that the
server needs authentication, tell the user to run `/mcp`, pick `deck`, Authenticate, and stop until
they say it is done. Never ask for a key or a password in the chat.

## Orient, every time

1. `list_decks` finds the deck; `create_deck` when there is none.
2. `get_deck` before touching a deck: what exists, the theme, the kit. `list_artifacts` for the order
   and titles; `get_artifact_text` is the cheap read of one.
3. `get_guide` topic `artifact-contract` once per session before you write anything. It is the live
   contract, never a copy.
4. The style: `get_brand_kit` when the deck is bound to a kit, else `get_design_system`. The deck's
   style beats your taste.

## Open the canvas beside the chat

Every deck result carries `deckUrl`, the workspace's full address. The user should watch the deck
fill in while you work, so:

1. The moment you know which deck you are on (after `create_deck`, `get_deck` or `list_decks`), and
   before the first write, open `deckUrl` in the host's browser pane when it has one: Claude Code
   desktop (`navigate` or `preview_start` with the url), Cowork (its browser). One tab per deck for
   the whole session; navigate that tab, never open a second one for the same deck.
2. Read the page. If it shows Deck's sign-in instead of the workspace, the pane is not signed in yet.
   Say one line: "Sign in to Deck in the browser pane, I'll wait." Then wait: re-read the page every
   few seconds for up to two minutes until the workspace shows (the deck title, the directory, the
   composer). Do not write to the deck while the pane shows sign-in, and never type credentials or
   a code yourself. If two minutes pass, ask the user to tell you when they are in.
3. Keep the tab open. Writes land there live; you do not need to reload. After `end_work`, take one
   screenshot of the pane so the user sees what landed, and repeat `deckUrl` in the summary.

Hosts without a browser pane (claude.ai chat, the API): hand the user `deckUrl` in your first
message and again in the summary, so they open it beside the chat themselves.

## Then route

| The ask | Skill |
|---|---|
| a new deck, a story, "what should the sections be" | deck-story |
| write or rewrite one artifact | deck-artifact |
| change something on an artifact that exists (text, layout, colour, a picture) | deck-edit |
| pictures: library, place, remove, "the one with the woman in red" | deck-images |
| brand kit: read a site, palette, fonts, rules, compositions, bind to a deck | deck-brand-kit |

Documents (`create_document`, `write_document`) hold research and notes beside the artifacts; they are
markdown, not slides.

## Rules of the room

- `begin_work` before a run of writes, `end_work` after, so the canvas shows progress.
- Announce the plan before the first write, one line per artifact touched, one summary at the end.
  Never "done" without a validated, baked result.
- Say no in the user's words: what is wrong and what to do instead, never "invalid".
- Copy voice: short plain sentences, no em dashes, no slogans, no stacked three-word fragments.
