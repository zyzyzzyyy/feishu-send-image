# Feishu Send Image Skill 🖼️

将本地图片发送到飞书聊天的 OpenClaw 技能。

## 功能特性

- ✅ 原样发回用户发送的图片
- ✅ 发送浏览器截图
- ✅ 发送本地图片文件
- ✅ 支持多种图片格式（JPG/PNG/GIF/WEBP）
- ✅ 自动识别 MIME 类型

## 安装方法

### 本地安装
```bash
# 克隆到此目录
npx skills add https://github.com/zyzyzzyyy/feishu-send-image
```

### 通过 OpenClaw
技能已内置在 `~/.openclaw/skills/feishu-send-image/`

## 使用示例

### 示例 1：发送图片
```
用户：把这张图片发给我
执行：message send -> 发送图片
```

### 示例 2：浏览器截图
```
用户：帮我截个图
执行：browser screenshot -> message send
```

## 触发词

- "发送图片"
- "发一下图片"
- "原样发回"
- "send image"
- "发送截图"

## 文件结构

```
feishu-send-image/
├── SKILL.md      # 技能定义文件
├── README.md     # 本文件
└── skill.yaml    # 技能配置
```

## 依赖

- OpenClaw Message 工具
- 飞书渠道配置

## 版本

1.0.0 - 初始版本

## 许可证

MIT
