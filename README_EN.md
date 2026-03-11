# Feishu Send Image Skill 🖼️

An OpenClaw skill for sending local images to Feishu chat.

## Features

- ✅ Send back user images
- ✅ Send browser screenshots
- ✅ Send local image files
- ✅ Support multiple formats (JPG/PNG/GIF/WEBP)
- ✅ Auto-detect MIME types

## Installation

### Local Installation
```bash
npx skills add <your-github-username>/feishu-send-image
```

### Via OpenClaw
Skill is built-in at `~/.openclaw/skills/feishu-send-image/`

## Usage Examples

### Example 1: Send Image
```
User: Send this image to me
Action: message send -> send image
```

### Example 2: Browser Screenshot
```
User: Take a screenshot for me
Action: browser screenshot -> message send
```

## Trigger Words

- "发送图片" (Send image)
- "发一下图片" (Send the image)
- "原样发回" (Send back as is)
- "send image"
- "发送截图" (Send screenshot)

## File Structure

```
feishu-send-image/
├── SKILL.md      # Skill definition
├── README.md     # This file (Chinese)
├── README_EN.md  # English version
├── LICENSE       # MIT License
└── skill.yaml    # Skill configuration
```

## Dependencies

- OpenClaw Message Tool
- Feishu Channel Configuration

## Version

1.0.0 - Initial release

## License

MIT License - See [LICENSE](LICENSE) for details.
