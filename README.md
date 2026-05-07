# drake-themes

A Quarto extension providing a small family of Reveal.js presentation
themes for academic talks. Serif typography, dark backgrounds by default,
with a light-flip layout for figure-heavy slides.

## Palettes

| Skin       | Use case                               | Background    | Accent          |
|------------|----------------------------------------|---------------|-----------------|
| `navy`     | Conferences, external talks            | Deep navy     | Antique gold    |
| `charcoal` | Working seminars                       | Warm charcoal | Slate blue      |
| `burgundy` | Named or distinguished lectures        | Deep burgundy | Champagne       |
| `forest`   | Ecology / teaching (ECOL 8910 etc.)    | Forest green  | Parchment       |

All four share `base.css` (typography, layout, captions). A skin only
overrides the color variables — swapping skins is a one-line change in
the YAML header.

## Install

In any Quarto project directory:

```bash
quarto add jdrake/drake-themes
```

This adds the extension under `_extensions/drake-themes/`. Commit that
directory so collaborators get the theme automatically.

To update later:

```bash
quarto update drake-themes
```

## Use

In a `.qmd` file's YAML header, pick one of the four formats:

```yaml
---
title: "Talk title"
format: drake-themes-navy-revealjs
---
```

Replace `navy` with `charcoal`, `burgundy`, or `forest` as needed.

## Slide-level features

The themes add a few opt-in classes:

**Light-background figure slide** — flip a single slide to a light
background for figures or quotes:

```markdown
## Slide title {.figure-slide}

![](figures/plot.png)
```

**Section divider** — centered, italic, accent-colored:

```markdown
# Methods {.divider}
```

**Frosted caption over background image** — for text overlaid on a
full-bleed image:

```markdown
## {background-image="figures/field.jpg" background-size="cover"}

::: {.frosted}
Caption text here.
:::
```

**Sans-serif source/caption line** — for figure attributions or notes:

```html
<p class="caption">Source: Author, Year.</p>
```

## See also

`template.qmd` in the repo root demonstrates every slide type in a single
deck. Render it with `quarto render template.qmd` to preview.

## Modifying the themes

The architecture is deliberately minimal:

- `base.css` — all shared logic. Change typography or layout here.
- `<skin>.css` — six CSS variables. Change colors here.

To add a new palette, copy one of the existing skin files, edit the
variables, and add a corresponding format entry in `_extension.yml`.

## License

MIT.
