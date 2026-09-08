---
name: deck-brand-kit
description: Brand kits in Deck: read a company's site into a kit, set the palette, fonts, tone and rules, keep the compositions each role earned, bind a kit to a deck and retheme what exists. Use for "make a kit from acme.com", "use our brand", "the first line is never a question, remember that", "apply the kit to this deck", "no gradient meshes ever".
allowed-tools: mcp__deck__list_brand_kits, mcp__deck__get_brand_kit, mcp__deck__create_brand_kit, mcp__deck__update_brand_kit, mcp__deck__read_site_into_kit, mcp__deck__set_kit_logo_from_url, mcp__deck__add_kit_rule, mcp__deck__remove_kit_rule, mcp__deck__add_kit_avoid, mcp__deck__set_default_kit, mcp__deck__bind_kit_to_deck, mcp__deck__unbind_kit_from_deck, mcp__deck__get_composition, mcp__deck__apply_theme_tokens, mcp__deck__get_deck, mcp__deck__list_artifacts
---

# Brand kits

A kit is the identity every artifact in a deck wears: palette with colour roles, the two fonts and
the type scale, tone of voice, a guideline, the logo, standing rules, things to avoid, and one
approved composition per artifact role. The kit is a hard constraint; the layout is chosen per
artifact from the nine families. Never trade one for the other.

## Make one from the brand's own site

1. `create_brand_kit`, then `read_site_into_kit` with the brand's site. It reads the real CSS:
   the palette, the colour roles, the font families as declared, the type scale as ratios. Measured,
   not guessed; do not "improve" a colour you did not see.
2. `set_kit_logo_from_url` stores our own copy of the mark; never keep a hotlink.
3. `get_brand_kit` and read it back to the user in three lines: the palette, the fonts, the tone.
   Ask for a correction only where the read was uncertain.

## Rules and avoids

- `add_kit_rule` for an instruction the brand should keep obeying ("the first line is never a
   question", "numbers always carry a unit"). Rules written from a deck are proposed and confirmed
   with the user, never silent.
- `add_kit_avoid` for what the brand never wants ("gradient meshes", "stock photos of handshakes").
- `remove_kit_rule` by id; `get_brand_kit` lists ids.

## Compositions

`get_composition` returns the complete document the kit uses for one artifact role, plus the rules
that role earned. When writing an artifact of that role, build on it; when the user approves a new
one, it becomes the reference. Roles are the third axis: the kit says what it looks like, the family
how it is arranged, the role what belongs on it.

## Apply

- `bind_kit_to_deck` makes the kit the deck's style for everything generated afterwards.
- `apply_theme_tokens` reskins every existing artifact's `--a-*` tokens in one pass; each rev goes
  up by one and the bakes refresh. Tell the user before doing it across a deck.
- `set_default_kit` is the fallback for decks that name none.
- `delete_brand_kit` is irreversible; confirm in the user's words first.
