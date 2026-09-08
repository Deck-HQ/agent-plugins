---
name: deck-images
description: Pictures in a Deck: the library with its memory lines, adding from a link, placing inside an artifact, removing, replacing, grids, and what to say when a picture cannot be used. Use for "put this image in the middle", "the one with the woman in red goes on artifact 4", "add these six as a grid", "take the logo off", "why is my image not showing".
allowed-tools: mcp__deck__list_images, mcp__deck__add_image, mcp__deck__place_image, mcp__deck__remove_image, mcp__deck__read_artifact, mcp__deck__edit_artifact, mcp__deck__look_at_artifact, mcp__deck__get_artifact_bake
---

# Pictures

## The library and its memory

Every picture the user dropped into Deck sits in the deck's library with a memory line written once at
upload: "woman in red coat, city street, evening", plus width, height and kind (photo, logo,
screenshot, illustration). `list_images` returns them. That is how "the one with the woman in red"
resolves to an id: read the memory lines, pick, never ask the user to name a file. A picture with no
memory line (stored before memory existed) is named by its file name; say so, never invent what it
shows.

`add_image` takes a direct image link. A page link is refused: "That link is a web page, not an
image. Copy the image address instead."

## Where a picture goes

A picture belongs INSIDE the artifact's own layout, wherever the composition wants it: a tile in a
grid, the left half of a split, the figure under a headline. That is an edit (deck-edit): read the
document, insert `<img data-deck-image="<id>" src="<url>" alt="<memory line>">` into the element,
give it the width the layout gives its siblings, `object-fit: cover` for a tile and `contain` for a
logo or a screenshot that must not be cropped, and look at the measured frame.

`place_image` and `remove_image` are the quick door when there is no layout to respect: positions
`middle`, `left`, `right`, `top`, `bottom`, `under-the-title`, `full-bleed`, `half-left`,
`half-right`, and `grid` with several ids (or `all`) for a gallery. Sizes: smaller, bigger, 2x, fit,
fill, or a width in px. Styles: border, thin-border, rounded, rounded-N. Bleed: "right 50%" hangs
half the picture off that edge. Placing a picture that is already on the artifact moves it; there is
never a second copy unless the user asked for one.

## Rules

- Never invent a picture, a stock photo or a placeholder box. No picture means no picture: ask for one.
- Never crop a screenshot or a logo silently; contain it, or ask.
- "Take it off" removes from the artifact and keeps the file. Delete from the library only when the
  user says library or both.
- Limits: 10 MB a file, image types only; an SVG with a script is stripped and the user told; a huge
  PNG gets a compressed copy in the artifact and the original stays.
- After every placement, the measured frame: inside, or clipped by N px. Fix clipped before answering.

## What to say

- No picture attached, ask to place: "No image attached. Drop one in and tell me where it goes."
- Ten pictures, sixteen artifacts: "Tell me which artifacts, or say 'first 10'."
- Picture not showing: read the artifact; a picture with a remote src the contract rejects, or a
  missing id, is the usual cause. Fix the img, do not rewrite the document.
