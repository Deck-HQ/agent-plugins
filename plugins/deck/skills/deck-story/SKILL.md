---
name: deck-story
description: Shape the story of a Deck before any artifact is written. Use for "make me a deck about X", "what should the sections be", "plan the deck", "who is this for", or when a request would produce more than two artifacts. Produces the goal, the audience, the section list with one idea each, and the composition per section.
allowed-tools: mcp__deck__get_deck, mcp__deck__get_guide, mcp__deck__plan_deck_compositions, mcp__deck__plan_artifact, mcp__deck__list_documents, mcp__deck__get_document, mcp__deck__create_document, mcp__deck__write_document
---

# The story first

A deck that reads well was decided before it was written. Do this before deck-artifact touches a frame.

## 1. The goal, in four lines

Write it down (a document named "Goal" via `create_document`, or in the chat when the user prefers):

- **Subject**: what the deck is about, in the user's own words.
- **Audience**: who is in the room and what they already believe. This changes how hard every claim
  lands. If the user has not said, ask this one question and nothing else.
- **Outcome**: what the audience should think, feel or do afterwards. One sentence.
- **Proof**: the facts, numbers, decisions and context the user gave. Real names and real numbers,
  never a placeholder like "[your metric]". If the user shared material (Linear, Figma, files,
  pictures), pull the specifics out of it here.

Never re-ask something the user already answered or declined.

## 2. Sections, one idea each

Six to nine artifacts for a normal deck. Each section is ONE idea stated as a sentence a reader could
disagree with ("Retention held at 118% through the price change"), never a topic label ("Retention").
Order them so each one earns the next: the tension first, the proof in the middle, the ask last.

A cover is the first artifact and states the outcome, not the subject.

## 3. The shape of each section

Call `plan_deck_compositions` with the section list. It returns one composition family per section
chosen for what that section has to say; read `get_guide` topic `compositions` once so you know
the nine (split, spectrum, field, orbit, ledger, single-number, stack, grid, full-bleed) and
`roles` for what belongs on each kind of artifact. Two adjacent sections should not share a family
unless they are genuinely the same kind of thing.

## 4. Hand over

For each section, deck-artifact gets: the idea sentence, the proof lines that belong to it, the role,
the family, and the audience line. `plan_artifact` gives the writer the one idea, the signature visual
device and the vertical budget for a single artifact when it needs a second opinion.

## What to refuse

- A deck with no audience: ask, once.
- More than twelve sections: say so and propose which to merge.
- Invented numbers: leave the slot honest ("no figure yet") and tell the user.
