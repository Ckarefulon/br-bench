# br-bench（已废弃）

这个仓库是 **Build-Runner 性能基准测试**的临时项目，用于测量云端构建各阶段耗时。

## 测量结论（已写入正式文档）

一次 Gradle 构建的端到端耗时分解：

| 阶段 | 优化前 | 优化后 |
|---|---|---|
| Environment 工具探测 | 29s | **5s** |
| 缓存下载/解包 | 16s（601 MB） | **3s**（137 MB） |
| 实际命令执行 | 10s | 10s |
| **AI 实际等待** | **96.6s** | **45.7s** |

结论与优化手法见：
- [Build-Runner](https://github.com/Ckarefulon/Build-Runner)（引擎侧改动）
- [Build-Runner-MCP](https://github.com/Ckarefulon/Build-Runner-MCP)（客户端轮询改动）

## 说明

本仓库可以安全删除。删除需要 `delete_repo` 权限：

```bash
gh auth refresh -h github.com -s delete_repo
gh repo delete Ckarefulon/br-bench --yes
```

保留着也不会影响任何东西——Build-Runner 引擎通过 workflow 参数指定目标仓库，
不会因为这个仓库存在与否而改变行为。
