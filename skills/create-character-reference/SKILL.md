---
name: create-character-reference
description: Build a character's full reference - a brief, reference sheets (base turnaround, one per outfit, one per detailed prop or recurring object), and the reference gallery a training set is chosen from - with an image-edit model, then hand the owner the images to choose from. Use when the owner asks to design or make a character, an outfit or prop sheet, or a character's reference gallery or dataset images; and from create-character-gallery for a new outfit, prop, or object a gallery needs. Not for cleaning, captioning, or training.
---

# Character reference

A character's reference is everything that fixes what it looks like: its brief, its reference sheets, and its reference gallery. This skill makes them and stops at the owner's choice. It hands the kept images and the brief back to the caller.

## The model

Every image here comes from an **image-edit model**: one that takes the reference sheets as input images and keeps them. Never use a text-to-image model, even with a look or a LoRA. It cannot hold a character from sheets, so the reference would not stay consistent.

## Find the specifics

The **execution skill** that implements `create-character-reference` in this setup says:

- which image-edit model runs;
- how a request is sent with its reference images;
- what it costs;
- where its output lands.

When that model has a workflow skill, read it for how to prompt it. Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

The caller gives:

- the owner's request and input images;
- an artifact folder, for prompts and images, each saved flat beside its prompt;
- a work folder, for everything else: the brief, the dataset plan, and the model's records.

Each step waits for the owner's yes before the next. Every paid request waits for a yes to its plan: the number of requests and an estimate.

Every image of a character who reads as a minor stays ordinary and everyday. Nothing is ever sexual or suggestive, in any step, prompt, or caption.

## 1. Brief

Fill [the brief template](templates/character-brief.md) from the owner's request and input images, and name the input images it is drawn from. The brief includes:

- a **Trigger word**;
- **Fixed tags**, in the prompting style of the family the LoRA will be for.

Show the brief to the owner; their corrections win.

## 2. Reference sheets

Each sheet is a separate 3:2 page with a header and one job, so no sheet is crowded.

- **Base sheet:** the character in the default outfit, as a four-view turnaround: front, three-quarter, side, and back.
  - Fill [the base template](templates/reference-base.md), and send it with the input images as references.
  - If the owner supplies a base sheet, use theirs.
- **Outfit sheet,** one per other outfit: the same turnaround and layout, with only the outfit changed.
  - Fill [the outfit template](templates/reference-outfit.md).
  - Send it with the base sheet first, and the input image that shows the outfit second.
- **Prop sheet,** for a prop or recurring object that needs detail to stay consistent: views of the object alone, labelled close-ups, and one small in-use panel for scale.
  - Fill [the prop template](templates/reference-prop.md).
  - Send it with the input images that show the prop, and the base sheet.

Expressions, head angles, poses, and gestures belong in the gallery, not on a sheet.

Make one sheet per request. Inspect each for drift from the base sheet, wrong colours, and broken anatomy, and report honestly. A new version is a new paid request, and needs the owner's yes.

When **create-character-gallery** asks for a sheet a new gallery needs, make only that sheet, from the existing base sheet.

## 3. Reference gallery

Fill [the dataset template](templates/dataset.md): a matrix of framings, views, outfits, expressions, props, and backgrounds. Then write one prompt per row.

Send each row with:

- the base sheet first;
- the row's outfit sheet, when the outfit is not the default;
- the prop sheet, when the row has that prop.

Run a few rows first, and compare them with the sheets and the input images before asking to run the rest.

Image-edit models leave grain in flat digital art. Say so when the gallery is done, so the caller can have it cleaned with **clean-artwork** before the owner chooses. Never offer a redraw by a text-to-image model: one took a character's gallery off model.

## 4. The owner's choice

Show the owner the gallery, and any cleaned-up versions beside it, and point them to the full-size files. The owner chooses which images to keep and which version of each; never choose yourself. Record each choice in the dataset plan's Kept images section.

Hand back to the caller:

- the kept images, each named by its row id;
- the brief;
- the top sheets: base, each outfit, and each prop.
