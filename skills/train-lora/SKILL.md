---
name: train-lora
description: Train a character LoRA from its captioned dataset with the model family's training recipe - plan it with its cost, train on the owner's yes, and publish the kept version as <family>_<character>_v<N> with its licence and a README that says how to prompt the character. Use after the dataset is captioned, such as "train Mira's LoRA". Not for captioning, making images to train on, or testing.
---

# Train a LoRA

## Find the specifics

- **The workflow skill** of the family the LoRA is for gives:
  - its training recipe: the trainer, the base model, and the settings;
  - its licence and use rule.

  If the family has no recipe, say so and stop.
- **The execution skill** that implements `train-lora` in this setup says where training runs, how it is planned, started, watched, and stopped, and how the LoRA is published.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## What it needs

The character's folder, which the caller names, must hold:

- `dataset/`, with images and captions that start with the trigger word, from the **caption-lora-dataset** skill;
- `ref/brief.md`, with the trigger word.

## 1. Plan

Show the owner the plan, and spend nothing before their yes to it:

- the dataset and its count;
- the settings and the steps;
- what is written where;
- the hardware and its price;
- the estimated time and cost.

## 2. Train

After the yes, start training with the execution skill. Training takes a while, so:

- run it so that this session ending cannot stop or orphan it;
- say what is running and how long it should take;
- report progress.

When it ends, report:

- the state;
- the minutes and the cost;
- where each epoch's file is.

If anything that bills is still running, stop it and say so.

A new run needs a new run name. The run name only keeps runs apart; it is not the LoRA's version.

## 3. Publish

A character's LoRA is named `<family>_<character>_v<N>`, the same everywhere. `<N>` counts the versions the owner has kept, so a character's first is `v1`. Use the last epoch unless the owner names another.

On the owner's word:

1. Put the LoRA where this setup's servers read it, and check its size against the original.
2. Add it to the character's folder, using large-file storage when that folder is a repository, together with:
   - the family's licence text and use rule, which go with it everywhere;
   - a README on how to prompt the character: the trigger word, the fixed traits, then words from the captions for the outfit, pose, and setting wanted, since the captions are what the LoRA learned to answer. Then a note on how it was trained.

Epoch files and training data are removed only on the owner's yes. Testing is the **test-lora** skill.
