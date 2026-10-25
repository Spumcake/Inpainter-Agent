# Character brief: {{name}}

Fill every field from the owner's request and the input images. Write "not specified" rather than inventing. Keep it short: the brief feeds the reference sheets and the dataset, and anything not listed here should not appear in either.

## Identity

- **Name:**
- **Trigger word:** a short, unusual token for the LoRA, such as `miraoc`
- **Role or concept:** one line
- **Personality:** three to five words
- **Signature expression:** the face the character makes most, beyond the core set

## Look

- **Art style:** the style of the input images, in a few words (for example, flat 2D anime cel shading, clean black linework)
- **Hair:** colour, length, shape
- **Eyes:** colour, shape
- **Skin:**
- **Build and proportions:** describe as drawn in the input images; do not add body measurements
- **Fixed traits:** what never changes between outfits
- **Fixed tags:** the fixed traits, comma-separated, in the prompting style of the model family the LoRA is for (its workflow skill says which; for a tag-prompted family, for example `long hair, green hair, green eyes`); every caption and every prompt for the character writes them after the trigger word

## Outfits

One entry per outfit. The first is the default.

- **{{outfit}}:** every visible garment, colour, and detail, top to bottom

## Props

- **{{prop}}:** what it is, colour, material, and how it is held or worn

## Palette

Five to eight colours, named, in order of area.

## Input images

- `{{path}}`: what it shows (outfit, expression, prop)
