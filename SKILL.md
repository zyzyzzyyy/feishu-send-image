# Feishu Send Image Skill 🖼️

## Description
将本地图片发送到飞书聊天。**注意：浏览器截图由 browser-screenshot skill 负责，会自动发送，不需要调用此 skill。**

## Activation
当用户提到以下关键词时触发：
- "发送图片"
- "发一下图片"
- "把图片发给我"
- "原样发回"
- "send image"
- "图片发过来"
- 用户发送图片后需要确认时

## ⚠️ 重要说明

**feishu-send-image 不处理 OpenClaw browser 工具的截图！**

- ❌ browser screenshot 的截图 → 由 **browser-screenshot skill** 负责（会自动发送）
- ✅ 本地图片文件（如 `~/workspace/images/xxx.png`）→ 使用 **feishu-send-image**
- ✅ 用户发送的图片 → 使用 **feishu-send-image**

```
❌ 错误：browser-screenshot + feishu-send-image → 发送两次
✅ 正确：browser-screenshot → 自动发送
✅ 正确：feishu-send-image → 发送本地图片/用户图片
```

## Workflow

### 步骤 0: 判断发送场景

根据用户需求选择合适的 skill：

| 用户需求 | 使用 Skill |
|---------|-----------|
| 浏览器截图、网页截图 | **browser-screenshot**（会自动发送） |
| 发送本地图片文件 | **feishu-send-image** |
| 发回用户发送的图片 | **feishu-send-image** |

### 步骤 1: 获取图片路径

#### 场景 A: 用户刚发送的图片
从系统元数据获取：
```
[media attached: ~/.openclaw/media/inbound/36b70131-a3c2-4a22-99a0-1126fd78f48b.jpg]
```

或从目录查找最新图片：
```bash
ls -lt ~/.openclaw/media/inbound/ | head -3
```

#### 场景 B: 本地图片文件
使用绝对路径：
```
~/workspace/images/xxx.png
```

### 步骤 2: 确定 MIME 类型

| 文件扩展名 | MIME 类型 |
|-----------|----------|
| .jpg / .jpeg | image/jpeg |
| .png | image/png |
| .gif | image/gif |
| .webp | image/webp |

### 步骤 3: 发送图片
```json
{
  "action": "send",
  "media": "<图片绝对路径>",
  "mimeType": "<MIME 类型>"
}
```

## Common Patterns

### 发回用户发送的图片
```
用户发送了一张图片

执行:
1. 从 metadata 获取图片路径
2. feishu-send-image -> 发回给用户
```

### 发送本地图片
```
用户：把这个文件发给我 ~/documents/screenshot.png

执行:
1. feishu-send-image -> 发送本地文件
```

## Error Handling

### 错误 1: 路径不存在
**现象**: 发送失败  
**解决**: 检查文件路径是否正确，使用绝对路径

### 错误 2: MIME 类型错误
**现象**: 图片无法显示  
**解决**: 根据文件类型选择正确的 MIME 类型

### 错误 3: 重复发送
**现象**: 同一张图片发了两次  
**解决**: 
- 如果是浏览器截图 → 只用 browser-screenshot，不要用 feishu-send-image
- 检查是否已经通过 MEDIA: 引用发送过

## Tips
- ✅ 浏览器截图用 browser-screenshot（会自动发送）
- ✅ 本地图片用 feishu-send-image
- ✅ 使用绝对路径
- ✅ 根据文件类型选择正确的 MIME
- ❌ 不要用 feishu-send-image 发送浏览器截图
- ❌ 不要在调用 browser-screenshot 后再调用 feishu-send-image

## Version
- 2.0.0 - 明确区分 browser-screenshot 和 feishu-send-image 的职责
