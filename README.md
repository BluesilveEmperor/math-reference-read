# math-reference-read

[English](#english) | 中文

数学/经济学学术文献 PDF 智能解析与三方视角审阅分析 Skill，专为数学、统计学、经济学、计量经济学、金融学等定量研究类学术 PDF 设计。

## 核心特性

- **三方视角审阅**：同一份文献支持三种不同身份视角的深度分析
- **智能 PDF 解析**：基于 MinerU SDK，支持数学公式和表格识别
- **结构化输出**：自动生成符合学术规范的审阅报告
- **日用量跟踪**：自动记录 API 使用量，便于配额管理
- **批量处理**：支持多份 PDF 独立处理，互不干扰

## 快速开始

### 前置条件

- Python 3.8+
- MinerU SDK（`pip install mineru-open-sdk`）
- MinerU API Token（[获取地址](https://mineru.net/apiManage/token)）

### 安装与配置

```bash
# 1. 克隆仓库
git clone https://github.com/BluesilveEmperor/math-reference-read.git
cd math-reference-read

# 2. 安装依赖
pip install mineru-open-sdk

# 3. 创建配置目录
mkdir -p ~/.mineru

# 4. 配置 API Token
echo "token: '你的API密钥'" > ~/.mineru/config.yaml
```

> **注意**：请前往 https://mineru.net/apiManage/token 注册获取 API 密钥。

## 使用方法

### 基本用法

```bash
# 研究生视角（默认）- 适合学习理解
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output

# 导师视角 - 适合指导评估
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output --perspective advisor

# 审稿人视角 - 适合同行评审
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output --perspective reviewer
```

### 三方视角模式

```bash
# 一次输出三份独立报告（研究生视角 + 导师视角 + 审稿人视角）
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output --perspective all
```

### 批量处理多份 PDF

```bash
# 处理多个文件（每份独立处理，各自生成对应报告）
for pdf in papers/*.pdf; do
    python scripts/math_pdf_extract.py "$pdf" --output-dir ./output
done
```

## 三种视角详解

### 1. 研究生视角（默认）

**适用场景**：课程作业、文献综述、开题报告、资格考试、自学理解

**分析重点**：
- 研究背景与问题提炼
- 文献综述与理论框架
- 研究方法详解（模型推导、实证策略）
- 核心发现与数据解读
- 关键公式与概念整理

**输出结构**：
```markdown
# [文献标题]
> 📖 **分析身份：研究生视角** — 以学习理解为导向

## 一、摘要（Abstract）
## 二、文献综述（Literature Review）
## 三、研究问题（Research Questions）
## 四、研究方法（Research Methods）
## 五、研究结果（Research Results）
## 六、讨论与评价
## 七、关键公式与概念
```

### 2. 导师视角

**适用场景**：指导学生选文献、判断文献与学生研究的匹配度、快速判断是否值得精读

**分析重点**：
- 文献学术定位与影响力
- 研究问题与贡献评估
- 方法论难度与先修知识要求
- 结果可信度评估
- 对学生研究的启发与建议

**输出结构**：
```markdown
# [文献标题]
> 🎓 **分析身份：导师视角** — 以指导评估为导向

## 一、文献定位（Literature Positioning）
## 二、研究问题与贡献评估
## 三、方法论评估
## 四、结果可信度评估
## 五、教学与指导建议
## 六、对学生研究的启发
```

### 3. 审稿人视角

**适用场景**：期刊审稿、学位论文评阅、课题评审、质量评估

**分析重点**：
- 总体评价与推荐意见
- 创新性与原创性评估
- 方法论严谨性审查
- 论证逻辑与证据充分性
- 具体修改意见（按重要程度排序）

**输出结构**：
```markdown
# 审稿意见：[文献标题]
> 🎯 **分析身份：审稿人视角** — 以评估评判为导向

## 一、总体评价（Overall Assessment）
## 二、研究问题与创新性评估
## 三、方法论评估
## 四、论证与证据评估
## 五、具体修改意见
## 六、写作与呈现质量
## 七、总结与建议
```

## 使用场景对照表

| 场景 | 推荐视角 | 说明 |
|------|---------|------|
| 课程作业 | 研究生视角 | 理解论文的模型推导和实证方法 |
| 文献综述 | 研究生视角 | 系统梳理理论框架和研究空白 |
| 开题报告 | 研究生视角 | 提取研究方法和关键发现 |
| 指导学生 | 导师视角 | 评估文献价值和学生匹配度 |
| 选题参考 | 导师视角 | 判断研究方向的可行性和创新性 |
| 组会分享 | 导师视角 | 快速评估是否值得精读 |
| 期刊审稿 | 审稿人视角 | 评估方法论严谨性和结论可靠性 |
| 论文评阅 | 审稿人视角 | 专业评判识别假设和因果推断 |
| 课题评审 | 审稿人视角 | 评判研究质量和贡献度 |

## 脚本参数详解

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--output-dir` | `./math-output` | 输出目录 |
| `--model` | `vlm` | 模型版本：`pipeline` / `vlm` / `html` |
| `--ocr` | 关闭 | 对扫描件启用 OCR（增加处理时间） |
| `--language` | `en` | 文档语言：`en`=英文，`ch`=中文 |
| `--no-formula` | 开启公式识别 | 禁用公式识别 |
| `--no-table` | 开启表格识别 | 禁用表格识别 |
| `--pages` | 全部 | 页码范围，如 `"1-10,15"` |
| `--perspective` | `student` | 视角选择：`student` / `advisor` / `reviewer` / `all` |

## 输出文件命名规则

| 视角 | 输出文件名 |
|------|-----------|
| 研究生视角 | `[原PDF文件名]_审阅报告_研究生视角.md` |
| 导师视角 | `[原PDF文件名]_审阅报告_导师视角.md` |
| 审稿人视角 | `[原PDF文件名]_审阅报告_审稿人视角.md` |
| 三方视角 | 三份独立文件分别输出 |

**示例**：
- `high_dimensional_econometrics_审阅报告_研究生视角.md`
- `high_dimensional_econometrics_审阅报告_导师视角.md`
- `high_dimensional_econometrics_审阅报告_审稿人视角.md`

## 核心规则

> ⚠️ **铁律**：一份 PDF → 一个 .md → 一份审阅报告

**严禁将多份 PDF 的内容合并到同一个 `.md` 文件中。** 每份 PDF 必须拥有自己独立的 Markdown 文件和独立的结构化审阅报告。

## 日用量跟踪

每次处理完一份 PDF，脚本会自动报告当日用量：

```
📊 ── 当日 MinerU API 用量 ────────────────────
   已用页数:         12
   剩余可处理页数:    1988（日限额 2000 页）
   已处理文件数:      3
   📌 注: 超出限额后解析优先级会降低，但仍可继续使用
──────────────────────────────────────────────
```

### 配额管理建议

| 操作 | 说明 |
|------|------|
| 查看今日用量 | 直接查看 `daily_usage.json` 文件 |
| 重置统计 | 更换 API Key 时，删除 `daily_usage.json` |
| 超出限额 | 不影响使用，仅优先级下降 |

## API 限制

| 限制项 | 数值 |
|--------|------|
| 单文件大小 | ≤ 200MB |
| 单文件页数 | ≤ 600 页 |
| 日限额（免费版） | 2000 页 |
| 上传链接有效期 | 24 小时 |
| 解析结果保存 | 30 天 |

## Windows 用户注意

如果遇到 GBK 编码错误，在命令前加 `PYTHONIOENCODING=utf-8`：

```bash
PYTHONIOENCODING=utf-8 python scripts/math_pdf_extract.py "paper.pdf"
```

或设置别名持久化：

```bash
# 在 ~/.bashrc 中添加
alias python3="PYTHONIOENCODING=utf-8 python3"
```

## 常见问题

### Q1: 如何获取 MinerU API Token？

1. 访问 https://mineru.net/apiManage/token
2. 注册并登录账号
3. 在 API 管理页面创建并复制 Token

### Q2: 处理扫描件 PDF 时输出乱码怎么办？

启用 OCR 模式：

```bash
python scripts/math_pdf_extract.py "scanned_paper.pdf" --ocr
```

### Q3: 如何处理中文论文？

```bash
python scripts/math_pdf_extract.py "chinese_paper.pdf" --language ch
```

### Q4: 如何只处理特定页码范围？

```bash
python scripts/math_pdf_extract.py "paper.pdf" --pages "1-10,15,20-30"
```

### Q5: 处理时间过长怎么办？

- 检查网络连接
- 确认文件大小不超过 200MB
- 如果是扫描件，可尝试关闭公式/表格识别加速

## 实测性能参考

- 52 页 PDF 转换耗时约 3 分钟（含上传+解析+下载）
- 日用量示例：52/2000 页

## 文件结构

```
math-reference-read/
├── README.md                # 本文件
├── SKILL.md                 # Skill 主文档（详细工作流）
├── LICENSE                  # MIT 许可证
├── daily_usage.json         # 日用量记录（自动生成）
├── scripts/
│   └── math_pdf_extract.py  # PDF 提取脚本
└── skills/
    └── nature-figure/       # 科研绘图技能
        ├── SKILL.md         # 技能路由和工作流
        ├── manifest.yaml    # 配置清单
        ├── README.md        # 技能说明文档
        ├── static/          # 静态资源
        └── references/      # 深度参考文档
```

## 附赠技能：nature-figure 科研绘图

本项目还包含一个独立的 **nature-figure** 技能，用于生成可投稿级科研图，面向 Nature 级期刊和高影响力学术场景。

### 主要特性

- **投稿级科研图工作流**：面向 Nature、Science、Cell 等高影响力期刊
- **Python/R 双后端支持**：matplotlib/seaborn 和 ggplot2/patchwork/ComplexHeatmap
- **图件契约系统**：从核心结论出发，而非直接套模板
- **配色方案**：内置 Nature 风格配色方案，包括 NMI pastel 系列
- **多面板信息结构**：支持复杂的多面板图设计
- **导出格式**：支持 SVG、PDF、TIFF 等投稿级格式

### 快速开始

```bash
# 将技能目录复制到你的 skills 目录
cp -R skills/nature-figure ~/.config/opencode/skills/
```

### 使用示例

```python
import matplotlib as mpl
import matplotlib.pyplot as plt

# 必需设置
plt.rcParams['font.family'] = 'sans-serif'
plt.rcParams['font.sans-serif'] = ['Arial', 'DejaVu Sans', 'Liberation Sans']
plt.rcParams['svg.fonttype'] = 'none'

# 绘图代码...
```

> 详细文档请参考 `skills/nature-figure/README.md`

## 技术架构

```
用户输入 PDF
    ↓
检查 MinerU SDK 配置
    ↓
调用 MinerU API 提取 Markdown
    ↓
根据视角选择审阅框架
    ↓
生成结构化审阅报告
    ↓
报告当日 API 用量
```

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 贡献

欢迎提交 Issue 和 Pull Request！

## 相关链接

- [MinerU 官网](https://mineru.net)
- [MinerU API 文档](https://mineru.net/apiManage/token)
- [GitHub 仓库](https://github.com/BluesilveEmperor/math-reference-read)
- [nature-figure 技能文档](skills/nature-figure/README.md)
- [nature-skills 项目](https://github.com/Yuan1z0825/nature-skills)

---

# English

math-reference-read: Intelligent PDF Analysis & Three-Perspective Review for Academic Literature

## Features

- **Three-Perspective Review**: Student (learning-oriented), Advisor (guidance-oriented), Reviewer (peer-review oriented)
- **Smart PDF Parsing**: Based on MinerU SDK, supports math formulas and tables
- **Structured Output**: Automatically generates academic-standard review reports
- **Daily Usage Tracking**: Auto-records API usage for quota management
- **Nature-figure Skill**: Publication-grade scientific figure generation for Nature/Science/Cell journals

## Quick Start

```bash
# Install
pip install mineru-open-sdk
mkdir -p ~/.mineru
echo "token: 'your-api-key'" > ~/.mineru/config.yaml

# Usage
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output
```

## Nature-figure Skill

This project includes a **nature-figure** skill for generating publication-grade scientific figures:

- **Python/R dual backend support**: matplotlib/seaborn and ggplot2/patchwork/ComplexHeatmap
- **Figure contract system**: Start from core conclusions, not templates
- **Nature-style color schemes**: Including NMI pastel series
- **Multi-panel information structure**: Support for complex figure layouts
- **Export formats**: SVG, PDF, TIFF for publication submission

See `skills/nature-figure/README.md` for detailed documentation.

## License

MIT License

---

**Made with ❤️ for researchers in quantitative fields**
