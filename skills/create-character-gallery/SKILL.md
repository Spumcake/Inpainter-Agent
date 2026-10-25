---
name: create-character-gallery
description: Make a themed gallery of an existing character - a set of images on one theme, such as a day at the beach or scenes from a story - from the character's reference sheets with an image-edit model, first having create-character-reference make a sheet for any new outfit, prop, or recurring object the theme needs. Use when the owner asks for a gallery, set, or series of images of a character who already has a reference. Not for building a character's reference or dataset.
---

# Character gallery

A gallery starts from a character that already exists, and a theme. The character's look comes from its reference: its sheets, and its brief when there is one, in the folder the caller names. If the character has no reference yet, use **create-character-reference** first.

Every image comes from an image-edit model that takes the reference sheets as input. Never build a gallery with a text-to-image model: it cannot hold the character from sheets.

## Find the specifics

The **execution skill** that implements `create-character-gallery` in this setup says:

- which image-edit model runs;
- how to send a request with its references;
- what it costs.

It comes from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

The caller gives an artifact folder, for prompts and images saved flat, and a work folder, for everything else. Each step waits for the owner's yes, and every paid request waits for a yes to its plan.

Every image of a character who reads as a minor stays ordinary and everyday. Nothing is sexual or suggestive, in any image, theme, or prompt.

## 1. Plan

Write `gallery.md` in the work folder: the theme in a sentence or two, then one row per image.

| id | scene | outfit | props and objects | expression | background | aspect |
|---|---|---|---|---|---|---|

Each id is short, lowercase, and hyphenated. Show the plan; the owner's corrections win.

## 2. New reference

List everything the plan needs that the reference does not show:

- a new outfit;
- a new prop;
- a recurring object that must look the same in more than one image.

For each one, have **create-character-reference** make that one sheet from the base sheet, and show it to the owner. The gallery waits until its new sheets are approved. The new sheets belong to the gallery, and are handed back with it; they are not added to the character's own reference.

Something that appears once, and need not match anything, can stay in the prompt alone.

## 3. Prompts

Write one prompt per row, based on the Entry prompt in create-character-reference's [dataset template](../create-character-reference/templates/dataset.md), with the row's scene and the theme. Keep the one-character line unless the owner's plan puts other people in the scene.

Attach, in this order:

1. the base sheet;
2. the row's outfit sheet, when it is not the default;
3. a sheet for each prop or object in the row.

## 4. Generate

Generate a few rows first, and compare them with the sheets before asking to run the rest. Inspect every image for drift from the reference, wrong colours, and broken anatomy, and report honestly. A new version is a new paid request, and needs the owner's yes.

When the gallery is flat digital art, say a cleanup may help.

## 5. The owner's choice

Show the owner the gallery, and any cleaned-up versions, and point them to the full-size files. The owner chooses which images to keep and which version of each; never choose yourself. Hand the kept images and the gallery's new sheets back to the caller.
