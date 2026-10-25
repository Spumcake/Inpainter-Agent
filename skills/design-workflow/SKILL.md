---
name: design-workflow
description: Add a model family's workflow - a graph, a look, a prompt skill, its workflow.json, and its workflow skill - to that family's workflow repository, so every general skill can use the model without being changed. Use when adding a new model, a new graph or pass for one, or a new look or prompt skill variation.
---

# Design a workflow

A workflow repository holds everything specific to one model family, and nothing about a setup. Its layout and its `workflow.json` are in the [workflow manifest](../../docs/workflow-manifest.md).

## Find the specifics

The **execution skill** that implements `design-workflow` in this setup says the graph format: how fields, inputs, settings, outputs, and model slots are declared, and how to check a look against a server. It comes from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## Write it from facts

- **Use the model's official example workflow** where one exists, carried over node for node rather than redesigned. Choose one configuration aimed at a keeper-quality result, with the setup's hardware as a limit, not a requirement.
- **Use logical model names,** never a filename only one server has.
- **Take triggers, quality words, negatives, and sampler settings from each model's card** or its own metadata. Never invent one.
- **Declare everything the graph takes and makes:** its text fields, its input files and their kinds, the settings a render may choose, its outputs, and where it may run when it only fits some servers.
- **A look** names its models and what it adds to each field.
- **A prompt skill** says how to write a good prompt for this graph, with a **For the model** section a model pass receives.
- **`workflow.json`** carries the family's facts as data: its fillers, caption style, LoRA rules, training recipe, and licence. It carries no folders, prices, or servers; those are the setup's.
- **The workflow skill** explains the same facts for people and agents. It holds only facts and dated owner decisions.

When the server lacks a model, follow the **find-missing-models** skill. Download nothing without the owner's approval of that file.

## Offering it

A new look or prompt skill is offered by adding it to what the workflow skill allows. Change a default only when the owner asks. Check which servers can run a new look, and report it.

## Stop

Return the paths. Do not render; a first render is a plan for the owner's yes, through the **run-prompt** skill.
