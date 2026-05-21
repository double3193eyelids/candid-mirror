<div align="center">

# 🪞 魏征 · Candid Mirror

**以Agent为镜，可以知得失。**

> A candid mirror for your AI agent usage — see your patterns, know your gains and losses.

[![Status](https://img.shields.io/badge/status-beta-orange)](https://github.com/your-org/candid-mirror)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.5.5-blue)](./candid-mirror/SKILL.md)

</div>

---

## 🎯 一句话介绍

**中文**：魏征读取你的 Agent 会话日志，分析使用模式，识别效率瓶颈，给出可执行的优化建议——一面直言不讳的镜子，帮你看得更清楚。

**English**: Candid Mirror reads your AI agent session logs, analyzes usage patterns, spots efficiency bottlenecks, and gives actionable optimization advice — a candid mirror to help you see more clearly.

---

## ✨ 功能亮点

- 🔍 **自动行为扫描** — 读取 OpenClaw 会话日志，7 天数据一键复盘，零配置开箱即用
- ⚠️ **智能预警检测** — 超级会话、高频短会话、深夜作业、副智能体闲置等 7 类硬信号预警
- 💡 **可执行建议** — 每条建议附带数据证据 + 因果诊断 + 具体动作，不说正确的废话
- 🪞 **魏征口吻** — 自称"臣"称你"陛下"，预警和建议用古文节奏进谏，数据表格保持严谨
- 📈 **基线追踪** — 自动记录历史基线，每周对比变化趋势，建议采纳状态全程追踪

---

## 📄 示例报告

> 以下为脱敏示例，真实报告会使用你的智能体名和项目名。

<details>
<summary>📖 点击展开示例报告</summary>

```markdown
🪞 魏征日报 · 2026-05-20
以智能体为镜,可以知得失。基于你最近 7 天的使用数据(排除1天无使用日期)。

📊 一眼看过去：会话数30，消息总数207，涉及4个智能体，
   核心时段18:00-20:00(39%)，平均改轮次6.9

🔧 工具Top5：写入文件2454、执行命令307、读取文件206、编辑43、网页抓取15
   写读比11.9:1，排除超级会话后0.36:1

🤖 智能体分布：Agent-A(主力) 21会话167消息、Agent-B 6会话7消息、
   Agent-C 2会话32消息、Agent-D 1会话1消息

⚠️ 预警：超级会话(100轮98.7h)、高频短会话(10个1轮子智能体)、
   副智能体闲置、深夜作业

💡 建议：超级会话防线升级、写读比基线修正、副智能体收尾

💬 金句："排除一个98.7小时的超级会话后,正常会话的写入反而少于读取。
   问题不在习惯,在那个不肯关闭的长会话。"
```

完整报告见 [`examples/example-report.md`](examples/example-report.md)

</details>

---

## 📦 安装

### 方式一：手动安装（OpenClaw / QClaw）

```bash
# 克隆仓库
git clone https://github.com/your-org/candid-mirror.git

# 复制到技能目录
cp -r candid-mirror/ ~/.openclaw/workspace/skills/candid-mirror/
```

### 方式二：SkillHub 安装

```bash
npx skills add candid-mirror
```

### 方式三：OpenClaw CLI

```bash
npx openclaw skill add candid-mirror
```

> 💡 其他平台（Claude Code、Codex、Hermes）的适配路径已写入 SKILL.md，但**未经实测验证**，欢迎提 PR 补充。

---

## 🚀 使用方式

安装后，**打开一个新的干净对话**，说：

> **"帮我复盘"**

即可体验完整报告。建议立即试一次！🪞

其他触发词：
- 中文：`分析我的使用习惯` / `我的AI用法有什么问题` / `优化我的AI工作流`
- English：`review my AI usage` / `weekly review` / `agent analytics`

> ⚠️ 建议在新的干净对话中触发，长对话的上下文重复读取会大幅增加字符量消耗。

首次运行时，魏征会用 2-3 个问题校准你的画像（你用 Agent 主要干嘛？每天用多久？），后续分析据此调整建议权重。

---

## 🤖 推荐模型

| 模型 | 推荐度 | 说明 |
|------|--------|------|
| **DeepSeek** | ⭐⭐⭐⭐⭐ | **最佳选择**。成本仅 ¥0.47/次，指令遵循能力强，中文输出稳定 |
| GLM-5 | ⭐⭐⭐ | 可用，但指令遵循偶有偏差，部分预警可能遗漏 |
| 混元 / Kimi | ⭐ | 不推荐。SKILL.md 较长（700+行），低端模型容易出现指令遗漏或截断 |

> 💡 魏征的 SKILL.md 包含详细的步骤定义、红线规则和报告模板，对模型的指令遵循能力有较高要求。模型越强，报告越准确。

---

## ⚙️ 配置说明

魏征使用 `candid-mirror.yaml` 存储用户画像、偏好、基线和建议追踪。

首次运行自动创建，无需手动编辑。主要区域：

| 区域 | 作用 | 更新方式 |
|------|------|----------|
| `profile` | 用户画像（目的、深度、风格） | 首次校准 + 后续确认更新 |
| `preferences` | 报告偏好（格式、预警级别、措辞风格） | 用户对话中修改 |
| `baselines` | 历史基线（上次运行、周均指标） | 每次运行自动更新 |
| `suggestions` | 建议追踪（历史建议 + 采纳状态） | 每次运行自动追加 |
| `guard` | 守卫规则阈值（深会话轮次、深夜时段等） | 用户对话中调整 |

详见 [`candid-mirror.yaml.example`](candid-mirror.yaml.example)。

---

## 📁 目录结构

```
candid-mirror/
├── SKILL.md                    # 核心指令文件（V5.5）
├── tips.md                     # Tips 知识库（20条，按画像×场景匹配）
├── candid-mirror.yaml          # 用户配置（含个人数据，已 gitignore）
├── candid-mirror.yaml.example  # 配置模板
├── .gitignore                  # 排除含个人数据的文件
├── README.md                   # 本文件
├── LICENSE                     # MIT
└── examples/
    └── example-report.md       # 脱敏示例报告
```

---

## 🔴 红线规则

| # | 规则 | 说明 |
|---|------|------|
| R1 | **不编数据** | 没有数据就说"数据不足"，绝不虚构指标（违反则报告作废） |
| R2 | **不输出对话原文** | 只输出统计、模式、脱敏摘要（违反则隐私泄露） |
| R3 | **不修改用户数据** | 全程只读（yaml 配置文件除外，见 Step 8） |
| R4 | **不联网** | 不调用任何外部 API |
| R5 | **不依赖特定脚本** | 仅说明要提取什么数据，AI 用当前环境可用工具提取 |
| R6 | **只用扫描数据** | 智能体列表、会话数据必须且只能从目录扫描结果生成，禁止推断补充 |
| R7 | **中文优先** | 所有输出中文，专业术语首次出现配英文括号 |
| R8 | **时区本地化** | 所有日期时间转为本地时区（默认 Asia/Shanghai UTC+8） |
| R9 | **禁止泄露执行过程** | 报告前后均不得展示任何内部步骤 |

---

## 🏷️ 状态

**Beta** — 已在 OpenClaw/QClaw 平台实测验证，Claude Code/Codex/Hermes 路径写入但未验证。欢迎其他平台用户测试反馈。

## 📜 License

[MIT](LICENSE)

---

<div align="center">

**以Agent为镜，可以知得失。**

*Your AI usage patterns are a mirror — look into it, and you'll see what's working and what's not.*

</div>
