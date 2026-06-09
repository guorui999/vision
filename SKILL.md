---
name: vision
description: |
  Give image recognition to models without native vision. Trigger when user sends/shares images or asks to analyze/describe/compare images.
  让没有原生 vision 能力的模型获得识图能力。当用户发送图片、分享图片路径、或要求分析/描述/识别图片内容时使用。
---

# Vision Skill

[English](#english) · [中文](#chinese)

---

## English

Enable models without native vision (e.g. DeepSeek) to "see" images via an external visual API.

### Quick Setup

```bash
node scripts/vision.js --setup
```

Follow prompts to enter API Key, API URL, and model name.

#### Check Current Config

```bash
node scripts/vision.js --config
```

### Usage

#### Auto-trigger (Recommended)

When user sends an image or asks to analyze one, call:

```bash
node scripts/vision.js "<image-path>" "Describe this image in Chinese"
```

#### Single Image

```bash
# Local image
node scripts/vision.js /path/to/image.jpg "Describe the content"

# Remote image
node scripts/vision.js --url https://example.com/image.png "What is this?"
```

#### Multiple Images

```bash
# Multiple local images
node scripts/vision.js image1.jpg image2.jpg image3.jpg "Compare these images"

# Mixed local and remote
node scripts/vision.js local.jpg --url https://example.com/online.png "How are these related?"
```

#### Cache Mode

```bash
# Avoid repeated API calls for the same image + prompt
node scripts/vision.js --cache photo.jpg "Describe this image"
node scripts/vision.js --cache img1.jpg img2.jpg "Compare these two"
```

Cache key is built from file path + mtime + size + prompt. Auto-managed (max 50 entries, LRU eviction).

### Supported Formats

jpg, jpeg, png, gif, webp, bmp

### Supported Vision Services

| Service | Model | Notes |
|---------|-------|-------|
| **Alibaba Cloud Bailian (recommended)** | `qwen3.5-omni-plus` | 1M free tokens for new users |
| Alibaba Cloud Bailian | `qwen-vl-max` | Same as above |
| OpenAI | `gpt-4o-mini` | Requires overseas payment |
| Others | Any OpenAI-compatible | Change `BASE_URL` + model name |

### Config File

`~/.claude/skills/vision/config.json`

```json
{
  "base_url": "https://dashscope.aliyuncs.com/compatible-mode/v1",
  "api_key": "your-api-key",
  "model": "qwen3.5-omni-plus"
}
```

### How It Works

1. Read image file → base64 encode
2. Call visual API (OpenAI-compatible format)
3. Return text description

### Notes

- Node.js runtime required
- API Key must be configured before first use
- Remote images must be publicly accessible

---

## Chinese / 中文

让没有原生识图能力的模型（如 DeepSeek）也能"看图"——通过调用外部视觉 API 获取图片的文字描述。

### 快速配置

```bash
node scripts/vision.js --setup
```

按提示输入 API Key、API 地址、模型名称。

#### 查看当前配置

```bash
node scripts/vision.js --config
```

### 使用方法

#### 自动触发（推荐）

当用户发送图片或要求分析图片时，自动调用：

```bash
node scripts/vision.js "<图片路径>" "用中文描述这张图片"
```

#### 单张图片

```bash
# 本地图片
node scripts/vision.js /path/to/image.jpg "描述图片内容"

# 网络图片
node scripts/vision.js --url https://example.com/image.png "这是什么？"
```

#### 多张图片

```bash
# 多张本地图片
node scripts/vision.js image1.jpg image2.jpg image3.jpg "比较这些图片的异同"

# 混合本地和网络图片
node scripts/vision.js local.jpg --url https://example.com/online.png "这两张图有什么关系？"
```

#### 缓存模式

```bash
# 避免同一图片重复调用 API
node scripts/vision.js --cache photo.jpg "描述这张图片"
node scripts/vision.js --cache img1.jpg img2.jpg "比较这两张图"
```

缓存基于文件路径 + 修改时间 + 大小 + prompt 生成 key，自动管理上限（最多 50 条，LRU 淘汰）。

### 支持的图片格式

jpg, jpeg, png, gif, webp, bmp

### 支持的视觉服务

| 服务 | 模型 | 备注 |
|------|------|------|
| **阿里云百炼（推荐）** | `qwen3.5-omni-plus` | 新用户 100 万 token 免费 |
| 阿里云百炼 | `qwen-vl-max` | 同上 |
| OpenAI | `gpt-4o-mini` | 需海外支付 |
| 其他 | 任何 OpenAI 兼容格式 | 改 `BASE_URL` 和模型名即可 |

### 配置文件说明

配置文件：`~/.claude/skills/vision/config.json`

```json
{
  "base_url": "https://dashscope.aliyuncs.com/compatible-mode/v1",
  "api_key": "你的API Key",
  "model": "qwen3.5-omni-plus"
}
```

### 工作原理

1. 读取图片文件 → 转换为 base64
2. 调用视觉 API（OpenAI 兼容格式）
3. 返回文字描述

### 注意事项

- 需要 Node.js 环境
- 首次使用需配置 API Key
- 网络图片需要能访问对应 URL
