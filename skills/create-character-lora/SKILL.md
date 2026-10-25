---
name: create-character-lora
description: Make a tested character LoRA from one or a few images of a character, start to finish - reference sheets and a gallery, cleanup, the owner's choice, captions, training, publishing, and a test - by sequencing the skills that do each step, for the model family the owner chooses. Use when the owner asks for a LoRA of a character in plain words, such as "create a LoRA out of this image of a character" or "make Mira a LoRA". It writes no images, captions, or settings itself. Not for one step on its own, and not for a style LoRA.
---

# Character LoRA

A character LoRA is made by one chain of skills, and this skill keeps the chain in order. The point of the test at the end is whether the character comes out recognizably as designed. How a checkpoint or style draws it is up to the model.

Every step keeps its own skill's approvals. Nothing renders, trains, or spends money without the owner's yes to that step's plan, and the owner chooses every image. Report progress during long steps.

## Find the specifics

- **The family** the LoRA is for comes from the owner. Ask when the request does not say. Its workflow skill must have a training recipe; if it has none, say so before starting.
- **This setup's execution skill** that implements `create-character-lora` says:
  - where a character's folders live: the folder the LoRA is made from, and the archive of its artwork;
  - how to make a new character's folders;
  - which working folders each step uses.
- **Each step's own skill** finds its own execution and workflow skills.

All come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

Before each step, check that its skill is listed. If one is missing, say which and stop. Never do a step by hand because its skill is missing.

## The chain

1. **Reference** (**create-character-reference**).
   - It writes the brief, with the trigger word and the fixed traits in the family's prompting style.
   - It makes the sheets, and the gallery the dataset is chosen from, with an image-edit model.
   - The owner approves the brief and the sheets, then chooses gallery images.
2. **Cleanup** (**clean-artwork**).
   - It denoises the chosen images and the top sheets, and shows them beside the originals.
   - The owner chooses per image.
3. **Dataset.**
   - The kept images go into the character's LoRA folder, in `dataset/`, each named by its row id.
   - The brief and the cleaned sheets go into its `ref/`.
4. **Captions** (**caption-lora-dataset**). Each caption is what you would write to make that image. The owner reviews them.
5. **Training** (**train-lora**).
   - It shows the plan with its cost, and trains on the owner's yes.
   - It publishes `<family>_<character>_v<N>`, with its licence and a README on how to prompt the character.
6. **Test** (**test-lora**).
   - It covers breadth, not epochs or strengths.
   - It reports identity first: hair, eyes, outfit, and proportions.
   - The owner judges.
7. **Archive.** On the owner's word, the gallery, its denoised copies, and the test go to the character's artwork archive.

Commit and push only when the owner asks.

When a step fails the character, change that step's skill, then repeat from that step.
