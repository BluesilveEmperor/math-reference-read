# Excalidraw Integration into math-reference-read

## Motivation

math-reference-read produces text-only review reports from math PDFs. Adding excalidraw enables:
- Concept diagrams / methodology flowcharts alongside reviews
- Report cover diagram for PDF export
- On-demand diagram generation via trigger keywords

## Architecture

Follow the exact pattern established in math-read-do:

```
math-reference-read/
├── SKILL.md               # + YAML routing, triggers, compatibility
├── excalidraw/             # copied from math-read-do/excalidraw/
│   ├── SKILL.md
│   ├── README.md
│   └── references/
│       ├── color-palette.md
│       ├── element-templates.md
│       ├── render_excalidraw.py
│       └── pyproject.toml
```

No shared layer needed — excalidraw is fully self-contained.

## Integration Points (3 locations)

| # | Location | What changes | Output |
|---|----------|-------------|--------|
| 1 | YAML frontmatter | description +exc算法 bullet; triggers +excal算法 keywords; compatibility +playwright | — |
| 2 | After Step 3 (report gen) | "可选: 生成图示" — concept / method / architecture diagram | `[name]_图示_概念图.png` |
| 3 | After Step 4 (export) | "可选: 生成封面图" — report cover with annotations | `[name]_封面图.png` |

## New Section: "## 集成子技能"

```
## 集成子技能 / Integrated Sub-Skills

本 skill 集成了一个 Excalidraw 图示子技能 (excalidraw/)，位于 math-reference-read/
目录下，可作为独立 skill 被调用，也可在报告生成后增强视觉呈现。

### 子技能路由

| 子技能 | 目录 | 入口文件 | 主要用途 |
|--------|------|---------|---------|
| excalidraw | excalidraw/ | SKILL.md + README.md | 概念图/流程图, PNG 标注覆盖, excalidraw→PNG 渲染 |

### 与主流程的协同

- **excalidraw** 在 Step 3 报告生成后可选生成论文结构图/方法流程图;
  在 Step 4 导出时可选生成封面概览图。

### 调用方式

通过 sub-skill 路由加载，无需额外配置。
```

## File Operations

1. Copy `excalidraw/` from math-read-do → math-reference-read/
2. Edit `SKILL.md`:
   - YAML description: add exc算法 bullet
   - YAML triggers: add exc算法 trigger line
   - YAML compatibility: add playwright dep
   - After Step 3 export: add optional diagram step
   - After Step 4: add optional cover diagram step
   - Before end of file: insert "## 集成子技能" section

## Non-Goals

- No nature-figure integration (excalidraw standalone per user decision)
- No shared layer
- No changes to report templates

## Verification

- `git status` shows excalidraw/ + modified SKILL.md
- grep excalidraw in SKILL.md reveals all 5+ integration points
