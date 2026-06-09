# Vision Skill

让没有原生识图能力的 Claude Code 模型也能"看图"。

## 安装

```bash
# 克隆仓库
git clone https://github.com/guorui999/claude-vision-skill.git
cd claude-vision-skill

# 复制到 Claude Code skills 目录
cp -r vision ~/.claude/skills/
```

## 配置

```bash
node ~/.claude/skills/vision/scripts/vision.js --setup
```

按提示输入 API Key、API 地址、模型名称。

或直接编辑配置文件：`~/.claude/skills/vision/config.json`

## 使用

配置完成后，直接发送图片或说"看这张图"即可自动识别。

## 文档

- [SKILL.md](SKILL.md) - 完整使用说明
- [install.sh](install.sh) - 一键安装脚本
