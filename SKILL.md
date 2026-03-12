---
name: feishu-send-image
description: 将本地图片发送到飞书聊天的技能，支持原样发回用户图片、浏览器截图和本地文件。
---

# 🦞 飞书图片消息处理技能

> **适用范围**：OpenClaw 平台 + 飞书（Feishu/Lark）渠道  
> **核心能力**：将用户发送的图片原样发回，或将浏览器截图发送给用户  
> **重要限制**：当前模型无法直接查看图片内容，需要用户口头描述

---

## 📌 触发场景

当用户表达以下意图时触发此技能：

- "发送图片"、"发一下图片"、"把图片发给我"
- "原样发回"、"转发图片"
- 用户发送图片后需要确认
- 需要发送浏览器截图
- 需要发送本地图片文件

**触发词示例**：
- "发送图片"
- "send image"
- "原样发回"
- "发一下图片"
- "截图给我看"

---

## 📥 步骤 1：获取图片路径

### 场景 A：用户刚发送的图片

系统会在对话上下文中提示：
```
[media attached: ~/.openclaw/media/inbound/xxx.jpg]
```

或者命令行查找最新图片：
```bash
ls -lt ~/.openclaw/media/inbound/ | head -3
```

### 场景 B：浏览器截图

截图后返回结果：
```
MEDIA:~/.openclaw/media/browser/xxx.png
```

### 场景 C：本地图片文件

使用绝对路径：`/path/to/your/image.png`

---

## 📤 步骤 2：发送图片

### 核心公式

```json
{
  "action": "send",
  "media": "~/.openclaw/media/inbound/xxx.jpg",
  "mimeType": "image/jpeg"
}
```

### 参数说明

| 参数 | 必填 | 说明 | 示例 |
|------|------|------|------|
| `action` | ✅ | 固定为 `"send"` | `"send"` |
| `media` | ✅ | 图片**本地绝对路径** | `"~/.openclaw/media/inbound/xxx.jpg"` |
| `mimeType` | ✅ | MIME 类型 | `"image/jpeg"` 或 `"image/png"` |
| `target` | ❌ | 省略（自动回复当前会话） | 不填 |

### MIME 类型对照表

| 文件扩展名 | MIME 类型 |
|-----------|----------|
| `.jpg` / `.jpeg` | `image/jpeg` |
| `.png` | `image/png` |
| `.gif` | `image/gif` |
| `.webp` | `image/webp` |
| `.bmp` | `image/bmp` |

---

## ✅ 完整示例

### 示例 1：发回用户图片

**场景**：用户发图问"这是什么？"

**操作**：
1. 从系统提示中复制图片路径
2. 调用 `message` 工具：
```json
{
  "action": "send",
  "media": "~/.openclaw/media/inbound/xxx.jpg",
  "mimeType": "image/jpeg"
}
```
3. 发送文字说明：
```
图片已发回！但我现在看不到图片内容，需要你描述一下图片里是什么，我才能帮你分析～ 👀
```

### 示例 2：发送浏览器截图

**步骤 1：打开网页**
```json
{
  "action": "navigate",
  "target": "host",
  "url": "https://www.baidu.com"
}
```

**步骤 2：截图**
```json
{
  "action": "screenshot",
  "target": "host",
  "type": "png"
}
```
返回结果：`MEDIA:~/.openclaw/media/browser/xxx.png`

**步骤 3：发送截图**
```json
{
  "action": "send",
  "media": "~/.openclaw/media/browser/xxx.png",
  "mimeType": "image/png"
}
```

---

## ❌ 常见错误与解决方案

| 错误 | 正确做法 |
|------|---------|
| `media: "./image.jpg"`（相对路径） | 必须用绝对路径 |
| `media: "~/workspace/..."` | 必须展开为完整路径 |
| `mimeType: "image/png"`（jpg 文件） | 根据实际类型选择 |
| 添加 `target` 参数 | 省略，自动回复当前会话 |
| 用 `read` 工具"查看"图片 | `read` 只能读元数据，模型看不到内容 |

---

## 🎯 成功关键

**一句话总结**：用户发图 → 保存本地 → `message` + 绝对路径 + MIME 类型 → 发回

**关键点**：
- ✅ 使用绝对路径
- ✅ 正确 MIME 类型
- ✅ 不填 `target` 参数
- ❌ 模型无法查看图片内容

---

## 📁 文件路径

- **用户发送的图片**：`~/.openclaw/media/inbound/<UUID>.jpg`
- **浏览器截图**：`~/.openclaw/media/browser/<UUID>.png`
- **本地图片**：用户工作区路径

---

## 📚 依赖

- OpenClaw Message 工具
- 飞书渠道配置
- 有效的图片文件

---

*版本：1.0.0*  
*最后更新：2026-03-12*  
*基于原始学习文件重写*
