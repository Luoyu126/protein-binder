# 共享文档根

这个目录在 `complexa-post/` 和 `RFD4-Proteina/` **两个仓库之上**，因为后续两条线并行开发，
文档需要同时被两边引用。

```
/home/lilic/yunyi/
├── docs/                 ← 本目录。跨仓库共享，自带 git
├── complexa-post/        ← git 仓库（develop-yunyi）
├── RFD4-Proteina/        ← git 仓库（main）
├── baselines/  slurm-jobs/  rfd4_nodeprobe/
```

## 为什么它自己是一个 git 仓库

**2026-11-20 上午，`complexa-post/docs/` 被整个删空。** 其中 67 个文件被 git 跟踪、从 HEAD
恢复了；**另外 25 个从未提交，git 救不回来，只在这个目录的旧副本里存活** ——
包括 `Research/STATE-OF-EVIDENCE.md`、11-12 的全套 Codex 审计、11-19 的面板选择证据。
另有两个文件（`claude-stability-plan.md`、`claude-weekly-report.md`）的未提交版本也只在这里。

所以这个目录**必须自己有版本控制**，否则它作为唯一副本的那一刻就是单点故障。

## 当前状态（2026-11-20 同步）

内容与 `complexa-post/docs/` 同步，**三处有意不同，这里是权威版**：

| 文件 | 为什么取这里的 |
|---|---|
| `Meetings/11-12/claude-stability-plan.md` | 3,731 行 vs 仓库 2,261 行。仓库那版是 HEAD 恢复的，丢了 1,478 行未提交内容。当天的 "Superseded 2026-11-13" 标注已重新应用到这个全版上 |
| `Meetings/11-12/claude-weekly-report.md` | 592 行的完成版（§2 "ran all 8 rounds"，另有 §2c/2d/2e）。仓库那版是 245 行的 interim 快照，在 complexa-post 的 git 历史里 |
| `Research/README.md` | 带 `STATE-OF-EVIDENCE.md` 的索引行 |

**两边都存在副本，所以会再分叉。** 若要彻底消除这个风险，可以把 `complexa-post/docs`
换成指向 `../docs` 的符号链接 —— 代价是那些内容不再进 complexa-post 的 git 历史。**尚未这么做。**

## 链接约定

docs 现在在仓库之上，所以指向仓库代码的链接要带仓库名：

```markdown
[脚本](../../complexa-post/build_diversity_weights.py)     ✅
[脚本](../../build_diversity_weights.py)                   ❌ 会指到 /home/lilic/yunyi/
```

2026-11-20 的同步已自动重定向了 85 条这类链接。剩 3 条 `file.py:422` 形式的带行号伪链接未修，
它们本来就不是合法的 markdown 链接。

## 目录

| | |
|---|---|
| [`Meetings/`](Meetings/) | 按周的组会记录。本周是 [`Meetings/11-26/`](Meetings/11-26/)，按三个方向分文件夹 |
| [`Research/`](Research/) | 跨周的状态记录。[`Research/STATE-OF-EVIDENCE.md`](Research/STATE-OF-EVIDENCE.md) 是入口 |
| [`Papers/`](Papers/) | 相关论文 |
| 顶层 `*.md` | Complexa 的使用与配置文档（评测指标、推理、训练、sweep 等） |
