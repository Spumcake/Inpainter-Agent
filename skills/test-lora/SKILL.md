---
name: test-lora
description: Test a character LoRA for breadth - what it was trained on and what it was not, across every look of its family the server has - with one image per idea on fixed seeds, controls without the LoRA, and labelled sheets by what each tests. Use when the owner asks to test a character's LoRA, such as "test Mira's LoRA". Not for training, captioning, or comparing epochs and strengths.
---

# Test a LoRA

A test spends every image on something new: what the LoRA was trained on, things it was not, and every look on the server. The point is whether the character comes out recognizably as designed. How a checkpoint or a style draws it is up to the model.

A character LoRA is not a style. It always runs at full strength, and its strength is never a variable. Neither are epochs. The owner judges; never pick or score.

## Find the specifics

- **The workflow skill** of the LoRA's family gives:
  - its base models to cover, the slots that make a look's base, and the slots a look has for stacked LoRAs;
  - the LoRAs refused with a character, and its short names.
- **The setup** gives where the character LoRA and the style LoRAs are kept, and the prices.
- **The execution skill** that implements `test-lora` in this setup says how to write and check the plan, render it, and make the sheets. When the family's captions are tags, the helper skill of the repository the workflow names under `captions.groups` sorts the trained concepts.

All come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## What it needs

The character's folder holds:

- `dataset/`, the images and captions the LoRA was trained on;
- `ref/brief.md`, the trigger word and the fixed traits;
- the LoRA itself.

The server must have the same LoRA under the same name. If anything is missing, say which and stop. Upload the folder's copy only on the owner's yes. Test files are work files, in a folder the caller gives.

## 1. What was trained

Group every caption word, with how many images use it:

- expressions;
- poses and gestures;
- views and framings;
- settings;
- the rest, usually outfit pieces and props.

The trigger and the fixed traits are left out: they are in every prompt, not concepts to test.

## 2. The plan

**Looks:**

- every base model of the family on the server, alone, each in a look of its own;
- stacks that together use every style LoRA on the server, up to the family's slots, each starting at 0.7.

Never stack a style on its own base model, and never use a LoRA the family refuses with a character. A model left out is listed with the reason, for the owner to see. Read every model's card first, and leave out a LoRA whose card shows it is another character rather than a style.

**Prompts:**

- A **trained** prompt combines one expression, one pose, one view, and an outfit or prop, in the captions' own words, in a setting the dataset did not use.
- A **new** prompt tries an outfit, setting, or action the captions never had.
- Write each prompt the way the character is prompted for real: the fixed traits first, then caption words. The look adds the trigger.
- Name only what the framing shows: a portrait leaves out the shoes, or the framing goes wider.
- Trained prompts go in three looks and new ones in two. No prompt repeats a look, and every look is used at least three times.

**Controls:** two or three prompts rendered without the LoRA, in a look where they also appear with it.

**Untested words:** only mouth and brow states, background objects, and tagger variants, each with its reason.

**The check.** Run the execution skill's plan check until it passes. Never drop a look to make it pass. Show the owner what it printed, the image count, and the cost, and wait for their yes.

## 3. Render

Render detached from the session, on the plan's fixed seeds, so it can resume. Then check every record:

- every LoRA image's text holds the trigger and every fixed trait;
- no control holds the trigger;
- every image has its planned seed.

## 4. Sheets

Make one sheet per group (expressions, poses and views, outfits and props, new concepts), and one sheet per look with its control beside it. Label every image with its look.

Report what holds and what breaks, group by group, identity first: hair, eyes, outfit, proportions. Examples are an expression ignored, a colour lost in one look, or a style overpowering the character. Point the owner to the full-size images, and never choose for them.

What holds becomes how to use the character. Offer to add the working prompts to the character folder's README.
