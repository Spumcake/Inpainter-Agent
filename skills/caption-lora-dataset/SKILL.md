---
name: caption-lora-dataset
description: Caption a character's chosen images as a LoRA dataset - each caption written as the prompt that would make that image (the trigger word, the character's fixed traits, then everything else it shows), drafted by the model family's tagger when it has one, checked against every image, and written beside each image. Use after the owner has chosen a character's dataset images, such as "caption Mira's dataset". Not for making or choosing images, and not for training.
---

# Caption a LoRA dataset

## A caption is what you would write to make that image

Every caption is the prompt that should produce its image:

1. the trigger word;
2. the character's fixed traits;
3. everything else the image shows: outfit, expression, pose, view, setting, and background.

The LoRA learns to answer the words people will actually type. The captions then double as the character's prompting guide. To make the character later, write the trigger, the fixed traits, and caption words for the outfit, pose, and setting wanted.

Never leave a visible trait out so that the trigger word "absorbs" it, a common habit in LoRA guides. A LoRA captioned that way lost its character's hair colour under strong styles, because no prompt asked for it.

## Find the specifics

- **The workflow skill** of the family the LoRA is for says the caption style (tags or sentences), and which tagger drafts captions.
- **The tagger's helper skill,** from the repository the workflow names as its tagger, says how to draft and check them. When the family has no tagger, write each caption yourself, in its style.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## What it needs

The caller names the character's folder. It holds:

- `dataset/`, the chosen images, each at least 1024 pixels on its long side;
- `ref/brief.md`, the brief, with a **Trigger word** line and a **Fixed tags** line.

If there is no brief, or either line is missing, stop and ask the owner. Never invent a trigger word or fixed traits.

Every caption of a character who reads as a minor stays ordinary: no sexual, suggestive, or body-focused words, ever.

## 1. Draft

Draft every caption with the execution skill, into a work folder the caller gives. Raw tags, drafts, and notes are work files, never committed.

Decide each frequent word that is not a fixed trait, and write why in `edits.md`:

- identity belongs in the brief's fixed traits, which are the owner's to approve;
- something that varies, such as an outfit piece, stays in the caption.

## 2. Check every caption against its image

Look at each image beside its draft, and ask whether this caption, typed as a prompt, would make this image.

- Remove wrong words, including a fixed trait the image does not show, such as eye colour in a view from behind.
- Add clear misses, using only words the model knows.
- Make sure every caption names the background.
- Write each edit and its reason in `edits.md`, then write the final captions beside the images.
- Report drawing flaws you notice. Never fix an image.

## 3. Check

Run the execution skill's check, and fix every problem it prints. Confirm that each caption lacking a fixed trait really does not show it. The check is a safety net, not a substitute for looking at every caption.

## 4. The owner's review

Show the owner a few captions and the edits list, and say what you could not verify. Captions are committed only on the owner's word. Training is the **train-lora** skill.
