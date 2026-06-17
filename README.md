# math-reference-read

数学/经济学学术文献 PDF 智能解析与三方视角审阅分析 Skill，专为数学、统计学、经济学、计量经济学、金融学等定量研究类学术 PDF 设计。

## 特性

- **三方视角**：研究生视角（学习理解）、导师视角（指导评估）、审稿人视角（同行评审）
- **智能 PDF 解析**：基于 MinerU SDK，支持数学公式和表格识别
- **结构化输出**：自动生成符合学术规范的审阅报告
- **日用量跟踪**：自动记录 API 使用量，便于配额管理

## 快速开始

### 前置条件

- Python 3.8+
- MinerU SDK（`pip install mineru-open-sdk`）
- MinerU API Token（[获取地址](https://mineru.net/apiManage/token)）

### 配置

```bash
# 1. 安装依赖
pip install mineru-open-sdk

# 2. 创建配置目录
mkdir -p ~/.mineru

# 3. 配置 API Token
echo "token: '你的API密钥'" > ~/.mineru/config.yaml
```

### 使用方法

```bash
# 研究生视角（默认）
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output

# 导师视角
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output --perspective advisor

# 审稿人视角
python scripts/math_pdf_extract.py "paper.pdf" --output-dir ./output --perspective reviewer
```

## 使用场景

| 场景 | 推荐视角 | 说明 |
|------|---------|------|
| 课程作业 | 研究生视角 | 理解论文的模型推导和实证方法 |
| 文献综述 | 研究生视角 | 系统梳理理论框架和研究空白 |
| 指导学生 | 导师视角 | 评估文献价值和学生匹配度 |
| 选题参考 | 导师视角 | 判断研究方向的可行性和创新性 |
| 期刊审稿 | 审稿人视角 | 评估方法论严谨性和结论可靠性 |
| 论文评阅 | 审稿人视角 | 专业评判识别假设和因果推断 |

## 输出示例

### 研究生视角输出

```markdown
# [文献标题]
> 📖 **分析身份：研究生视角** — 以学习理解为导向
> **领域标签**：[数学 / 经济学 / 计量经济学 / 金融学 / 统计学]

## 一、摘要（Abstract）
## 二、文献综述（Literature Review）
## 三、研究问题（Research Questions）
## 四、研究方法（Research Methods）
## 五、研究结果（Research Results）
## 六、讨论与评价
## 七、关键公式与概念
```

### 导师视角输出

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

### 审稿人视角输出

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

## 身份切换

| 命令 | 视角 |
|------|------|
| 默认（无关键词） | 研究生视角 |
| 包含 `导师`/`advisor`/`导师视角` | 导师视角 |
| 包含 `审稿人`/`reviewer`/`审稿` | 审稿人视角 |
| 包含 `三方`/`全部`/`三种` | 三方视角（依次输出三份） |

## 脚本参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--output-dir` | `./math-output` | 输出目录 |
| `--model` | `vlm` | 模型版本：`pipeline` / `vlm` / `html` |
| `--ocr` | 关闭 | 对扫描件启用 OCR |
| `--language` | `en` | 文档语言（`en`=英文，`ch`=中文） |
| `--no-formula` | 开启公式识别 | 禁用公式识别 |
| `--no-table` | 开启表格识别 | 禁用表格识别 |
| `--pages` | 全部 | 页码范围，如 `"1-10,15"` |

## 文件结构

```
math-reference-read/
├── README.md              # 本文件
├── SKILL.md               # Skill 主文档
├── daily_usage.json       # 日用量记录
└── scripts/
    └── math_pdf_extract.py  # PDF 提取脚本
```

## API 限制

- 单文件 ≤ 200MB，≤ 600 页
- 免费版日限额：2000 页
- 上传链接有效期：24 小时
- 解析结果保存：30 天

## Windows 用户注意

如果遇到 GBK 编码错误，在命令前加 `PYTHONIOENCODING=utf-8`：

```bash
PYTHONIOENCODING=utf-8 python scripts/math_pdf_extract.py "paper.pdf"
```

## 许可证

MIT License
