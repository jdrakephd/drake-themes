# drake-themes

Quarto Reveal.js presentation themes for academic talks and teaching.
Two theme families: **academic** (dark backgrounds, serif typography)
and **teach** (light backgrounds, sans-serif, bold color palette).

## Academic themes

Dark backgrounds with serif typography. Each has a distinctive
typographic character.

| Skin       | Format name                | Use case                            |
|------------|----------------------------|-------------------------------------|
| `navy`     | `drake-navy-revealjs`      | Conferences, external talks         |
| `charcoal` | `drake-charcoal-revealjs`  | Working seminars                    |
| `burgundy` | `drake-burgundy-revealjs`  | Named or distinguished lectures     |
| `forest`   | `drake-forest-revealjs`    | Ecology / teaching (ECOL 8910 etc.) |

## Teaching themes

Light backgrounds with DM Sans typography. Each color is designed
so that every lecture in a course gets a different primary color
while the overall feel stays consistent.

| Color    | Format name                    | Hex       |
|----------|--------------------------------|-----------|
| `coral`  | `drake-teach-coral-revealjs`   | `#e63946` |
| `teal`   | `drake-teach-teal-revealjs`    | `#2a9d8f` |
| `violet` | `drake-teach-violet-revealjs`  | `#7b2d8e` |
| `blue`   | `drake-teach-blue-revealjs`    | `#2563eb` |
| `orange` | `drake-teach-orange-revealjs`  | `#e76f51` |
| `green`  | `drake-teach-green-revealjs`   | `#16a34a` |
| `pink`   | `drake-teach-pink-revealjs`    | `#db2777` |
| `amber`  | `drake-teach-amber-revealjs`   | `#d97706` |

Author defaults to "John M. Drake" in the teaching themes.

## Install

In any Quarto project directory:

```bash
quarto add jdrakephd/drake-themes
```

This adds the extensions under `_extensions/`. Commit that directory
so collaborators get the themes automatically.

## Use

### Academic theme

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

### Teaching theme

```yaml
---
title: "Lecture 4 --- Population Regulation"
subtitle: "Density dependence and its consequences"
event: "ECOL 3500 --- Ecology"
location: "Room 200, Biological Sciences"
date: today
format:
  drake-teach-coral-revealjs:
    slide-number: c/t
---
```

Author defaults to "John M. Drake" in teaching themes (override
in YAML if needed). Swap `coral` with any other color for the
next lecture.

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

### Figure slide (dark background)

Uses the theme's dark background color. For figures drawn in
light colors on a transparent background — they render naturally
without a white box around them.

```markdown
## Figure title {.figure-dark}

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
# Academic themes
quarto render examples/navy-example.qmd
quarto render examples/charcoal-example.qmd
quarto render examples/burgundy-example.qmd
quarto render examples/forest-example.qmd

# Teaching theme
quarto render examples/teach-coral-example.qmd
```

## Modifying the themes

The architecture is deliberately minimal:

```
_extensions/
  shared/
    base.css               — academic theme: shared typography, layout, slide types
    teach-base.css         — teaching theme: shared typography, layout, slide types
    title-slide.html       — custom title slide partial (event/location fields)
  drake-navy/              — academic skins (dark background, serif)
  drake-charcoal/
  drake-burgundy/
  drake-forest/
  drake-teach-coral/       — teaching palettes (light background, DM Sans)
  drake-teach-teal/
  drake-teach-violet/
  drake-teach-blue/
  drake-teach-orange/
  drake-teach-green/
  drake-teach-pink/
  drake-teach-amber/
```

- `shared/base.css` — academic theme typography and layout.
- `shared/teach-base.css` — teaching theme typography and layout.
- `shared/title-slide.html` — title slide structure (shared by both families).
- `<skin>.css` — color variables and theme-specific overrides.

To add a new academic palette, create `_extensions/drake-<name>/`.
To add a new teaching color, create `_extensions/drake-teach-<color>/`.

## License

MIT.
