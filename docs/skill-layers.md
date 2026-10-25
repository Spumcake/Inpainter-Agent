# Skill layers

How a task is split across skills, so one general skill serves any model and any setup. As the owner set on 2026-10-24.

## The three layers

- **General skill.** It lives in this repository, under `skills/<name>/SKILL.md`, and its name has no prefix, such as `train-lora`.
  - It says how to go about a task: the method, what good looks like, what the owner approves, and when to stop and ask.
  - It names no model, server, folder, key, price, or command.
  - It has no scripts.
  - As the owner set on 2026-10-25, a kind of media comes as a pair of general skills:
    - **a task skill,** such as `image-to-video`, which holds the method and the approvals;
    - **a prompt guide,** `<task>-prompt-guide`, which says what a good prompt for that kind of media holds with any model.

    Every workflow has a prompt skill for each kind of request, whether its model runs as a graph or as a hosted service, and a prompt file holds only named fields, which any execution skill can read. The prompt guide writes through `write-prompt`, and reads each model's own syntax from the graph's prompt skill (a workflow's `prompt-skills/<name>.md`, the only thing called a prompt skill). The task skill renders through an execution skill that implements the task itself, or else through one that implements `run-prompt`.
- **Workflow skill.** It lives in one model family's workflow repository, such as `illustrious-workflows`, and is named after that repository.
  - It says what is true of that model: how to prompt it, what its looks and graphs are for, its training recipe, and its licence.
  - Scripts read the same facts from the repository's `workflow.json`, which [workflow-manifest.md](workflow-manifest.md) describes.
- **Execution skill.** It lives beside the code it runs, in that repository's `.project/skills/<category>/<name>/`, and its name starts with that repository's name, such as `comfyui-runner-run-prompt`.
  - It says how a step is done with that tool: the commands, their options, what they write, and how they fail.
  - Its frontmatter lists the general skills it carries out:

    ```yaml
    ---
    name: comfyui-runner-artwork-set
    description: ...
    implements: [clean-artwork, refine-artwork]
    ---
    ```

  - It names nothing outside its repository. Folders, keys, servers, prices, and how a setup arranges its models folder come from its caller.
- **Helper skill.** An execution skill that a workflow reaches through its `workflow.json`, such as a filler or a tagger, lists `helps: [<general skill>, …]` instead of `implements`. It does one part of a step for the families that name it, and is never an alternative to the step's execution skill. A general skill uses a helper only when the workflow names its repository.

## Setup values

A setup is one place the skills run, such as a person's computer with its servers, or a hosted instance. What belongs to a setup, not to a model, is given to every execution skill by its caller:

- the data folder, the server profiles, and the workflow repositories present;
- key files;
- the cost of a run on each server;
- how the models folder is arranged, for each family:
  - where a new character LoRA is published;
  - which folders hold style LoRAs to stack.

### The setup file

A setup writes its values in one UTF-8 JSON file, `format` `setup-v1`, and gives its path to every execution skill: with `--setup <file>`, or in the `SKILLS_SETUP` environment variable. A tool reads the keys it needs and ignores the rest. A tool that needs a key that is missing stops and names it. A relative path is relative to the file. The file names key files, never keys.

```json
{
  "format": "setup-v1",
  "data": "<folder for prompts, renders, artifacts, and work files>",
  "servers": "<folder of this setup's server profiles and snapshots>",
  "workflows": ["<workflow repository>", "..."],
  "env_file": "<file of NAME=value secrets>",
  "credentials": "<file holding the RunPod API key>",
  "models": "<this computer's ComfyUI models folder>",
  "tagger": "<the WD tagger folder>",
  "prices": { "<profile>": { "per_gpu_hour": 1.75, "note": "..." } },
  "lora": { "<family>": { "publish": "<models-relative folder for character LoRAs>", "styles": ["<models-relative folder>"] } },
  "runpod": {
    "volume": "<network volume id>",
    "datacenter": "<datacenter id>",
    "s3_endpoint": "<the volume's S3 address>",
    "gpu_types": ["<GPU type id>"],
    "container_disk_gb": 60,
    "max_lifetime_minutes": 90,
    "poll_seconds": 60
  }
}
```

The setup's own documents say where its file is.

## Finding the other layers

Every setup that runs these skills must list, for the agent:

- each execution skill, with its repository and its `implements` or `helps` list;
- each workflow skill, with its repository and the path of its `workflow.json`.

A general skill finds its counterparts in that listing, never through a command it names:

1. **The workflow skill** for the model the request names, or the one the owner chooses. When the request names no model and more than one fits, ask.
2. **An execution skill** whose `implements` includes this skill. When several fit, the request decides, such as the server it names. When none fits, say so and stop. Never do the step by hand.

Read both skills completely before planning.

## What every general skill keeps

- Nothing renders, trains, downloads, or spends money before the owner's yes to that specific plan.
- The owner chooses keepers and judges results. A skill never scores a picture or a sound.
- Every image of a character who reads as a minor stays ordinary and everyday. Nothing is sexual or suggestive, in any step, prompt, or caption.
- Long steps report progress, and say what is running and how long it takes before waiting.
