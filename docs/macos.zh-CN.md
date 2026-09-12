# macOS 使用指南

本文适用于 **macOS + Codex 桌面版**。本 skill 的 Automations 需要在 Codex 桌面版中创建和核对；岗位资料仍写入你打开的工作区。

## 安装、更新和卸载

在 Mac 的 Terminal（zsh）中安装：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/HanjingLaura/precision-recruiter-flow.git ~/.codex/skills/precision-recruiter-flow
```

默认目录是 `~/.codex/skills/precision-recruiter-flow`，也就是 `/Users/<用户名>/.codex/skills/precision-recruiter-flow`。更新时运行：

```bash
git -C ~/.codex/skills/precision-recruiter-flow pull
```

卸载时删除安装目录：

```bash
rm -rf ~/.codex/skills/precision-recruiter-flow
```

删除 skill 不会删除工作区中的岗位资料；岗位资料位于每个工作区的 `.precision-recruiter-local/jobs/`。

## 用 Finder 打开安装目录

在 Finder 按 `Command-Shift-G`（前往文件夹），输入 `~/.codex/skills` 并按回车。也可以在 Terminal 执行 `open ~/.codex/skills`。若看不到 `.codex`，它只是隐藏目录，使用“前往文件夹”仍可直接打开。

## 开新岗位和目录

在 Codex 桌面版打开目标工作区后，说“新岗位：职位名称、地点、薪资和 JD”，或说“使用 `$precision-recruiter-flow` 开一个新岗位”。skill 会在该工作区创建：

```text
.precision-recruiter-local/
└── jobs/
    └── <slug>/
        ├── 01-职位理解.md
        ├── 02-标准简历.md
        ├── 03-候选人-list.md
        ├── 04-电话话术.md
        ├── 05-搜索清单.md
        ├── 06-目标公司-核心人.md
        ├── 07-通话记录.md
        ├── resumes/
        └── reviews/
```

`.precision-recruiter-local/jobs/<slug>/` 是工作区本地数据，和 macOS、Windows 无关；简历、通话记录和复盘不会提交到仓库。

## 在 Codex Desktop Automations 中核对配置

打开 Codex 桌面版的 **Automations** 面板，进入当前工作区，逐项核对以下配置和读写路径：

1. **5 分钟定标杆**：开新岗位并确认职位理解后创建一次性 Automation。它读取 `01-职位理解.md` 和 leader 样板，输出 `02-标准简历.md`。
2. **Sourcing 2 小时**：确认标杆后创建定向 sourcing Automation，运行窗口为 2 小时；它更新 `05-搜索清单.md`、`03-候选人-list.md` 和 `resumes/`，不自动外呼或推客户。
3. **12:00、18:00 复盘**：岗位进行中创建每天两个复盘 Automation，分别检查准人进度、呼出、搜超时以及标杆和职位理解回写，并生成 `reviews/YYYY-MM-DD-HH-复盘.md`。

在每条 Automation 的详情页检查触发时间、工作区、prompt 以及读写文件。若界面没有自动创建按钮，复制 skill 输出的触发、prompt 和读写文件配置，在 Automations 面板手动新建。

## 常见问题

### Skill 没有出现

确认仓库位于 `~/.codex/skills/precision-recruiter-flow`，目录内有 `SKILL.md`；在 Terminal 运行 `git -C ~/.codex/skills/precision-recruiter-flow pull` 后完全退出并重新打开 Codex 桌面版。也要确认打开的是包含 `.precision-recruiter-local/` 的目标工作区。

### 权限或无法写入

确认当前 macOS 用户拥有 `~/.codex` 和目标工作区的读写权限。Finder 中选中文件夹后按 `Command-I` 查看“共享与权限”；必要时把当前用户设为“读与写”。不要用 `sudo` 安装，否则目录可能属于其他用户。

### 路径中有空格

把路径放在引号中，例如：`git -C "$HOME/My Work/.codex/skills/precision-recruiter-flow" pull`。使用 `~` 或 `$HOME` 可避免手写用户名和空格转义问题。

### Mac 上有多个用户名

每个 macOS 用户都有独立的 `/Users/<用户名>/.codex/skills`。请用实际登录用户的 Terminal 安装，并在同一用户的 Codex 桌面版中打开；不要把一个用户的安装目录当作另一个用户的目录。

## 返回根文档和示意图

- [根 README](../README.md)
- [目录树示意图](../references/images/directory-tree.svg)
- [状态机示意图](../references/images/state-machine.svg)
- [Automation 时间线示意图](../references/images/automation-timeline.svg)
