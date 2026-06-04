# 当前阶段任务清单 —— comment-service(填写示例)

[English](TASKS.md) | **简体中文**

> 本文件为 `claude-workflow-template` 的填写示例。状态标签里**故意混用** `[x]` / `[~]` / `[ ]`,
> 演示一个推进到一半的项目长什么样。

## 当前进度

> **当前任务**:阶段 3 — 实现接收路由(鉴权 + 字段校验 + 幂等 + 写 RECEIVED + ack)
> **上次更新**:2026-05-20

---

## 阶段 1:项目初始化与开发基础

- [x] 配置依赖管理(uv)
- [x] 配置 lint + 类型检查(ruff + mypy --strict)
- [x] 配置测试框架(pytest,一条 happy path 跑通)
- [x] 创建 `.env.example` + 本地 `.env`(不入 git)
- [x] 实现 settings 加载(含字段校验)
- [x] 实现 structured 日志
- [x] 实现 `GET /health`(不依赖外部)
- [x] 容器化(Dockerfile)
- [x] 完善 README

## 阶段 2:基础数据结构

- [x] 设计任务库 schema(`comment_tasks` + `comment_task_logs`)
- [x] 编写迁移脚本
- [x] 实现任务库连接池
- [x] 实现业务库只读连接池
- [x] DB ping 接入 `GET /health`
- [x] 实现状态机封装的 repository 层
- [x] 探查业务库实际表结构 → 记录到 docs/decisions.md(DECISION-001)

## 阶段 3:核心 API 与状态机骨架

- [x] 实现请求 schema(字段约束 + 控制字符过滤)
- [x] 实现回调 payload schema
- [x] 实现鉴权依赖(静态 Token)
- [x] 实现状态枚举 + 合法转移表 + `transition()` 校验函数
- [~] 实现接收路由:鉴权 + 字段校验 + 幂等检查 + 写 `RECEIVED` + 立即 ack
- [ ] 实现 worker 骨架(RECEIVED → QUERIED → 占位失败)
- [ ] 实现启动恢复(扫 24h 内未完成任务)
- [ ] 单元测试:状态机合法/非法转移、幂等、字段校验

## 阶段 4:业务逻辑模块

- [ ] 实现互动数据查询(只读 SQL,脱敏)
- [ ] worker 接入真实查询,推进到 `QUERIED`
- [ ] 仅查询模式:直接拼装统计结果到 `GENERATED`

## 阶段 5:LLM 调用模块

- [ ] 实现 prompt 模板(system + user 渲染)
- [ ] 实现 LLM SDK 封装 + ephemeral cache + prefill
- [ ] 实现单次超时 + HTTP 5xx 重试
- [ ] 实现输入脱敏校验
- [ ] 实现输出解析 + 解析失败重试
- [ ] 单元测试 + prompt injection 安全测试
- [ ] evals:至少 1 条用例(评论生成合法路径)

## 阶段 6:回调推送模块

- [ ] 实现回调客户端(异步 POST + 超时 + 3 次退避重试)
- [ ] 实现成功 / 失败 payload 拼装
- [ ] 实现 error_msg 分类映射器
- [ ] 单元测试 + 集成测试

## 阶段 7:端到端集成与 evals

- [ ] 端到端用例 11.1 ~ 11.5(见 ACCEPTANCE.md)
- [ ] 性能压测(ack 延迟 / 全链路延迟)
