---
name: deck
description: Work on a Deck presentation from this session through Deck's hosted MCP server. Start here for "make me a deck about X", "add an artifact", "change artifact 2", "put this picture in", "apply my brand kit", or any usedeck.ai ask; it orients, then hands the craft to deck-story, deck-artifact, deck-edit, deck-images and deck-brand-kit.
allowed-tools: mcp__deck__list_decks, mcp__deck__create_deck, mcp__deck__get_deck, mcp__deck__get_guide, mcp__deck__get_design_system, mcp__deck__get_brand_kit, mcp__deck__list_brand_kits, mcp__deck__get_deck_theme, mcp__deck__list_artifacts, mcp__deck__get_artifact_text, mcp__deck__begin_work, mcp__deck__end_work, mcp__deck__reorder_items, mcp__deck__set_artifact_presentation, mcp__deck__duplicate_artifact, mcp__deck__delete_artifacts, mcp__deck__list_documents, mcp__deck__get_document, mcp__deck__create_document, mcp__deck__write_document
---

# Deck

A deck is an infinite canvas of **artifacts**: complete, self-contained HTML documents on a 1920x1080
frame. Deck validates what you write, bakes it in the user's browser, and the canvas updates in about
150 ms. You are the agent; the in-app one is not needed.

## First run

The `deck` MCP server needs the user's Deck API key in `DECK_API_KEY` (Deck, Account, API key). If a
call answers "needs a Deck API key", say so and stop. Never guess a key, never ask for it in the chat.

## Orient, every time

1. `list_decks` finds the deck; `create_deck` when there is none.
2. `get_deck` before touching a deck: what exists, the theme, the kit. `list_artifacts` for the order
   and titles; `get_artifact_text` is the cheap read of one.
3. `get_guide` topic `artifact-contract` once per session before you write anything. It is the live
   contract, never a copy.
4. The style: `get_brand_kit` when the deck is bound to a kit, else `get_design_system`. The deck's
   style beats your taste.

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
