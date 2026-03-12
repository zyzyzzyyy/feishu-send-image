# Feishu Send Image Skill

🖼️ 将本地图片发送到飞书聊天的 OpenClaw 技能。

## 功能特性

- ✅ 原样发回用户发送的图片
- ✅ 发送浏览器截图
- ✅ 发送本地图片文件
- ✅ 支持多种图片格式（JPG/PNG/GIF/WEBP）
- ✅ 自动识别 MIME 类型

## 前置条件

使用前请确保：

1. **OpenClaw 已安装**：版本 >= 2026.3.0
2. **飞书渠道已配置**：已连接 Feishu 渠道
3. **消息工具可用**：已配置 `message` 工具

## 安装方法

```bash
npx skills add https://github.com/zyzyzzyyy/feishu-send-image
```

## 快速开始

### 1. 发送图片

在对话中发送图片后说：
```
把这张图片发给我
```

### 2. 发送截图

```
帮我截个图并发给我
```

### 3. 发送本地图片

```
发送 /path/to/image.png 给我
```

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
├── SKILL.md # 技能定义文件
├── README.md # 本文件
└── skill.yaml # 技能配置
```

## 常见问题

### Q: 图片发送失败？

**A**: 检查文件路径是否为绝对路径，MIME 类型是否正确。

### Q: 支持哪些图片格式？

**A**: 支持 JPG、PNG、GIF、WEBP 等常见格式，会自动识别 MIME 类型。

### Q: 可以发送其他渠道吗？

**A**: 当前仅支持飞书渠道，其他渠道需要额外配置。

## 依赖

- OpenClaw Message 工具
- 飞书渠道配置

## 版本

1.0.0 - 初始版本

## 许可证

MIT
