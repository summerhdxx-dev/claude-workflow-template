# 验收标准 —— comment-service(填写示例)

[English](ACCEPTANCE.md) | **简体中文**

> 本文件为 `claude-workflow-template` 的填写示例,**做了精简**。每条都能用「测试 / 命令 / 人工核对」回答通过与否。

## 1. 验收范围

覆盖 7 个维度:接口、状态机、业务逻辑、LLM、回调、数据安全、端到端,与 `SPEC.md` 对应章节对齐。

## 2. 接口验收

### 2.1 鉴权
- 缺 `X-API-Token` → 401
- Token 错误 → 401
- Token 正确 → 进入字段校验

### 2.2 字段校验

| 字段 | 非法值 | 预期 |
|---|---|---|
| `task_id` | 空 | 400, `字段 task_id 不合法:必填` |
| `post_id` | 0 或负 | 400, `字段 post_id 不合法:必须 > 0` |
| `callback_url` | http(非 https) | 400, `字段 callback_url 不合法:必须 https` |

### 2.3 幂等
同一 `task_id` 第 1 次 200,后续 409(`task already exists`)。

## 3. 状态机验收

| 验收项 | 验证方式 | 通过条件 |
|---|---|---|
| `RECEIVED → QUERIED` | 单元测试 + DB row | 状态更新且日志表写入 |
| `GENERATED → DONE` | 集成测试(mock 回调) | 回调成功后置 DONE |
| 终态不可逆 | 单元测试模拟 `DONE → 任意` | 抛 IllegalTransitionError |
| 跳态拦截 | 单元测试模拟 `RECEIVED → DONE` | 抛 IllegalTransitionError |

- [ ] 状态机所有合法转移均有单元测试覆盖
- [ ] 终态不可逆 + 跳态已自动化拦截
- [ ] 状态日志表与主表字段保持一致

## 5. LLM 调用验收

- [ ] prompt caching 命中率 > 0
- [ ] 输入脱敏校验拒绝含昵称/手机号的 prompt
- [ ] prompt injection 用例(`prompt_hint` 内含「忽略上述指令」)输出仍为合法评论 JSON
- [ ] 输出解析失败重试 1 次后仍失败 → 标 FAILED
- [ ] 调用日志含模型/token/耗时,不含 prompt 全文

## 7. 数据安全验收

- [ ] 凭证不入 git(`git log -p | grep` 0 命中)
- [ ] 凭证不入日志
- [ ] 用户昵称/手机号不入 LLM 调用
- [ ] 业务库账号为只读

## 11. 端到端用例

- 11.1:完整 LLM 路径,断言终态 `DONE`,回调收到 `comment`
- 11.2:业务库不可达 → `FAILED`
- 11.3:LLM 不可达(连续 5xx)→ `FAILED`
- 11.4:重复 `task_id` → 第 1 次 200,后续 409
- 11.5:worker 处理中重启进程 → 启动恢复继续到 `DONE`
