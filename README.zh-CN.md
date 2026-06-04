# claude-workflow-template

[English](README.md) | **简体中文**

> 一套与技术栈无关的「AI 协作 + 文档先行」工作流模板,把 AI 从「自由发挥写一堆」约束成「受规则约束、稳定交付可维护 MVP」的开发成员。

[![Release](https://img.shields.io/github/v/release/summerhdxx-dev/claude-workflow-template?color=success)](https://github.com/summerhdxx-dev/claude-workflow-template/releases)
[![Stars](https://img.shields.io/github/stars/summerhdxx-dev/claude-workflow-template)](https://github.com/summerhdxx-dev/claude-workflow-template/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.zh-CN.md)
![Stack agnostic](https://img.shields.io/badge/stack-agnostic-blue.svg)

基于一个真实业务项目的工程实践抽象而成。配合 Claude Code 等 AI 编码工具使用效果最佳,纯人工照此流程推进同样适用。

---

## 适用 / 不适用

**适合**:
- 需求边界容易蔓延、想用「明确不做」挡住范围的项目
- 用 AI 写代码,但受不了它「自由发挥、顺手重构、跳过测试」
- 有严格状态流转 / 对外协议 / 数据安全要求的后端服务
- 想让协作约定、技术决策可追溯的团队

**不适合**:
- 几十行的一次性脚本 / demo(流程开销大于收益)
- 还在探索期、需求每天推翻重来的原型(文档先行会拖慢)

---

## 它是什么

模板提供：
- `CLAUDE.md` — AI 协作工作规则（25 节，§9 / §24 留占位）
- `PROJECT.md` / `SPEC.md` / `TASKS.md` / `ACCEPTANCE.md` — 四件套文档骨架
- `docs/` — 架构 / 接口 / 决策 / 工具 / 运维 / bug 模板
- `evals/` — LLM 评估占位（不调 LLM 可删）
- `CHANGELOG.md` / `.gitignore` — 通用辅助文件

模板**不**提供：源码骨架、依赖管理、Dockerfile、CI 配置 — 这些由具体技术栈决定。

> 中英文说明:每个核心文档都有 `*.md`（英文）与 `*.zh-CN.md`（中文）两个版本。
> 用模板时,**保留你团队使用的语言版本即可,另一份可删**。

---

## 怎么用（5 分钟起步）

### 1. 克隆模板到新项目目录

```bash
git clone --depth=1 https://github.com/summerhdxx-dev/claude-workflow-template.git my-new-project
cd my-new-project
rm -rf .git
git init
```

### 2. 全局搜替换占位符

模板里所有待填位置可一次性 grep 到：

```bash
grep -rni "删除以上示例后填写\|替换为本项目\|DELETE the example above\|REPLACE with your project" .
```

### 3. 按顺序填写四件套（**这是关键 — 不要跳过、不要打乱顺序**）

1. 先写 `PROJECT.zh-CN.md`：项目目标、角色、范围、明确不做、风险（约 20 分钟）
2. 再拆 `TASKS.zh-CN.md` 阶段 1：项目初始化任务（约 10 分钟）
3. 再写 `SPEC.zh-CN.md` §1-§3（总览、范围、核心接口/协议）（约 30 分钟）
4. 再写 `ACCEPTANCE.zh-CN.md` §1（验收范围）+ §2（核心接口验收）（约 10 分钟）
5. 第一次 commit：`docs: 项目初始化文档落盘`

### 4. 按需调整 CLAUDE.md

- **必填**：§9 项目专用规则（数据存储读写权限、敏感字段、专用红线）
- **如调用 LLM**：§24 LLM 调用规则；否则**整节删除**
- **§11 任务状态机**：把 `<INITIAL> / <STAGE_1> / ... / <TERMINAL_OK>` 占位改成本项目实际状态名
- **§12 技术栈红线**：列出本项目允许引入的框架清单
- **§25 文档同步矩阵**：按本项目实际章节号补全表格

### 5. 跑 CLAUDE.md §2 核心执行流程

把 `TASKS.zh-CN.md` 阶段 1 的第一个 `[ ]` 任务交给 AI（或自己），按 `CLAUDE.zh-CN.md §2` 第 1-7 步推进。

---

## 设计哲学

- **文档先行**：先把"要做什么 / 不做什么 / 怎么算完"写清楚，再动代码
- **稳定 > 抽象**：MVP 阶段优先正确性、可维护性、可测试性，不追求架构炫技
- **AI 受约束**：模板给 AI（含 Claude Code）一套强约束，避免"自由发挥写一堆"
- **决策可追溯**：每条非显然取舍写到 `docs/decisions.zh-CN.md`

---

## 参考实现

模板从一个真实业务项目（接收方服务，含外部数据查询 + LLM 调用 + 异步回调）抽象而来。

`examples/sample-comment-service/` 提供了一份**占位符全部填好**的参考样例（评论生成服务），直观展示「模板填完之后长什么样」——四件套怎么写实、状态机/LLM 规则怎么落到具体字段。不知道某一节该填到什么粒度时，去那里看。

---

## 模板自身的版本

参见 `CHANGELOG.md`。模板会随实践持续演进；新项目用了模板后，**不需要**追上模板的后续更新（除非有重大缺陷修复）。
