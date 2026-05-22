# CC-Benchmark — Claude Code Agentic Benchmark

**EN** | A benchmark for evaluating AI models on real-world agentic engineering tasks. Not a coding quiz — a test of whether a model can actually drive a multi-step engineering workflow.

**ZH** | 面向真实 agentic 工程任务的 AI 模型评测基准。测的不是"能不能写出正确代码"，而是"能否驾驭真实多步工程工作流"。

---

## What Is This / 项目简介

**EN**

CC-Benchmark (Claude Code Agentic Benchmark) measures how well AI models perform on authentic agentic engineering tasks — the kind that arise in real software development when using an AI coding agent like Claude Code.

Existing benchmarks like HumanEval test isolated code generation correctness. SWE-bench tests patch application on GitHub issues. CC-Benchmark tests something different: given a realistic engineering scenario, can a model select the right tools, maintain context across a long session, recover from errors, follow project-specific conventions, and deliver a coherent, high-quality output?

Tasks are executed in `cc_one_shot` mode: each task runs as a single, fully autonomous session with no human intervention.

**ZH**

CC-Benchmark（Claude Code Agentic Benchmark）测量 AI 模型在真实 agentic 工程任务上的表现——这类任务来自在 Claude Code 等 AI 编程 Agent 实际使用场景中遇到的真实问题。

HumanEval 等现有基准测试的是孤立的代码生成正确性；SWE-bench 测试的是对 GitHub issue 的 patch 应用。CC-Benchmark 测的是另一件事：面对真实工程场景，模型能否选择正确工具、在长会话中保持上下文、从错误中恢复、遵循项目约定，并交付连贯且高质量的输出？

所有任务以 `cc_one_shot` 模式执行：每个任务作为一次完全自主的会话运行，无任何人工干预。

---

## Leaderboard / 排行榜

> Data is being compiled. Scores reflect weighted totals (Capability x 0.7 + CES x 0.3).
>
> 数据整理中。分数为加权总分（能力分 x 0.7 + CES x 0.3）。

| Rank | Model | Capability Score | CES | Weighted Total |
|------|-------|-----------------|-----|----------------|
| 1 | — | — | — | — |
| 2 | — | — | — | — |
| 3 | — | — | — | — |
| 4 | — | — | — | — |
| 5 | — | — | — | — |
| 6 | — | — | — | — |
| 7 | — | — | — | — |
| 8 | — | — | — | — |

Models evaluated: MiniMax M2.7, DeepSeek V4 Pro, Claude Sonnet 4.6 (baseline), Qwen3.6-Plus, Xiaomi Mimo v2.5 Pro, GLM 5.1, Xiaomi Mimo v2.5, Kimi for Coding

---

## Methodology / 方法论

### Evaluation Dimensions / 评测维度

**EN**

Six dimensions are scored per task. Each dimension is scored 0–10 and weighted into a composite capability score.

**ZH**

每个任务按六个维度评分，每个维度满分 10 分，加权合并为能力分。

| Code | Dimension | Weight | Description / 说明 |
|------|-----------|--------|---------------------|
| TC | Tool Call Accuracy / 工具调用正确率 | 20% | Whether the right tools are called with correct parameters / 工具选择与参数是否正确 |
| CP | Task Completion / 任务完成度 | 25% | Whether the task objective is fully met / 任务目标是否完整达成 |
| FI | Faithfulness / 输出忠实度 | 15% | Whether output matches instructions without hallucination / 输出是否忠实于指令，无幻觉 |
| ER | Error Recovery / 错误恢复 | 15% | Whether the model detects and recovers from tool errors or bad state / 是否能识别并从错误中恢复 |
| QU | Output Quality / 输出质量 | 15% | Readability, structure, and correctness of artifacts produced / 产出物的可读性、结构性与正确性 |
| CT | Context Tracking / 上下文保持 | 10% | Whether the model maintains coherent state across a long session / 长会话中上下文状态是否连贯 |

---

### Test Stages and Tasks / 测试阶段与任务体系

**EN**

Tasks are organized into 9 stages (T0–T8) grouped under 3 broader stages. Each stage has a weight in the final capability score.

**ZH**

任务按 T0–T8 共 9 个阶段组织，分属 3 个大 Stage。每个阶段在能力分中有对应权重。

#### Stage 1 — Foundational LLM Capability / 基础 LLM 能力（35%）

