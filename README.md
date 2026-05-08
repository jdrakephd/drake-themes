# drake-themes

A Quarto extension providing a small family of Reveal.js presentation
themes for academic talks. Serif typography, dark backgrounds by default,
with specialized slide types for figures, transitions, and more.

## Palettes

| Skin       | Format name                | Use case                            |
|------------|----------------------------|-------------------------------------|
| `navy`     | `drake-navy-revealjs`      | Conferences, external talks         |
| `charcoal` | `drake-charcoal-revealjs`  | Working seminars                    |
| `burgundy` | `drake-burgundy-revealjs`  | Named or distinguished lectures     |
| `forest`   | `drake-forest-revealjs`    | Ecology / teaching (ECOL 8910 etc.) |

All four share `base.css` (typography, layout, captions) from
`_extensions/shared/`. Each skin adds its own color variables and
distinctive typographic overrides.

## Install

In any Quarto project directory:

```bash
quarto add jdrakephd/drake-themes
```

This adds the extensions under `_extensions/`. Commit that directory
so collaborators get the themes automatically.

## Use

In a `.qmd` file's YAML header, pick one of the four formats:

```yaml
---
title: "Talk title"
subtitle: "Optional subtitle"
author: "Author Name"
institute: "Affiliation"
event: "Conference or Seminar Name"
location: "City, Venue"
date: today
format:
  drake-navy-revealjs:
    slide-number: c/t
---
```

Replace `drake-navy` with `drake-charcoal`, `drake-burgundy`, or
`drake-forest` as needed.

### Title slide fields

The themes provide a custom title slide with the following YAML fields:

| Field       | Required | Description                              |
|-------------|:--------:|------------------------------------------|
| `title`     | yes      | Talk title                               |
| `subtitle`  | no       | Subtitle, displayed below title          |
| `author`    | yes      | Speaker name                             |
| `institute` | no       | Affiliation                              |
| `event`     | no       | Conference, seminar, or course name      |
| `location`  | no       | Venue or city                            |
| `date`      | yes      | Renders as "MMMM D, YYYY" by default    |

## Slide types

### Standard content slide

The default. Dark background, light serif text.

```markdown
## Slide title

Content goes here with **bold** and *italic* text.
```

### Section divider

Centered, italic, accent-colored heading. Use for lightweight
section breaks.

```markdown
# Section name {.divider}
```

### Transition slide

Inverted color scheme — the accent color fills the entire background
with the theme's dark color used for text. Use for major section
breaks.

```markdown
# New Section {.transition}

Optional subtitle text
```

### Figure slide (white background)

Pure white background with dark text. Ideal for pre-made figures
that have white backgrounds, giving clean lines with no color mismatch.

```markdown
## Figure title {.figure}

![](figures/plot.png){fig-align="center"}

<p class="caption">Figure caption here.</p>
```

### Figure slide (tinted background)

Light, warm-tinted background using the theme's `--bg-alt` color.
A softer alternative to the pure-white `.figure` slide.

```markdown
## Figure title {.figure-slide}

![](figures/plot.png){fig-align="center"}
```

### Full-bleed image slide

A photograph or image fills the entire slide. Use an empty `##`
heading for a titleless slide.

```markdown
## {.full-image background-image="figures/photo.png" background-size="cover" background-position="center"}

::: {.full-image-label}
Optional label text
:::
```

### Frosted caption over background image

Text overlaid on a full-bleed image with a frosted-glass effect.

```markdown
## {background-image="figures/field.jpg" background-size="cover"}

::: {.frosted}
Caption text here.
:::
```

### Watermark slide

A faded background image behind content, useful for institutional
branding or acknowledgment slides.

```markdown
## Acknowledgments {.watermark background-image="figures/seal.png" background-size="contain" background-position="center" background-opacity="0.12"}

Thank you to our sponsors.
```

Adjust `background-opacity` (0.08--0.20) to taste. The `.watermark`
class adds a text shadow so content stays legible.

### Collaborators slide

Circular portrait photos arranged in a row with names underneath.
Images are automatically cropped to circles with an accent-color
border.

```markdown
## Collaborators {.collaborators}

::: {.people}

::: {.person}
![](figures/alice.jpg)

Alice Smith
:::

::: {.person}
![](figures/bob.jpg)

Bob Jones
:::

:::
```

Wrap all `.person` divs in a single `.people` container. The layout
uses flexbox and will wrap to multiple rows if needed.

### Source/caption line

A small, muted line for figure attributions or notes.

```html
<p class="caption">Source: Author, Year.</p>
```

## Examples

The `examples/` directory contains a full demo deck for each theme
showing every slide type. Render any of them:

```bash
quarto render examples/navy-example.qmd
quarto render examples/charcoal-example.qmd
quarto render examples/burgundy-example.qmd
quarto render examples/forest-example.qmd
```

## Modifying the themes

The architecture is deliberately minimal:

```
_extensions/
  shared/
    base.css               — all shared typography, layout, and slide types
    title-slide.html       — custom title slide partial (event/location fields)
  drake-navy/
    _extension.yml
    navy.css               — navy color variables + typographic overrides
  drake-charcoal/...
  drake-burgundy/...
  drake-forest/...
```

- `shared/base.css` — change typography, layout, or add new slide types here.
- `shared/title-slide.html` — modify the title slide structure here.
- `<skin>.css` — change colors and theme-specific styling here.

To add a new palette, create a new `_extensions/drake-<name>/`
directory with an `_extension.yml` and skin CSS file. Use an existing
skin as a template.

## License

MIT.
