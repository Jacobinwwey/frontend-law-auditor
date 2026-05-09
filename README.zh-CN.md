# Frontend Law Auditor

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE.txt)
[![Python](https://img.shields.io/badge/python-3.x-blue.svg)](https://www.python.org/)
[![Laws](https://img.shields.io/badge/laws-21-orange.svg)](./rules/_sections.md)
[![Fast Gate Checks](https://img.shields.io/badge/fast_gate_checks-10-purple.svg)](./scripts/law_audit.py)

[English](./README.md) | [中文](./README.zh-CN.md)

---

`frontend-law-auditor` 是一个独立技能仓库，用于将前端 UX 评估转换为可执行、可量化、可门禁的审计流程。它把人因设计法则转成统一检查规则，帮助团队更早发现阻塞点、排序修复优先级，并在 CI 中落实发布阈值。

## 功能特性

- **快速门禁（10 项）**：用于二值化发布检查（触控目标尺寸、反馈延迟、选项密度、进度可见性、校验质量等）。
- **深度法则诊断（21 条）**：覆盖 Fitts、Hick、Gestalt 系列、Von Restorff、Jakob、Miller、Goal-Gradient、Zeigarnik、Tesler、Peak-End、Postel、Doherty、Serial Position、Occam、Parkinson。
- **加权评分模型**：基于 `pass/fail/unknown` 输出并归一化为 0-100 分。
- **可执行修复输出**：失败项自动映射到法则文档，并给出优先级修复方向。
- **CI 严格模式**：存在门禁失败或分数不达标时返回非零退出码。

## 环境要求

- Python 3.x
- 可测量的真实流程证据（如注册、结账、引导流程）

检查 Python：

```bash
python --version
```

## 安装

```bash
git clone https://github.com/Jacobinwwey/frontend-law-auditor.git
cd frontend-law-auditor
```

无需额外安装依赖。审计脚本仅使用 Python 标准库。

## 快速开始

1. 生成证据模板。
2. 使用真实流程数据填写指标。
3. 执行审计并查看报告。
4. 可选：在 CI 中启用严格门禁。

```bash
# 1) 生成模板
python scripts/law_audit.py --init-template ./examples/evidence.local.json

# 2) 在 ./examples/evidence.local.json 中填写测量数据

# 3) 生成审计报告
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --output ./examples/audit.local.md \
  --json-out ./examples/audit.local.json

# 4) 严格门禁（不达标将返回非零退出码）
python scripts/law_audit.py \
  --input ./examples/evidence.local.json \
  --strict \
  --fail-threshold 85
```

## 输出契约

每次审计应输出以下结构：

1. **Fast Gate Failures**：仅列出失败门禁和直接证据。
2. **Law Diagnosis**：按以下结构呈现：
   `Principle -> Observed friction -> Why it happens -> UI change`。
3. **Priority Fix Plan**：按 `P0/P1/P2` 分组。
4. **Recheck Checklist**：下一轮复检必须通过的项。

## 证据模型

输入结构与阈值定义见：
- [references/metrics-schema.md](./references/metrics-schema.md)

理论说明与法则落地指南见：
- [references/theory-playbook.md](./references/theory-playbook.md)
- [rules/_sections.md](./rules/_sections.md)
- `rules/<law>.md`

关键证据缺失时，对应法则会标记为 `unknown`。

## 评分与严格模式

- 法则评分状态：
  - `pass = 1.0`
  - `fail = 0.0`
  - `unknown = 0.4`
- 总分计算：
  - 按权重计算后归一化到 `0-100`
- 严格模式失败条件：
  - 任一快速门禁失败，或
  - 总分低于 `--fail-threshold`（默认 `85`）

## 覆盖法则

- Fitts's Law
- Hick's Law
- Gestalt: Proximity, Similarity, Continuity, Closure, Figure/Ground, Common Fate, Focal Point
- Von Restorff Effect
- Jakob's Law
- Miller's Law
- Goal-Gradient Hypothesis
- Zeigarnik Effect
- Tesler's Law
- Peak-End Rule
- Postel's Law
- Doherty Threshold
- Serial Position Effect
- Occam's Razor
- Parkinson's Law

## 仓库结构

```text
frontend-law-auditor/
|-- SKILL.md
|-- scripts/law_audit.py
|-- examples/evidence.sample.json
|-- references/
|   |-- metrics-schema.md
|   `-- theory-playbook.md
`-- rules/
    |-- _sections.md
    `-- *.md
```

## 贡献说明

- 修改或新增法则/指标时，保持 `scripts/law_audit.py`、`references/metrics-schema.md`、`rules/` 三者一致。
- 优先使用可量化阈值，避免纯主观描述。
- 若评分逻辑有调整，更新示例证据以反映新语义。

## 许可证

MIT License，详见 [LICENSE.txt](./LICENSE.txt)。