| Task | Weight | Focus / 考察重点 |
|------|--------|-----------------|
| T0 | 5% | Basic tool execution: single-tool trigger, chained calls, error handling / 基础工具执行：单工具触发、链式调用、错误处理 |
| T1 | 10% | Understanding and reasoning: cross-document contradiction detection, dependency analysis, architectural coherence / 理解与推理：跨文档矛盾识别、依赖分析、架构自洽性 |
| T2 | 10% | Code writing: style consistency, class extension, error-handling patterns / 代码编写：风格一致性、类扩展、错误处理模式 |

#### Stage 2 — Claude Code Support Capability / CC 支持能力（15%）

| Task | Weight | Focus / 考察重点 |
|------|--------|-----------------|
| T3 | 10% | Context management: long-context recall, CLAUDE.md compliance / 上下文管理：长上下文召回、CLAUDE.md 遵从 |
| T4 | 5% | CC CLI fundamentals: skill execution, pipeline steps, schema output / CC CLI 基础：skill 执行、pipeline 步骤、schema 输出 |

#### Stage 3 — Engineering Synthesis / 工程综合能力（50%）

| Task | Weight | Focus / 考察重点 |
|------|--------|-----------------|
| T5 | 10% | Files and scripts: multi-step file operations, Git workflow, data processing / 文件与脚本：多步文件操作、Git 工作流、数据处理 |
| T6 | 15% | Analysis and synthesis: code review, multi-document synthesis, data insight / 分析与综合：代码 review、多文档综合、数据洞察 |
| T7 | 15% | Complex orchestration: skill auditing, cross-skill coordination, multi-phase tasks / 复杂编排：skill 审查、跨 skill 编排、多阶段任务 |
| T8 | 20% | PM engineering: backlog prioritization, sprint planning, architecture proposals / PM 工程化：Backlog 优先级、Sprint 计划、架构提案 |

---

### Scoring System / 评分体系

**EN**

Each model receives two scores:

1. **Capability Score** (0–10): Weighted average of the six dimension scores across all tasks, scaled by task-stage weights.

2. **Cost Efficiency Score (CES)** (0–10): Measures token economy relative to the baseline model (Claude Sonnet 4.6). Lower token consumption yields a higher CES. A model spending the same tokens as the baseline scores 5.0; spending half scores proportionally higher; spending double scores proportionally lower.

3. **Weighted Total** = Capability Score x 0.7 + CES x 0.3

**ZH**

每个模型得到两项分数：

1. **能力分**（0–10）：六个维度得分按任务阶段权重加权平均，满分 10。

2. **成本效率分（CES）**（0–10）：衡量相对于基线模型（Claude Sonnet 4.6）的 Token 消耗效率。Token 消耗越低分越高；与基线消耗相同得 5.0 分；消耗减半则得分按比例更高；消耗翻倍则得分更低。

3. **加权总分** = 能力分 x 0.7 + CES x 0.3

---

## Data and Dashboard / 数据与看板

**EN**

All raw scores, per-task breakdowns, and case definitions are stored under `benchmark/`:

```
benchmark/
  cases/          # Task case definitions (T0-T8)
  scores/         # Raw scoring results per model per task
  reports/        # Aggregated scorecard reports
  scripts/        # Scoring and aggregation scripts
  public/         # This README and any published outputs
```

To view aggregated results, run the scorecard script:

```bash
python benchmark/scripts/scorecard.py
```

**ZH**

所有原始评分、逐任务明细及 case 定义存储在 `benchmark/` 目录下：

```
benchmark/
  cases/          # 任务 case 定义（T0-T8）
  scores/         # 各模型各任务原始评分
  reports/        # 汇总 scorecard 报告
  scripts/        # 评分与汇总脚本
  public/         # 本 README 及已发布输出
```

查看汇总结果：

```bash
python benchmark/scripts/scorecard.py
```

---

## Disclaimer / 声明

**EN**

CC-Benchmark is designed around real agentic engineering tasks encountered during Claude Code usage. It is not a general-purpose coding benchmark and does not claim to measure general reasoning or language ability.

Results are specific to the task set, execution environment, and model versions tested. Scores may change as the task set evolves or as model APIs are updated. All model versions are logged at time of evaluation.

This benchmark does not rank general model intelligence. A model that scores well here is specifically capable at agentic engineering workflows as defined by this task set.

**ZH**

CC-Benchmark 围绕 Claude Code 使用过程中真实遇到的 agentic 工程任务设计，不是通用编程基准，也不声称衡量通用推理或语言能力。

结果仅适用于本任务集、执行环境和所测模型版本。随着任务集演进或模型 API 更新，分数可能变化。所有模型版本在评测时均已记录。

本基准不对模型的通用智能进行排名。在此得分较高，仅代表该模型在本任务集所定义的 agentic 工程工作流上具有较强能力。

---

*Last updated: 2026-05-22*
