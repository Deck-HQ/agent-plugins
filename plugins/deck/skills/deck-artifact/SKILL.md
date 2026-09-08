---
name: deck-artifact
description: Write one artifact for a Deck, a complete self-contained HTML document on a 1920x1080 frame that passes Deck's contract, bakes without clipping, and says one thing well. Use for "write artifact N", "add a cover", "make a metrics artifact", "rewrite this one from scratch", or when deck-story has handed over a section.
allowed-tools: mcp__deck__get_guide, mcp__deck__get_deck, mcp__deck__get_design_system, mcp__deck__get_brand_kit, mcp__deck__get_composition, mcp__deck__plan_artifact, mcp__deck__begin_work, mcp__deck__end_work, mcp__deck__create_artifact, mcp__deck__write_artifact, mcp__deck__append_artifact, mcp__deck__validate_artifact, mcp__deck__get_artifact_bake, mcp__deck__look_at_artifact, mcp__deck__get_artifact, mcp__deck__set_artifact_role, mcp__deck__undo_artifact, mcp__deck__list_images
---

# Writing an artifact

## Before the first line

1. `get_guide` topic `artifact-contract`, once per session. It is the law: the output shape, the
   1920x1080 canvas, the manifest, the `--a-*` token block, the vertical budget arithmetic, the type
   scale, motion restraint, the settle law. Everything below assumes you have read it.
2. The style: `get_brand_kit` (bound kit) or `get_design_system`. Palette, the two fonts, the tone.
   When the kit has an approved composition for this role, `get_composition` gives you the document
   that role earned; build on its bones, not on your habit.
3. The brief from deck-story, or, for a single ask, `plan_artifact`: the one idea, the signature
   visual device, the family, the role.

## The craft, in order of what makes the difference

**One idea.** The headline is a sentence with a verb that the audience could disagree with. If a
second idea wants in, it is the next artifact.

**Show the budget.** Before writing, add the heights: title, gap, body, gap, footer, against 1080
minus the margins. If it does not fit, split into two artifacts or cut words. Never shrink type to
make it fit; the contract's type scale is fixed.

**Words are measured.** A headline is one line at display size, about eight words. A body block is
three to five lines. A card carries a label of two or three words and one line under it. A stat is
a number, a unit and a four-word caption. These are measured against the frame, so treat them as
caps, not suggestions.

**Choose the structure for what the content IS.** Two things in tension: split. An ordered range:
spectrum. One figure that is the argument: single-number. Peers read the same way: grid. Rows that
share columns: ledger. One centre with satellites: orbit. Many small things whose spread is the
point: field. One claim developing downward: stack. A picture or colour carrying the feeling with
few words: full-bleed. Do not reach for three cards under an eyebrow out of habit; the contract bans
the eyebrow device.

**Real pictures only.** The user's library pictures go in as
`<img data-deck-image="<id>" src="<url>" alt="<memory>">` (ids and URLs from `list_images` or the
brief). A logo is a real company mark by domain. Never a stock photo, never a grey placeholder, never
a drawn logo.

**Copy voice.** Short, plain sentences. No em dashes, no slogans, no stacked three-word fragments,
no decorative bullet dots. Quote the user's numbers exactly.

**One aesthetic.** The kit's tokens on `:root`, nothing hard-coded, the same two fonts, motion only
where the contract allows it and settled before the bake.

## Write, then look

- `begin_work`, then ONE complete document per `write_artifact` (or `create_artifact` with html),
  quoting the `expectedRev` you read. A conflict means someone wrote first: read again, write again.
- `validate_artifact`. Fix every reject before anything else; treat flags as advice.
- `get_artifact_bake` or `look_at_artifact` after the browser settles it: the measured result. A
  clipped or overlapping element is fixed before you answer. Never claim "fits" without the bake.
- `set_artifact_role` when the role is known; it steers the kit's compositions next time.
- `end_work`.

For a long document, `append_artifact` streams it onto the canvas piece by piece; the user watches it
arrive. The last piece carries `done`.
