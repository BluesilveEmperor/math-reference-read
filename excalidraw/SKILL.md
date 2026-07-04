---
name: excalidraw
description: >-
  Generate Excalidraw concept diagrams, workflow visualizations, and annotation
  overlays for math-read-do reproduction reports. Enhances nature-figure data
  plots with arrows, callouts, and [A][B] markers. Covers Phase 5.5 (annotation
  overlay), Phase 6 (architecture/judgment diagrams), Phase 7 (cover/method overview).
  Triggers: diagram, flowchart, architecture, workflow, cover diagram, annotation overlay.
---

# Excalidraw Diagram — math-read-do Integration

Generate `.excalidraw` JSON files that **argue visually**, then render to PNG.

**Setup:** If the render pipeline hasn't been set up:
```bash
cd excalidraw/references
uv sync
uv run playwright install chromium
```

## Customization

All colors in `references/color-palette.md`. Read it before generating any
diagram and use as the single source of truth.

## Core Philosophy

**Diagrams should ARGUE, not DISPLAY.** The shape should BE the meaning.
See the original excalidraw-diagram-skill SKILL.md for full methodology.

## Integration Phases

### Phase 5.5: Annotation Overlay

After nature-figure exports a PNG, this skill reads it as a background image,
overlays [A][B][C] markers, arrows, and callout boxes.

Data flow:
1. Read `excalidraw_manifest.json` for `sources[]` list
2. For each source, load its PNG as excalidraw `image` element
3. Add annotation elements referencing `region` → [A]/[B] labels
4. Export as both PNG and PDF

### Phase 6: Diagrams for Report

- Architecture diagram showing Phase 0→7 data flow
- Judgment decision tree (five-state verdict visualization)
- Methods overview diagram

### Phase 7: Final Polish

- Cover diagram (paper method + nature-figure hero panel + annotations)
- Workflow summary (end-to-end pipeline visual)

## Rendering

```bash
cd 实验复刻结果汇总/实验图表（含代码）
python "$SKILL_DIR/excalidraw/references/render_excalidraw.py" \
  diagram.excalidraw --output annotated_diagram.png
```

## Quality Checklist

1. **Research done**: Specs/colors correct?
2. **Multi-zoom**: Summary + section boundaries + detail?
3. **Connections**: Every relationship has an arrow?
4. **Color meaning**: Colors encode semantics, not decoration?
5. **Overlay alignment**: [A][B] markers precisely match PNG source?
6. **Render validation**: PNG inspected and visually verified?
