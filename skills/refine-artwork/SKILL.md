---
name: refine-artwork
description: Redraw a set of artwork images lightly with a model family's refine look through image-to-image at a chosen strength, into a new set beside the originals. Use only when the owner asks for a refine, redraw, or a named model's pass by name. Not for cleanup - a request to clean up or denoise flat digital art is the clean-artwork skill - and not for keeping a character on model.
---

# Refine artwork

Refining redraws each image lightly in a model's look. It gives a smoother finish, but it redraws: colours, faces, and small details move. Say this plainly before offering it for anything where a character must stay on model. Never use it as cleanup; that is the **clean-artwork** skill. The originals are never changed.

## Find the specifics

- **The workflow skill** of the family names its refine looks, the default strength, and what drift it has shown.
- **The execution skill** that implements `refine-artwork` in this setup says how to list the images with their text, check, and run the set.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

The caller gives:

- the images;
- a work folder, for the image list and the set's record;
- an output folder.

## 1. The image list

Each image needs the text that describes it, in the family's prompting style. For a character, write the fixed traits into every image's text, then what that image shows: framing, view, pose, outfit, expression, and background. A redraw without the fixed traits drifts further.

Give each image an id that names the set, because an output never overwrites an existing file.

## 2. Plan

Check the set without sending anything. Show the owner:

- the number of images;
- the look and the strength;
- the server;
- the estimate.

A lower strength keeps more of the original, and a higher one redraws more. Send nothing before the owner's yes.

## 3. Run and choose

After the yes, run the set. Show the originals and the redraws side by side, and point the owner to the full-size files. Report honestly what moved: colours, faces, and details lost or invented. The owner chooses what to keep; never choose for them.
