# Excalidraw Diagram — math-read-do Sub-Skill

Enhances reproduction reports with concept diagrams, workflow visualizations,
and annotation overlays on nature-figure plots.

## Setup

```bash
cd excalidraw/references
uv sync
uv run playwright install chromium
```

## Usage

The root SKILL.md orchestrates excalidraw calls in Phases 5.5, 6, and 7.
To generate a diagram standalone: ask your AI agent to create a diagram using
the excalidraw sub-skill.

## File Structure

```
excalidraw/
  SKILL.md                  — Design methodology + workflow
  README.md                 — Setup instructions
  references/
    color-palette.md        — Colors (cross-ref nature-figure PALETTE)
    element-templates.md    — JSON templates for each element type
    render_excalidraw.py    — .excalidraw → PNG via Playwright
    pyproject.toml          — Python dependencies
```

## Customization

Edit `references/color-palette.md` to match brand colors.
