# 怎么让每个 AI 都读到这个库

先说清楚一件事：**没有任何标准能让 ChatGPT、Claude、Gemini 自动共享你的私人记忆。** 各家的「记忆」是彼此隔离的。

能做的只有一件事：**你维护一份主库，然后给每个 AI 一条它能走通的路。** GitHub 公开仓库的好处是——这条路对几乎所有 AI 都是通的，只是走法不同。

---

## 路线一：零配置，一次一句话（推荐起步）

公开仓库的每个文件都有一个 raw 地址：

```
https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/card.md
```

在任何能联网的 AI 里，把这句话放在问题前面：

> 先读这个链接，按里面的约定来回答我下面的问题：
> https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/card.md

通用于：ChatGPT（联网模式）、Claude（联网）、Gemini、Kimi、豆包、DeepSeek、Grok、Perplexity、以及任何有 WebFetch 能力的 agent。

**这一步 30 秒就能做完，先做这个。**

---

## 路线二：写进各家的「记忆」（一劳永逸）

| 平台 | 放在哪 | 放什么 |
| --- | --- | --- |
| ChatGPT | 设置 → 个性化 → 自定义指令 | `card.md` 全文 |
| ChatGPT Projects | 项目 → 添加文件 | `card.md` + `context/*` |
| Claude | Settings → Profile → 个人偏好 | `card.md` 全文 |
| Claude Projects | 项目 → Project knowledge | 整个仓库打包上传 |
| Gemini | 设置 → 已保存的信息 / Gem 指令 | `card.md` 全文 |
| 豆包 / Kimi / DeepSeek | 各自的「我的信息 / 记忆」入口 | `card.md` 全文 |
| Cursor | Settings → Rules → User Rules | `card.md` 全文 |

关键：**放 `card.md`，不要放整个仓库。** 自定义指令有长度上限，塞多了会被截断，反而更差。细节让 AI 需要时再去读链接。

### 长度不够时怎么拆

`card.md` 现在约 1950 字符，ChatGPT 自定义指令每个框上限 1500 字符，需要拆成两个框：

- **「你想让 ChatGPT 了解你什么」** ← 放 `## 我是谁` + `## 怎么回答我`
- **「你希望 ChatGPT 如何回复」** ← 放 `## 什么时候才允许生成文件` 到结尾（含论文格式规范与技术红线）

Claude 的 Profile 偏好、Gemini 的 Gem 指令可以直接整份粘。如果哪个平台还是装不下，**优先砍论文格式那一节，改成让它读 `context/50-doc-format.md` 的链接** —— 那本来就是按需加载的内容。

---

## 路线三：代码类工具自动继承

这些工具会自动读仓库根目录的约定文件，不需要你做任何事：

| 工具 | 认的文件 |
| --- | --- |
| Claude Code | `CLAUDE.md` |
| Codex / Cursor / Copilot / Windsurf / Amp | `AGENTS.md` |

**真正省事的用法**：在**每**一个新项目里放一个只有一行的 `AGENTS.md`：

```markdown
我的个人上下文：https://github.com/howingtonliter683-max/ai-profile
动手前先读 card.md，读完再干活。
```

这样每个新项目都自动继承你的画像，不用重新调教。

---

## 路线四：MCP（更彻底，但配置成本高）

如果你用 Claude Desktop、Cursor、WorkBuddy 这类支持 MCP 的客户端，可以挂一个 GitHub MCP server，让它直接读私有/公开仓库，而不是靠粘贴。

适合：仓库内容多、需要按需检索而不是每次全量塞进上下文的情况。
不适合：还没跑通路线一的时候折腾这个。

---

## 建议的落地顺序

1. 今天：把 `card.md` 填完，丢进 ChatGPT 和 Claude 的自定义指令。（20 分钟，收益最大）
2. 本周：在任何常用项目里加一行 `AGENTS.md` 指过来。
3. 长期：每次被 AI 惹毛、或纠正了它一次，就回这个仓库加一条。**库是靠摩擦长出来的，不是靠一次性写完。**

---

## 三条可直接复制的开场白

放在任何一个 AI 的对话框第一句，后面接你的实际问题。

**问 RFIC 概念**

```
先读 https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/card.md
然后：<你的问题>
```

**让它生成学位论文格式的文档**

```
先读下面两份，再按里面的格式规则给我生成 Word：
https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/card.md
https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/context/50-doc-format.md
内容：<你的正文或要求>
要求：公式必须是 Word 原生公式（OMML），生成后逐条对照 50-doc-format.md 的自检清单。
```

**让它写网页或后端**

```
先读下面两份：
https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/card.md
https://raw.githubusercontent.com/howingtonliter683-max/ai-profile/main/context/60-delivery.md
做一个 <你想要的页面>。交付时给出本地运行命令和上线步骤。
```
