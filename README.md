# 🖼️ Vision Skill

[English](#english) · [中文](#chinese)

---

## English

Give image recognition ability to models without native vision support (like DeepSeek) — by calling an external visual API.

### Quick Install

```bash
npx skills add guorui999/vision
```

### Setup

```bash
node ~/.claude/skills/vision/scripts/vision.js --setup
```

Enter your API Key, API URL, and model name when prompted.

Or edit config directly: `~/.claude/skills/vision/config.json`

```json
{
  "base_url": "https://dashscope.aliyuncs.com/compatible-mode/v1",
  "api_key": "your-api-key",
  "model": "qwen3.5-omni-plus"
}
```

### Usage

After setup, send an image or say "look at this image" — Claude will auto-trigger the skill.

```bash
# Local image
node scripts/vision.js photo.jpg "Describe this image"

# Remote image
node scripts/vision.js --url https://example.com/img.png "What is this?"

# Multiple images
node scripts/vision.js img1.jpg img2.jpg "Compare these two"

# With cache (skip API call if same image + prompt analyzed before)
node scripts/vision.js --cache photo.jpg "Describe this image"
```

### Supported Formats

jpg, jpeg, png, gif, webp, bmp

### Supported Services

| Service | Model | Notes |
|---------|-------|-------|
| **Alibaba Cloud Bailian** | `qwen3.5-omni-plus` | 1M free tokens for new users |
| Alibaba Cloud Bailian | `qwen-vl-max` | Same as above |
| OpenAI | `gpt-4o-mini` | Requires overseas payment |
| Others | Any OpenAI-compatible | Change `BASE_URL` + model name |

### How It Works

1. Read image → base64 encode
2. Call visual API (OpenAI-compatible format)
3. Return text description

### Docs

- [SKILL.md](SKILL.md) — Full documentation (CN/EN)
- [install.sh](install.sh) — One-click install script

---

## Chinese / 中文

让没有原生识图能力的模型（如 DeepSeek）也能"看图"——通过调用外部视觉 API 获取图片的文字描述。

### 一键安装

```bash
npx skills add guorui999/vision
```

### 配置

```bash
node ~/.claude/skills/vision/scripts/vision.js --setup
```

按提示输入 API Key、API 地址、模型名称。

或直接编辑配置文件：`~/.claude/skills/vision/config.json`

```json
{
  "base_url": "https://dashscope.aliyuncs.com/compatible-mode/v1",
  "api_key": "你的API Key",
  "model": "qwen3.5-omni-plus"
}
```

### 使用

配置完成后，直接发送图片或说"看这张图"即可自动识别。

```bash
# 本地图片
node scripts/vision.js photo.jpg "描述这张图片"

# 网络图片
node scripts/vision.js --url https://example.com/img.png "这是什么？"

# 多张图片
node scripts/vision.js img1.jpg img2.jpg "比较这两张图"

# 缓存模式（同一图片+prompt 避免重复调用 API）
node scripts/vision.js --cache photo.jpg "描述这张图片"
```

### 支持的图片格式

jpg, jpeg, png, gif, webp, bmp

### 支持的视觉服务

| 服务 | 模型 | 备注 |
|------|------|------|
| **阿里云百炼（推荐）** | `qwen3.5-omni-plus` | 新用户 100 万 token 免费 |
| 阿里云百炼 | `qwen-vl-max` | 同上 |
| OpenAI | `gpt-4o-mini` | 需海外支付 |
| 其他 | 任何 OpenAI 兼容格式 | 改 `BASE_URL` 和模型名即可 |

### 工作原理

1. 读取图片文件 → 转换为 base64
2. 调用视觉 API（OpenAI 兼容格式）
3. 返回文字描述

### 文档

- [SKILL.md](SKILL.md) — 完整使用说明（中英双语）
- [install.sh](install.sh) — 一键安装脚本
