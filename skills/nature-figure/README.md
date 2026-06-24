# nature-figure 技能

`nature-figure` 用于生成可投稿级科研图，面向 Nature 级期刊和高影响力学术场景，同时支持 Python 与 R 两条绘图路径。

## 主要特性

- **投稿级科研图工作流**：面向 Nature、Science、Cell 等高影响力期刊
- **Python/R 双后端支持**：matplotlib/seaborn 和 ggplot2/patchwork/ComplexHeatmap
- **图件契约系统**：从核心结论出发，而非直接套模板
- **配色方案**：内置 Nature 风格配色方案，包括 NMI pastel 系列
- **多面板信息结构**：支持复杂的多面板图设计
- **导出格式**：支持 SVG、PDF、TIFF 等投稿级格式

## 安装

将 `skills/nature-figure` 目录复制到你的 skills 目录中。

## 使用方法

### Python 后端

```python
import matplotlib as mpl
import matplotlib.pyplot as plt

# 必需设置
plt.rcParams['font.family'] = 'sans-serif'
plt.rcParams['font.sans-serif'] = ['Arial', 'DejaVu Sans', 'Liberation Sans']
plt.rcParams['svg.fonttype'] = 'none'

# 绘图代码...
```

### R 后端

```r
library(ggplot2)
library(patchwork)

# 使用预设主题...
```

## 文件结构

```
nature-figure/
├── SKILL.md                     # 路由和工作流
├── manifest.yaml                # 配置清单
├── README.md                    # 本文件
├── static/
│   ├── core/                    # 核心规则
│   │   ├── contract.md          # 图件契约
│   │   └── stance.md            # 默认立场
│   └── fragments/
│       └── backend/             # 后端特定规则
│           ├── python.md        # Python 规则
│           └── r.md             # R 规则
└── references/                  # 深度参考文档
    ├── figure-contract.md       # 图件契约详细说明
    ├── api.md                   # API 参考和常量
    ├── design-theory.md         # 设计理论
    ├── common-patterns.md       # 常用模式
    ├── chart-types.md           # 图表类型
    └── ...
```

## 配色方案

### PALETTE

```python
PALETTE = {
    "blue_main":      "#0F4D92",
    "blue_secondary": "#3775BA",
    "green_3": "#8BCF8B",
    "red_strong": "#B64342",
    "neutral_light": "#CFCECE",
    "neutral_mid":   "#767676",
    "neutral_dark":  "#4D4D4D",
    "teal":   "#42949E",
    "violet": "#9A4D8E",
}
```

### PALETTE_NMI_PASTEL

```python
PALETTE_NMI_PASTEL = {
    "baseline_dark": "#484878",
    "baseline_mid":  "#7884B4",
    "baseline_soft": "#B4C0E4",
    "ours_tiny":  "#E4E4F0",
    "ours_base":  "#E4CCD8",
    "ours_large": "#F0C0CC",
}
```

## 图表类型

- 分组柱状图
- 趋势图
- 热图
- 森林图
- 雷达图
- 散点图
- 多面板图

## 许可证

Apache-2.0 License