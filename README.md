# Claude Code × OpenCode Zen API — Cross-Platform Setup Guide, no proxy, no rate limiting, no bs.

Translations: [Arabic](README.ar.md) | [Chinese](README.zh.md)

> **Privacy notice first:** Free models on OpenCode Zen or ANY OTHER FREE LLM PROVIDER may use your prompts to improve their models.
> Avoid sending sensitive code, credentials, or proprietary information.
> See the [Zen privacy docs](https://opencode.ai/docs/zen/#privacy) and [privacy policy](https://opencode.ai/legal/privacy-policy) for details.

---

## What is OpenCode Zen?

OpenCode Zen is a free, Anthropic-compatible API gateway that benchmarks the best models and providers for coding agents. While it is designed to pair with OpenCode, **it works with any agent** — including Claude Code — by simply pointing `ANTHROPIC_BASE_URL` at `https://opencode.ai/zen`.

Its stated goal is:

> *"Benchmark the best models/providers for coding agents."*
> — [opencode.ai/docs/zen/#goals](https://opencode.ai/docs/zen/#goals)

---

## Working Models

Only two models are currently confirmed to work reliably:

| Model | Notes |
|---|---|
| `big-pickle` | **Recommended.** Map all Anthropic model slots to this. |
| `minimax-m2.5-free` | Free tier alternative. Data may be used for model training. |

Other models won't not work for now. 
[If you care enough, report it as an issues here](https://github.com/anomalyco/opencode/issues/new).

---

## Known Limitations

- ❌ **Claude for Chrome** extension is not supported — as Zen is an API backend only, yet playwright works well.
- ❌ **Slack, Telegram, etc channels integrations** are not supported
- ❌ Only `big-pickle` and `minimax-m2.5-free` models work.
- ❌ Again, as these are free models, prompts may be used for training — do not send sensitive or proprietary code.

---

## Best Known Configuration

This is the recommended config that maps all Anthropic model tiers to `big-pickle`:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://opencode.ai/zen",
    "ANTHROPIC_AUTH_TOKEN": "sk-In....", # paste your opencode zen api key here 
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "big-pickle"
  },
  "model": "big-pickle"
}
```

---

## Setup Guide

### Step 1 — Install Claude Code

Visit [claude-code github repo](https://github.com/anthropics/claude-code)

### Step 2 — Get Your Zen API Key

Visit [opencode.ai/zen](https://opencode.ai/docs/zen/#how-it-works) , create an account and copy your API key, no need to enable billing. 
Place it in `PASTE_YOUR_KEY` in `config.json` file.

---

### Step 3 — Configure Your Environment

This **config file** method is the only method I recommend as it is portable and platform-agnostic.

Fisrt back up you existing config , as you will need to overwrite your existing one.

```
# macOS / Linux
~/.claude/config.json

# Windows
%USERPROFILE%\.claude\config.json
```

Create or edit `config.json` in your home directory:

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
---

---

### Step 4 — Launch Claude Code

```bash
cd /your/project
claude /logout
claude
```

Claude Code will automatically use Zen as its backend. Ask it something simple to confirm it is working.

---

## How It Works

Zen acts as a drop-in replacement for Anthropic's API. Claude Code never knows the difference — all three model tiers (Sonnet, Opus, Haiku) are mapped to `big-pickle`, which is an alias Zen uses internally. Also it delegate any potential SubAgents errors.
The actual underlying model may vary, as Zen benchmarks models anonymously to remove bias.

---

## Links

- [Zen dashboard](https://opencode.ai/zen)
- [Zen privacy docs](https://opencode.ai/docs/zen/#privacy)
- [Zen goals](https://opencode.ai/docs/zen/#goals)
- [Privacy policy](https://opencode.ai/legal/privacy-policy)
- [Terms of service](https://opencode.ai/legal/terms-of-service)
- [Report an issue](https://github.com/anomalyco/opencode/issues/new)
