---
name: image-to-video
description: Make a short video with any video model - from a first frame, optionally a last frame, and a description of the motion and sound, or from a description alone when the model allows it - and present it for the owner to judge. Use when someone asks to animate an image, make a clip, or bring a still to life. Not for music or speech on their own.
---

# Make a video

The person gives a starting image, and optionally an ending image, and describes what happens between them. They get back a short clip, with sound when the model makes it.

A good clip keeps what the images show: the characters stay on model, and the setting stays the same. It moves the way the description says, at a believable pace, and ends where the last frame says it ends. A clip where a character melts, morphs, or turns into someone else has failed, however smooth it is. The owner judges by watching; never score it.

Use only images the owner has the right to use this way. Animate a recognisable real person only when the owner confirms that the person agreed to this use, or a guardian did for a child, the same as for a cloned voice. Never make a clip that shows a real person doing or saying something they did not, to deceive anyone. A character who reads as a minor stays ordinary and everyday: nothing sexual or suggestive, ever. Nothing of that kind involving minors is made by any route.

## Find the specifics

- **The prompt guide,** `image-to-video-prompt-guide`, says what a good video prompt holds.
- **The workflow skill** of the model family the request names, or that the owner chooses, says:
  - which graph takes a first frame, a last frame, or text alone;
  - how long a clip it makes;
  - whether it makes sound;
  - where it runs.

  When the request names no model and more than one fits, ask.
- **The execution skill** that implements `image-to-video` in this setup renders it; when none does, the one that implements `run-prompt`.

All come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md). If one is missing, say which and stop.

## 1. What it needs

- The first frame, and the last frame when the person has one, as images. Check that their sizes fit the graph, and that the last frame shows the same characters and setting.
- The description of what happens: the motion, the camera, and the sound.
- The length, when the person cares. Otherwise use the workflow's default.

Ask for anything missing. Never invent a character's appearance the images do not show.

## 2. Prompt

Write the prompt with **image-to-video-prompt-guide**.

## 3. Plan

Video is the most expensive kind of media, so the plan is explicit. Show, and wait for the owner's yes:

- the model, its graph or service, and its look or settings, and where it runs;
- the frames;
- the length, the size, and the number of takes;
- the cost, from the setup's prices, including starting the server when it is cold;
- anything missing.

A first clip on a new model or server is a short test before any longer one.

## 4. Render and report

Render with the execution skill found above. Report each output's path, with the first and last frames beside it so the owner can compare them. Say honestly where it drifted: faces, hands, colours, or the ending frame. The owner chooses what to keep; a new take is a new plan.
