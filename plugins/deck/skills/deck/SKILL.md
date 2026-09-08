---
name: deck
description: Build, edit and restyle Deck presentations from this session through Deck's hosted MCP server. Use for "make me a deck about X", "add an artifact", "put this image in artifact 2", "change the title", "apply my brand kit", "why is it clipped", or any work on a usedeck.ai deck. Every write lands on the user's open canvas live.
allowed-tools: mcp__deck__list_decks, mcp__deck__create_deck, mcp__deck__get_deck, mcp__deck__get_guide, mcp__deck__get_design_system, mcp__deck__get_brand_kit, mcp__deck__list_brand_kits, mcp__deck__get_deck_theme, mcp__deck__set_deck_theme, mcp__deck__plan_deck_compositions, mcp__deck__plan_artifact, mcp__deck__begin_work, mcp__deck__end_work, mcp__deck__list_artifacts, mcp__deck__get_artifact, mcp__deck__get_artifact_text, mcp__deck__get_artifact_bake, mcp__deck__create_artifact, mcp__deck__write_artifact, mcp__deck__append_artifact, mcp__deck__validate_artifact, mcp__deck__read_artifact, mcp__deck__edit_artifact, mcp__deck__look_at_artifact, mcp__deck__set_artifact_text, mcp__deck__undo_artifact, mcp__deck__duplicate_artifact, mcp__deck__delete_artifacts, mcp__deck__reorder_items, mcp__deck__set_artifact_role, mcp__deck__set_artifact_presentation, mcp__deck__apply_theme_tokens, mcp__deck__list_images, mcp__deck__add_image, mcp__deck__place_image, mcp__deck__remove_image, mcp__deck__list_documents, mcp__deck__get_document, mcp__deck__create_document, mcp__deck__write_document, mcp__deck__bind_kit_to_deck, mcp__deck__get_composition
---

# Deck

A deck is an infinite canvas of **artifacts**. An artifact is one complete, self-contained HTML
document on a 1920x1080 frame. You write the document; Deck validates it, bakes it in the user's
browser, and the canvas updates in about 150 ms. You never need the in-app agent.

## First run

The `deck` MCP server needs the user's Deck API key in the `DECK_API_KEY` environment variable
(Deck, Account, API key). If a call answers "needs a Deck API key", say so and stop: never guess a
key and never ask the user to paste it into the chat.

## Order of work, every time

1. **Orient.** `list_decks` to find the deck, `create_deck` when there is none. `get_deck` before
   touching a deck: it says what exists, the theme, the kit.
2. **Read the contract once per session.** `get_guide` with topic `artifact-contract`. Every document
   you write is held to it; a document that breaks it is refused, not fixed.
3. **Read the style.** `get_brand_kit` when the deck is bound to a kit, otherwise `get_design_system`.
   The deck's style beats your taste.
4. **Plan the shape** for a whole deck with `plan_deck_compositions`; one artifact with `plan_artifact`.
5. **Batch.** `begin_work` before a run of writes, `end_work` after, so the canvas shows progress.
6. **Write one artifact per call** with `write_artifact` (or `create_artifact` with html), quoting the
   `expectedRev` you read. A conflict means someone wrote first: read again, then write again.
7. **Validate** with `validate_artifact` and fix every reject before moving on.
8. **Look.** `get_artifact_bake` is what actually settled on the canvas. Fix what clipped or overlapped.
9. `end_work`.

## Changing an artifact that exists

Never rewrite a document to change a part of it. Read, edit, look:

- `read_artifact` gives the html, the rev, and the picture library (id, url, memory line).
- `edit_artifact` takes exact search-and-replace edits copied verbatim from the read, several per
  call, all or nothing, rev-checked, undoable. Text, layout, colours and pictures all go through it.
  The result carries the look: each picture's measured frame once the user's tab has baked the new
  document. A clipped result is fixed with another edit before you answer.
- `look_at_artifact` when you want to check without changing anything.
- `set_artifact_text` for a pure wording change; `undo_artifact` reverts the last write.

## Pictures

The user's uploads sit in the deck's library with a memory line ("woman in red coat, city street").
A picture goes INTO the document as `<img data-deck-image="<id>" src="<url>" alt="<memory>">`
wherever the layout wants it: a tile, a column, a figure. Never invent a picture, a stock photo or
a placeholder box. `list_images` finds one by description; `add_image` takes a direct image link
(not a page); `place_image` and `remove_image` are the quick slot edits (middle, left, right, top,
bottom, under-the-title, full-bleed, half-left, half-right, grid).

## Brand kits

`list_brand_kits`, `get_brand_kit` for the palette, fonts, tone and the compositions a role earned
(`get_composition`). `bind_kit_to_deck` makes a kit the style of a deck; `apply_theme_tokens` reskins
every artifact's `--a-*` tokens in one pass.

## Rules

- Read only what you need: `get_artifact_text` is the cheap read, `get_artifact` the full one.
- Announce the plan before the first write, one line per artifact touched, one summary at the end.
  Never say "done" without a validated, baked result.
- Say no in the user's words: what is wrong and what to do instead, never "invalid".
