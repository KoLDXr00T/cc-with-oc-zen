# Claude Code × OpenCode Zen API — 跨平台设置指南，无代理、无速率限制、无废话。

> **先看隐私说明：** OpenCode Zen 上的免费模型，或任何其他免费 LLM 提供商，可能会使用你的提示词来改进模型。
> 不要发送敏感代码、凭据或专有信息。
> 详情请参阅 [Zen 隐私文档](https://opencode.ai/docs/zen/#privacy) 和 [隐私政策](https://opencode.ai/legal/privacy-policy)。

---

## 什么是 OpenCode Zen？

OpenCode Zen 是一个免费的、兼容 Anthropic 的 API 网关，用于基准测试最适合编程代理的模型和提供商。虽然它是为 OpenCode 设计的，**但它适用于任何代理**，包括 Claude Code，只需把 `ANTHROPIC_BASE_URL` 指向 `https://opencode.ai/zen`。

它公开的目标是：

> *“基准测试最适合编程代理的模型/提供商。”*
> — [opencode.ai/docs/zen/#goals](https://opencode.ai/docs/zen/#goals)

---

## 可用模型

目前仅确认两个模型稳定可用：

| 模型 | 说明 |
|---|---|
| `big-pickle` | **推荐。** 将所有 Anthropic 模型槽位都映射到它。 |
| `minimax-m2.5-free` | 免费层替代方案。数据可能会用于模型训练。 |

其他模型目前无法正常工作。
[如果你很在意，可以在这里报告问题](https://github.com/anomalyco/opencode/issues/new)。
已向维护者报告问题，请在这里查看更新。

---

## 已知限制

- ❌ 不支持 **Claude for Chrome** 扩展，因为 Zen 只是一个 API 后端。
- ❌ 不支持 **Slack**、**Telegram** 等渠道集成。
- ❌ 目前只有 `big-pickle` 和 `minimax-m2.5-free` 可用。
- ❌ 再次提醒，由于这些是免费模型，提示词可能会被用于训练，不要发送敏感或专有代码。

---

## 最佳已知配置

下面是推荐配置，它把所有 Anthropic 模型层都映射到 `big-pickle`：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://opencode.ai/zen",
    "ANTHROPIC_AUTH_TOKEN": "sk-In....", # 在这里粘贴你的 opencode zen api key
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "big-pickle"
  },
  "model": "big-pickle"
}
```

---

## 设置指南

### 步骤 1 — 安装 Claude Code

访问 [Claude Code 的 GitHub 仓库](https://github.com/anthropics/claude-code)

### 步骤 2 — 获取你的 Zen API Key

访问 [opencode.ai/zen](https://opencode.ai/docs/zen/#how-it-works)，创建账户并复制你的 API key，无需启用计费。
将它填入 `config.json` 文件中的 `PASTE_YOUR_KEY`。

### 步骤 3 — 配置你的环境

我推荐的唯一方法是使用 **config 文件**，因为它可移植，并且与平台无关。

先备份你现有的配置，因为之后需要覆盖它。

在你的主目录中创建或编辑 `.claude/config.json`：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://opencode.ai/zen",
    "ANTHROPIC_AUTH_TOKEN": "PASTE_YOUR_KEY",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "big-pickle"
  },
  "model": "big-pickle"
}
```

```text
# macOS / Linux
~/.claude/config.json

# Windows
%USERPROFILE%\.claude\config.json
```

### 步骤 4 — 启动 Claude Code

```bash
cd /your/project
claude /logout
claude
```

Claude Code 会自动使用 Zen 作为后端。你可以问它一个简单问题来确认是否正常工作。

---

## 工作原理

Zen 是 Anthropic API 的即插即用替代品。Claude Code 不会感知到差异，因为三个模型层级（Sonnet、Opus、Haiku）都会映射到 `big-pickle`，这是 Zen 在内部使用的别名。实际底层模型可能会变化，因为 Zen 会匿名基准测试模型以减少偏差。

---

## 链接

- [Zen 仪表板](https://opencode.ai/zen)
- [Zen 隐私文档](https://opencode.ai/docs/zen/#privacy)
- [Zen 目标](https://opencode.ai/docs/zen/#goals)
- [隐私政策](https://opencode.ai/legal/privacy-policy)
- [服务条款](https://opencode.ai/legal/terms-of-service)
- [报告问题](https://github.com/anomalyco/opencode/issues/new)