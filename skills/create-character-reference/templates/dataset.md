# Dataset plan: {{name}}

The gallery a character LoRA is trained on. Every image is drawn from the approved reference sheets, so identity stays fixed while framing, view, outfit, expression, and background vary. Fill the matrix, then write one prompt file per row with the entry template below.

## The matrix

About 36 images, one row each, as the owner approved on 2026-10-19. Five framings:

| Framing | Rows | What is in frame | Mix |
|---|---|---|---|
| **full-body standing** | 6 | head to feet, relaxed stance | front, three-quarter, side, back in the default outfit; front and back in each other outfit |
| **full-body action** | 6 | head to feet, doing something | everyday actions that suit the character: walking, sitting, crouching, using the prop; at least one per other outfit |
| **upper-body** | 10 | waist or thigh up | varied poses, gestures, and expressions; two with the camera above, two below; two without removable headwear in the default outfit |
| **portrait** | 6 | head and shoulders | front, three-quarter, side, back, across outfits |
| **expression** | 8 | face close-up, head and neck | the core expressions (neutral, happy, angry, sad, surprised), the signature expression, and two more that suit the character, spread over front, three-quarter, and side |

- **Views and angles**: every outfit is seen from more than one side. The back view appears only in full-body and portrait rows; an expression has no back view.
- **Poses**: no more than a third of the rows are plain standing. A dataset of only standing poses trains a stiff LoRA.
- **Headwear and accessories**: anything removable appears off at least twice in the default outfit, so the LoRA does not tie its absence to another outfit.
- **Props**: in two to four rows, held or used naturally. Most rows have none.
- **Backgrounds**: about a third plain white or light grey; the rest simple, uncluttered settings that suit the character, never the same twice in a row. A dataset that is all white teaches the LoRA to draw only white backgrounds.
- **Not in the dataset**: the reference sheets themselves; several views on one image confuse training.
- **Content**: clothing and poses stay ordinary and everyday. A character who reads as a minor is never drawn in sexual or suggestive ways, in any row or caption.

| id | framing | view | outfit | expression | prop | background |
|---|---|---|---|---|---|---|
| `fb-front-{{outfit}}` | full-body | front | | | | |

## Entry prompt

One file per row, named for its id (for example `fb-front-hoodie.md`), generated with the base sheet as the first reference image, the outfit sheet when the row's outfit is not the default, and the prop sheet when the row has that prop.

```markdown
---
aspect_ratio: "{{2:3 for full-body, 3:2 for wide action, 3:4 for upper-body and portrait, 1:1 for expression}}"
quality: high
---
## Prompt

A single illustration of {{name}}, exactly as drawn on the attached reference sheets: same face, hair, eyes, proportions, colours, and art style ({{art_style}}).

- Framing: {{framing description}}.
- View: {{view}}, {{pose}}.
- Outfit: {{outfit description from the brief}}.
- Expression: {{expression}}.
- Prop: {{prop, or "none"}}.
- Background: {{background}}.

One character only. No text, labels, borders, or panels. The character fills the frame as the framing says.
```

## Kept images

The owner's choice for each row, once the gallery is cleaned up: `original`, `cleanup`, or `dropped`. Only kept rows are published into the character's `dataset/`.

| id | keep |
|---|---|
| `fb-front-{{outfit}}` | |
