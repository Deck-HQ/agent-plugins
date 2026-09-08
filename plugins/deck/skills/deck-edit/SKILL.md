---
name: deck-edit
description: Change an artifact that already exists on a Deck without rewriting it: text, layout, colours, spacing, order, pictures. Use for "make the title shorter", "move the chart left", "take the second one out of the grid", "don't crop those two images", "change $18 to $49", "make it bigger". Read, edit with exact search-and-replace, look at the measured result.
allowed-tools: mcp__deck__read_artifact, mcp__deck__edit_artifact, mcp__deck__look_at_artifact, mcp__deck__set_artifact_text, mcp__deck__undo_artifact, mcp__deck__get_artifact_bake, mcp__deck__validate_artifact, mcp__deck__begin_work, mcp__deck__end_work, mcp__deck__list_images
---

# Editing what exists

Never rewrite a document to change a part of it. Read, edit, look.

## Read

`read_artifact` returns the html, the rev, and the picture library (id, url, memory line). Read the
whole document once; the search strings below are copied from it, never retyped.

## Edit

`edit_artifact` takes exact search-and-replace edits, several per call, applied in order, all or
nothing, rev-checked, undoable.

- **Copy the search verbatim**, whitespace and all. Minimal but unique: one to eight lines, enough
  context that it matches exactly once. A search that matches twice or not at all fails the whole
  call and tells you which one.
- **Delete by replacing with nothing.** Removing an element means all of it: its markup and the
  styles that exist only for it, nothing else.
- **Change only what the ask names.** Nothing the user did not name moves. Carry the user's protect
  words verbatim in your note: "keep", "don't touch", "leave the right part as it is".
- **Resize is not scale.** "Smaller" means a smaller box with the same internal proportions and
  refitted content; "scale" means the whole thing shrinks. Use the user's word.
- **Style asks move only style.** "Swap the violet to pink", "calm the colours down": token values
  and colour rules change, markup and layout stay.
- **Pictures** go in as `<img data-deck-image="<id>" src="<url>" alt="<memory>">` into the element
  the layout wants (a tile, a column, a figure), or out by removing that img. Stacking, reordering
  and spacing are CSS edits on the container. Never a placeholder, never an invented picture.
- Absolute pixel sizes, exactly as the document already does. The kit's tokens own every colour.
- Ten or more edits, or a change to most of the document, is a rewrite: hand it to deck-artifact.

`set_artifact_text` is the shortcut for pure wording (find and replace on the text layer only).
`undo_artifact` reverts the last write when the user says "no, put it back".

## Look

The edit result carries the look: the contract check and, once the user's tab has baked the new
document, each picture's measured frame ("inside the frame" or "clipped by 212 px on the right"
with its box). A red look is fixed with another edit before you answer. When nothing is measured
yet ("no open tab has settled it"), say that instead of claiming it fits. `look_at_artifact` checks
without changing anything.

## Say it plainly

One line per edit in your answer ("Took the second picture out of the grid, five remain"). Never
"done" over a red look.
