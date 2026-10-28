# 🛡️ DSH-Guardian (DeepSeek Harness 智能体纪律守则与防死循环全能增强套件)

<p align="center">
  <img src="https://img.shields.io/badge/DSH-Compatible-blue?style=for-the-badge&logo=deepseek" alt="DSH" />
  <img src="https://img.shields.io/badge/Codex%2B%2B-Supported-brightgreen?style=for-the-badge" alt="Codex" />
  <img src="https://img.shields.io/badge/WorkBuddy-Ready-orange?style=for-the-badge" alt="WorkBuddy" />
  <img src="https://img.shields.io/badge/Token_Saver-99%25-red?style=for-the-badge" alt="Save Token" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge" alt="License" />
</p>

> **一键终结 AI 智能体在后台无脑转圈、盲目写测速探针、踩中语法报错无限重试与狂烧百万 Token 的世纪顽疾！**  
> 专为 DeepSeek Harness (DSH)、Codex++、WorkBuddy 及多 Agent 生产级环境打造的标准化行为规范与工程防御套件。

---

## 💥 痛点背景：你的 Agent 为什么动不动就在“无脑烧 Token”？

在长期的 Agentic AI 落地实战中，几乎所有开发者都踩过这些致命大坑：
1. **执行过载（Over-Action Bias）**：
   你本想询问“*为什么网络变慢了/怎么拉起服务*”，拥有命令行权限的 Agent 却自作主张把它当成 Engineering Task，在后台徒手编写 Python 多线程测速脚本、盲目建立几百个 TCP 连接去挨个 ping，**整整自嗨 10 多分钟，白白烧掉几百万 Token**；
2. **报错自愈死循环 (Self-healing Loop Trap)**：
   脚本在 Windows PowerShell 中因为管道符或引号触发语法报错，Agent 的“自动改错机制”被无限激发：*报错 ➔ 改代码 ➔ 再报错 ➔ 再改再测*，单轮暴走狂跑近百步，主线程完全卡死，用户中途插话根本插不进去！
3. **超长历史上下文诅咒 (Context Overhang)**：
   会话累积了上千条历史记录（几十万 Token），模型背负巨大包袱，陷入代码完美主义强迫症，迟迟不给正文回复，最终触发流式超时 `message.stopped` 崩溃。

---

## ⚡ 核心铁律：三大绝对行为红线 (Top Redlines)

针对上述痛点，本项目提炼并固化了**不可逾越的三大绝对死规矩**：

### 1. 咨询与提问类【纯文字优先，严禁动手写脚本】
* 凡是用户询问原理、排查原因、配置方式、操作步骤等咨询类任务：
* **绝对禁止编写 Python/Shell 脚本！绝对禁止在后台发起网络测速、端口扫描或长耗时后台任务！**
* **必须直接用清晰整洁的文字直接正面回答原因与极简手动步骤！**

### 2. 报错立即熔断【严禁自我修复死循环】
* 任何工具调用（命令、写脚本、读写文件）若连续失败 **2 次**，**必须立即强制终止工具调用**！
* 严禁私自反复穷举试探，必须停下来如实向用户呈现报错输出，等待人类决策。

### 3. 单轮步数克制【防暴走烧 Token】
* 单轮任务中连续调用工具不得超过 **5 步**。
* 每完成 2~3 个操作，必须向用户汇报阶段性事实与进展，严禁后台暗箱自跑几十步。

---

## 🎯 业务分工：多 Agent 矩阵量体裁衣

本项目反对粗暴的“一刀切”，针对不同 Agent 的擅长领域，提供了专属细分规范模板：

| 平台 / Agent | 专属角色定位 | 核心优势与职责 | 对应规范文件 |
| :--- | :--- | :--- | :--- |
| **DSH (DeepSeek Harness)** | 全能管家 / 中枢调度 | 严守步数限制、防自嗨跑批、规范分步干活（Plan First） | [`AGENTS.md`](AGENTS.md) |
| **WorkBuddy** | 资深商务办公总监 | 专攻合同协议审校、报价单勾稽强核算、工程图纸规格审查 | [`templates/workbuddy-business-audit.md`](templates/workbuddy-business-audit.md) |
| **Codex / Codex++** | 顶级全栈架构师 | 专攻生产级代码交付、复杂系统排障、跨平台底层攻坚，强制置顶简体中文 | [`templates/codex-engineering-architecture.md`](templates/codex-engineering-architecture.md) |

---

## 🚀 快速使用指南 (Quick Start)

### 方式一：工作区根目录部署（最简单）
直接将本项目根目录下的 **`AGENTS.md`** 复制到你任何项目的根目录下：
```bash
cp AGENTS.md /path/to/your/project/AGENTS.md
```
DSH、Codex、WorkBuddy 启动时会自动扫描工作区根目录并强制载入为最高优先级 System Prompt！

### 方式二：DSH 技能中心安装 (DSH Skill)
1. 打开 DSH Desktop 界面，点击左侧菜单 **【技能中心】 ➔ 【创建】**；
2. 按照本项目 [`docs/DSH_技能创建与操作规范指南.html`](docs/DSH_技能创建与操作规范指南.html) 中的一键复制卡片逐项粘贴；
3. 点击【创建技能】即可实现全局热加载，随时输入 `/disciplined-workflow-guard` 一键唤出护栏！

---

## 📂 项目结构全景 (Repository Tree)

```text
DSH-/
├── README.md                                  # 项目官方开源文档
├── AGENTS.md                                  # 核心通用规范（DSH / Codex / Workbuddy）
├── CLAUDE.md                                  # Claude 体系纯净高能规范
├── skills/
│   └── disciplined-workflow-guard/
│       └── SKILL.md                           # 开箱即用的 DSH 标准技能定义包
├── templates/
│   ├── workbuddy-business-audit.md            # WorkBuddy 商务办公/合同审校专属模板
│   └── codex-engineering-architecture.md      # Codex++ 顶级架构师专属模板
└── docs/
    ├── DSH_技能创建与操作规范指南.html        # 可视化交互 HTML 操作手册 (带一键复制)
    └── 从零到一教会你发布GitHub开源项目实战指南.md # 给新手的开源全流程教程
```

---

## 📖 新手教程：如何维护与发布你自己的 GitHub 仓库？

如果你也是第一次接触开源，我们在文档库中特别为你准备了保姆级指南：
👉 详细阅读：[从零到一教会你发布 GitHub 开源项目实战指南](docs/从零到一教会你发布GitHub开源项目实战指南.md)

---

## 📄 开源许可证 (License)

本项目基于 [MIT License](LICENSE) 开源，欢迎自由使用、分发与二次定制。
让天下没有失控暴走的 Agent！欢迎提 Issue 与 PR 共建！
