---
name: clean-artwork
description: Clean up flat digital artwork - remove an image model's grain and compression noise while keeping every line and colour exactly where it was - into a new set beside the originals. Use whenever the owner asks to clean up, denoise, or de-grain images that are, or will come out as, flat digital art (anime, cel-shaded, flat-colour illustration), such as a character's gallery. Cleanup always means this, never a redraw. It applies when the images themselves are cleaned ("clean up this image"), not when a folder of files is tidied. Not for photographs, realistic, or painterly images.
---

# Clean up artwork

Cleaning up artwork means denoising it. It removes grain and compression noise, and keeps the drawing exact, so a character stays on model. It is never a redraw; a redraw is the **refine-artwork** skill, which runs only when the owner asks for one by name.

Tell the request apart by what is being cleaned. "Clean up this image" or "clean up the gallery" means the pictures, and is this skill. Tidying a folder of files is not. When it is unclear, ask.

## Find the specifics

- **The workflow skill** of the cleanup method gives its graph, its look, and what it was measured to do.
- **The execution skill** that implements `clean-artwork` in this setup says how to list the images, check, and run the set.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## What it needs from the caller

- the images to clean;
- a work folder, for the image list and the set's record;
- an output folder, for the cleaned images.

The originals are never changed.

## 1. Plan

List the images. Give each an id that says it is denoised, because an output never overwrites an existing file. Check the set without sending anything.

Show the owner:

- the number of images;
- the server;
- the estimate, from the setup's prices.

Send nothing before their yes.

## 2. Run

After the yes, run the set. A failed image is recorded, and the rest still run. A second try gets new ids.

## 3. The choice

Show the originals and the cleanups side by side, and point the owner to the full-size files, since grain barely shows in a small contact sheet. Report honestly what changed.

For each image, the owner names one of:

- the original;
- the cleanup;
- dropped.

Hand that choice back to the caller.

## Naming

A denoised image says so in its name wherever it goes, so it is never mistaken for its original. Beside its original it is `<original name>_denoised.<ext>`. A folder whose images are all denoised, such as a training set whose file names must match their captions, may leave the word out when its README says so.
