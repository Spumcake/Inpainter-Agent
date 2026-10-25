---
name: find-missing-models
description: List the models a server lacks for a look or graph - with each model's kind, folder, official source, size, and licence - and download one only after the owner approves that file. Use when a server cannot run a look, or when someone asks where to get a missing model.
---

# Find missing models

## Find the specifics

The **execution skill** that implements `find-missing-models` in this setup says how to check a look against a server, and which folder each kind of model goes in. The **workflow skill** says which models a look uses and where the model family publishes them. Both come from the setup's skill listing; see the [skill layers](../../docs/skill-layers.md).

## List

For each model the server cannot resolve, report:

- the logical name;
- the kind;
- the target folder;
- an official source;
- the size;
- the licence.

Prefer the model author's own file, then the platform's official repackaging. If neither exists, say so. Never invent a source, a size, or a licence.

A graph marked as running only on some kinds of server is not missing anything elsewhere. Report where it runs, and never offer to download its models onto a server it does not run on.

## Download

- Never download without the owner's approval of that file. A yes to a render plan is not approval of a file.
- Download only into this setup's own models folder, never for a server other people reach.
- After the download, make the model's card when the execution skill has one, and check the server again.
- Never move or delete a model file without the owner's word.
