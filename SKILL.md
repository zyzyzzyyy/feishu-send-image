---
name: feishu-send-image
description: |
  Send local images to Feishu chat. Use this skill when the user wants to send, forward, or return images in Feishu conversations — including sending back user images, browser screenshots, or local files. Trigger on phrases like "发送图片", "send image", "原样发回", "发一下图片", or when the user shares an image and wants it sent somewhere.
---

# Feishu Send Image Skill 🖼️

Send local images to Feishu chat. Supports returning user images, browser screenshots, and local files.

## When to Use

- User sends an image and wants it sent back or forwarded
- Need to send browser screenshots to chat
- Sending local image files
- Multiple images need to be sent sequentially

## Workflow

### Step 1: Get Image Path

**Scenario A: User just sent an image**
```
[media attached: ~/.openclaw/media/inbound/xxx.jpg]
```

Or find latest:
```bash
ls -lt ~/.openclaw/media/inbound/ | head -3
```

**Scenario B: Browser screenshot**
```
MEDIA:~/.openclaw/media/browser/xxx.png
```

**Scenario C: Local file**
Use absolute path: `/home/user/workspace/images/xxx.png`

### Step 2: Determine MIME Type

| Extension | MIME Type |
|-----------|-----------|
| .jpg / .jpeg | image/jpeg |
| .png | image/png |
| .gif | image/gif |
| .webp | image/webp |
| .bmp | image/bmp |

### Step 3: Send Image

```json
{
  "action": "send",
  "media": "<absolute-path>",
  "mimeType": "<mime-type>"
}
```

**Key points:**
- Use absolute paths
- Match MIME type to file
- Omit `target` (auto-replies to current session)

## Common Patterns

### Send back user image
```json
{
  "action": "send",
  "media": "~/.openclaw/media/inbound/xxx.jpg",
  "mimeType": "image/jpeg"
}
```

### Send browser screenshot
```json
{
  "action": "send",
  "media": "~/.openclaw/media/browser/xxx.png",
  "mimeType": "image/png"
}
```

### Send local file
```json
{
  "action": "send",
  "media": "/home/user/workspace/demo.png",
  "mimeType": "image/png"
}
```

## Error Handling

| Error | Cause | Fix |
|-------|-------|-----|
| Path invalid | Relative path | Use absolute path |
| MIME mismatch | Wrong type | Check file extension |
| Send failed | File missing | Verify with `ls -lh` |
| Wrong session | Has `target` | Remove `target` param |

## Tips

✅ Use absolute paths
✅ Match MIME type correctly
✅ Omit `target` parameter
✅ Verify file exists before sending

❌ Don't use relative paths
❌ Don't use `~/` prefix in paths
❌ Don't add `target` parameter

## Files

- Inbound images: `~/.openclaw/media/inbound/`
- Browser screenshots: `~/.openclaw/media/browser/`
- Local images: User workspace

## Dependencies

- OpenClaw Message tool
- Feishu channel configuration
- Valid image files

## Version

1.0.0 - Initial release
