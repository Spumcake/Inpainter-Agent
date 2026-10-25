---
name: image-to-video-prompt-guide
description: Write a prompt for a short video with any video model - what moves and how, what the camera does, how the clip ends, and the sound - written to agree with the first and last frames, then hand it to write-prompt in the model's own syntax. Use when image-to-video needs a new prompt. Prompt writing only; it never renders.
---

# Video prompts

A video prompt describes what changes, not what the first frame already shows. The frames carry the look; the prompt carries the time.

Write it in this order, for any model:

1. **The action:** who moves, what they do, in the order it happens, such as "she turns her head toward the window, then smiles".
2. **The pace:** slow, steady, or sudden; one action per few seconds is believable. A short clip cannot hold many actions.
3. **The camera:** still, a slow push in, a pan, or a handheld sway. One camera move per clip is safest.
4. **The ending:** how the clip arrives at the last frame, when there is one, without contradicting it.
5. **The sound,** when the model makes sound:
   - the setting's ambience;
   - the sounds of the action, such as footsteps;
   - music or voices, when wanted.

   Spoken words are quoted exactly.
6. **What must not change,** when it matters, such as the character's outfit or the time of day.

Describe the characters only as the frames show them, and by role ("the girl in the red cap"), never by a real person's name. Keep it to a few clear sentences; long prompts make models drop parts. Leave out what the model ignores, as its prompt skill says.

## Find the specifics

- **The workflow skill** says which graph or service the request uses, and which field or input each part fills, such as the description into one field, the first frame and last frame into their own inputs, and the sound into the same field or its own.
- **Its prompt skill**, `prompt-skills/<name>.md` in the workflow repository, gives the model's own syntax and limits: sentences or tags, how sound is described, and the longest clip.
- **write-prompt** writes the prompt file.

## Write it

1. Look at the frames, and gather the action, the camera, the ending, and the sound from the request. Ask for the action when it is missing.
2. Draft the description in the order above, agreeing with what the frames show.
3. Put each part into its field in the model's syntax, as its prompt skill says, and name the frames as the job's inputs.
4. Write it with **write-prompt**, naming the prompt skill the workflow skill gives for this request, and return the prompt's name.
