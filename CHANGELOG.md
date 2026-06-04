# 更新日志

本项目变更记录。格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [Unreleased]

### Added
- 开源配置：MIT `LICENSE`、`CONTRIBUTING.md`、issue / PR 模板
- `examples/sample-comment-service/`：占位符全部填好的参考样例（评论生成服务）
- README 首屏：适用 / 不适用场景、badge、更明确的 tagline

### Changed
- README「参考实现」一节指向 `examples/`

### Fixed
- evals 占位目录改用合法名（`example-scenario-a/b`），去掉路径中的尖括号，兼容 Windows
- 补 `docs/prd/README.md` 目录说明（此前 `CLAUDE.md` 引用该目录但实际缺失）

### Removed

---

> 维护说明：
> - 每完成一个 TASKS.md 任务，在 `[Unreleased]` 下追加一条 `### Added/Changed/Fixed`
> - 发布版本时，把 `[Unreleased]` 改成 `[X.Y.Z] - YYYY-MM-DD`，重新开一个 `[Unreleased]`
