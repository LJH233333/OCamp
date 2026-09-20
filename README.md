# OCamp —— 把 OpenCode 装进安卓 App（OC + 内置 Linux）

> **项目名 / App 名：`OCamp`**（读作「OC 营地」）。`OC` = OpenCode，`camp` = 营地/基地——手机端是"你的营地"（自带 OpenCode + Linux，能独立干活），从这里还能连线电脑端那支"大部队"；也甩掉了旧名 `OConnector`（"远程连接器"）不再准确的含义。
>
> 2026-09-20 从 `daily-assistant` 拆出的**独立项目**。与"陪伴型 Agent"项目无关，本目录只做**嵌入**这件事。

## 目标

把**原生 OpenCode**（MIT）连同**最小 Linux 运行环境**嵌进安卓 App，作为 App 自带的一个进程：**跟随 App 启停**；App 上用**浮窗前端**与它交互。同时 App 仍可用 HTTP 连电脑端 OpenCode（开发团队用）。两条并行、互不干扰。

## 范围（边界）

- **做**：嵌入 OpenCode + 最小运行环境、子进程启停、静默更新、浮窗对接；无障碍作为后续能力。
- **不做**：长记忆、人设、陪伴逻辑——那些在 `daily-assistant`。
- 不依赖 adb / root。

## 结构

```
App（OCamp；基座：OConnector-Pro）
├─ 浮窗前端            ← 与内置 OpenCode 交互
├─ 子进程守护          ← App 起即拉起，App 关即退出
├─ 更新器              ← 查/下/校验/替换/重启/回滚
└─ 私有目录（内置 Linux 盒子）
   ├─ 最小 Linux 工具（sh/bash/coreutils…）
   └─ opencode 二进制
```

## 状态

- 2026-09-20：评估完成，设计基本闭环。**未开工。**
- 唯一未定：浮窗与内置 OpenCode 的**通信方式**（本机 HTTP vs ACP/stdio）——见 `设计定案.md`。

## 关键路径 / 参考

| 项 | 值 |
|---|---|
| 更新源（OpenCode 安卓包） | `Hope2333/opencode-termux`（MIT，aarch64 包） |
| App（OCamp）基座 | `LJH233333/OConnector-Pro`（私有仓库；OCamp 在其上改造） |
| 旧内嵌实验（已停） | 仓库 `LJH233333/termux-assistant`、本地 `workspace/termux-app` |
| OpenCode 源码沙箱（共享） | `~/daily-assistant/workspace/opencode-src` |
| 安卓二进制参考 | `~/opencode-1.17.9-android-aarch64.zip` |

## 文档

- `README.md` —— 本文件（公开，进仓库）。
- `AGENTS.md` —— 项目规范 / 铁律（**内部文档，仅本地，不进公开仓库**）。
- `设计定案.md` —— 本项目的决定（**内部**）。
- `优化清单.md` —— 未完成/在办项（**内部**）。
- `评估-嵌入与无障碍.md` —— 能力清单 / 硬边界 / 技术事实（**内部**）。
