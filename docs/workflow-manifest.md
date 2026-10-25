# Workflow repositories and workflow.json

A workflow repository holds everything specific to one model family, as data that tools read and as a workflow skill that people and agents read. As the owner set on 2026-10-24, a model family's specifics live only here. The runner, the general skills, and the execution skills read them, and carry none themselves.

## Layout

```text
<family>-workflows/
  workflow.json                        what scripts read
  workflows/<graph>.graph.json         graphs, in the runner's graph format
  presets/<look>.json                  looks
  prompt-skills/<name>.md              how to write a prompt for a graph
  training/                            optional: the trainer's templates
  .project/skills/workflow/<family>-workflows/SKILL.md   the workflow skill
```

A graph, look, or prompt skill name is unique across every workflow repository a setup has.

## workflow.json

UTF-8 JSON, `format` `workflow-v1`. Only `format` and `family` are required. A section the family does not have is left out: a voice model has no `lora` or `training`.

```json
{
  "format": "workflow-v1",
  "family": "illustrious",
  "fillers": {
    "positive": { "kind": "danbooru-tags", "sources": ["posts", "subject"] }
  },
  "captions": {
    "style": "tags",
    "tagger": "danbooru-tags",
    "groups": "danbooru-tags"
  },
  "lora": {
    "base": { "slots": ["checkpoint"] },
    "slots": ["lora_2", "lora_3", "lora_4"],
    "character_slot": "lora_1",
    "character_strength": 1.0,
    "refused": ["hard-degenerate"],
    "short_names": { "sd-xl_illustrious": "illustrious-base" },
    "checkpoints": { "card_base_model": ["Illustrious"] }
  },
  "training": {
    "trainer": "kohya-ss/sd-scripts",
    "image": "<container image pinned by digest>",
    "install": ["<shell lines run in the Pod before training>"],
    "files": { "train.toml": "training/train.toml", "dataset.toml": "training/dataset.toml" },
    "command": "accelerate launch ... sdxl_train_network.py --config_file {run_dir}/train.toml",
    "base_model": "<models-relative path of the base model>",
    "min_gpu_memory_gb": 24,
    "settings": { "max_train_epochs": 10, "num_repeats": 8, "batch_size": 4 },
    "epoch_files": "{output_name}-{epoch:06d}.safetensors",
    "final_file": "{output_name}.safetensors"
  },
  "licence": {
    "text": "LICENSE-LORA.md",
    "note": "<the line written into a derived file's metadata>",
    "use": "<the rule that travels with anything derived, such as ideation only>"
  }
}
```

### Sections

- **`family`:** a short lowercase name, used in file names, such as `illustrious_<character>_v<N>.safetensors`.
- **`fillers`:** for each prompt field that is not written directly, which filler writes it and from what sources.
  - `kind` names the repository that provides the filler, and its execution skill says how to run it.
  - The filler runs before the runner's `prompt` command, and writes a jobs file for it.
  - A field with no filler is written by the agent or by a model pass.
- **`captions`:** how a LoRA dataset's captions are written.
  - `style` is `tags` or `sentences`.
  - `tagger` names the filler kind that drafts tag captions from images.
  - `groups` names the filler kind that sorts caption tags into expressions, poses, views, settings, and the rest, for a LoRA test.
- **`lora`:** what is true of this family's LoRAs:
  - `base`: the slots that make a look's base model, such as `["checkpoint"]`, or `["diffusion_model", "text_encoder", "vae"]` for a family that loads them apart. `vary`, by default the first slot, is the one a LoRA test covers with one look per model; the other base slots are kept from an existing look;
  - the preset slots a look stacks LoRAs in, and the character LoRA's slot and strength;
  - LoRAs refused with a character, matched by name;
  - short names for file names; a name not listed is shortened by removing a leading `<family>_`;
  - which base models a LoRA test must cover: those in the `vary` slot's folder whose model card's base model is in `card_base_model`.

  Where LoRAs live on disk is a setup value, not this file's.
- **`training`:** the recipe a training execution skill runs:
  - `image` and `install`: the container and the commands that prepare the trainer, all pinned;
  - `files`: templates, which the skill fills and uploads beside the dataset;
  - `command`: run in the Pod;
  - `base_model`, `min_gpu_memory_gb`, `settings`, the name of each numbered epoch's file, and `final_file`, the last epoch's name when the trainer writes it without a number;
  - any other key, such as version pins, is the recipe's own, and is only read by its templates.

  Templates and `command` use these placeholders:
  - `{run_dir}`, `{dataset_dir}`, `{output_dir}`, `{output_name}`, and `{models_dir}`;
  - `{base_model}` and `{licence_note}`;
  - `{settings.<key>}`.

  The datacenter, volume, GPU list, time limit, and prices are setup values.
- **`licence`:** the licence file that goes with anything derived from this family, the note written into a derived file, and the use rule.
