---
name: write-prompt
description: Write a new prompt for a graph - fill its fields from the request, with the filler the model family uses (such as tags read from posts) or in words, then optionally have a model revise it in a pass the endpoint registry chooses. Use when a request needs a new prompt. Prompt writing only; it never chooses a look or renders.
---

# Write a prompt

A prompt holds what will be said to the model, one job per thing to make. It holds no models, look, seeds, settings, or server. Choosing a look and rendering are the **run-prompt** skill's work.

## Find the specifics

- **The workflow skill** of the model family says:
  - which graph and prompt skill the request uses, and which fields that graph has;
  - which field a filler writes, such as tags read from posts;
  - how a good prompt for this model reads.
- **The execution skill** that implements `write-prompt` in this setup says the commands that write the prompt and save a pass. When a field has a filler, the helper skill of the repository the workflow names for it says how to run it.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md). Never use a prompt skill the workflow skill does not allow, and never invent rules or trigger words.

## Name it

Choose two or three lowercase words, joined by hyphens, that say what the prompt is, such as `beach-portraits`. The name must be unique among the existing prompts, with no dates or random strings. If the person gives a name, use theirs.

## Fill the fields

- **A field with a filler** is written by the filler, from the sources the request gives, such as post URLs or a subject. Never assemble a filler's output by hand. When the filler fails on a source, stop and report that source.
- **A field without a filler**, such as lyrics or a voice line, is written from the request in the model's own style, as its prompt skill says.
- **An input a job needs,** such as a source image or a song, is named as the person gave it.

Then write the prompt with the execution skill.

## A model pass

A pass is a model revising the prompt's fields. Passes are numbered from 1.

- It needs an endpoint registry and a remote-task runner from the setup. Without them, say no pass was run.
- **Choose the endpoint:**
  - the one the owner names;
  - otherwise the registry's first matching route;
  - otherwise its default for written artifacts.

  Consider only endpoints whose tasks include prompt writing. Never switch models silently. If the chosen one cannot run, say so and ask.
- **A billed endpoint waits for a yes** to a plan naming:
  - the endpoint and the model;
  - why it was chosen;
  - the whole cost, including starting it and the time it stays up idle;
  - that a retry may double the cost.
- **An in-session endpoint** means you revise the fields yourself, following the prompt skill's **For the model** section.
- **Save the pass** with the execution skill. It keeps the filler's original output beside the revision.

Never send or relay a request whose purpose is sexually explicit content; say so, and give the owner the commands to run themselves. Nothing involving minors is written or sent by any route.

## Curate

Edit fields by hand only when the owner asks, and record who changed them. A prompt that has been rendered is never rewritten; a different prompt gets a new name. Stop when the prompt is ready, and return its name.
