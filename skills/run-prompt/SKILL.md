---
name: run-prompt
description: Render a prompt that already exists - with a look the request allows, on the server the request names - or render it again, elsewhere, with another look, reproduce an earlier render exactly, or send chosen outputs through a follow-up pass such as high-res. Use whenever a written prompt is to be rendered. A new request goes first to the skill that matches it; a new prompt is the write-prompt skill's work. Never writes a prompt.
---

# Run a prompt

You send a prompt that already exists to a server, with the system as it is. You never write or edit a prompt; that is the **write-prompt** skill's work. You never build a graph or a look. If the request needs one that does not exist, say so and stop: that is development, for a separate request.

## Find the specifics

- **The workflow skill** of the prompt's model family says which graphs and looks exist, what each is for, and which looks a request may use.
- **The execution skill** that implements `run-prompt` in this setup says the commands, and how to check, render, reproduce, and pass outputs on.

Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md). Read both before planning. If either is missing, say which and stop.

## Plan

Gather the plan from the request, the prompt, and the execution skill's check:

- the prompt, the prompt skill that wrote it, and its latest model pass;
- the look and the models it resolves to on the named server;
- the server, the graph, and any settings, such as a size or a duration;
- the jobs, the count, and the outputs in total, each with a new seed;
- each job's fields as written; the look is applied when it is sent;
- the cost, from the setup's prices, when the server bills;
- anything missing. When the server cannot run the look, follow the **find-missing-models** skill and put its findings in the plan.

Show the plan and wait for an explicit yes. A yes to a plan never approves a download.

The server is the one the request names. Never start, stop, or restart a server. If it does not answer, say so and stop.

## Send

After the yes, render with the execution skill. Report:

- the render's name;
- each output file's path;
- any output that failed, with its error.

The owner chooses keepers; never judge the outputs.

## Again, elsewhere, or with another look

- **"Again"** sends the same prompt with new seeds.
- **"On <server> too"** sends it to that server.
- **"With another look"** uses another look the workflow skill allows.

Each is a new render, and each waits for a yes to its own plan.

## Reproduce

"Reproduce <render>" repeats an earlier render exactly, from its record: the same text, models, seeds, settings, and inputs.

- The plan names the render being reproduced and the server.
- Afterwards, compare each new output with the original of the same number. Report:
  - whether the server, GPU, or software version differs;
  - that some samplers repeat exactly only on the same kind of GPU.
- If the graph changed since the original, the execution skill refuses. Report that and stop.

## A follow-up pass

"Upscale <outputs> from <render>", or another pass on chosen outputs, uses only the outputs the person names.

- Stop if the family has no graph for that pass.
- Never add outputs the person did not name.
- Show the plan, and wait for a yes.
