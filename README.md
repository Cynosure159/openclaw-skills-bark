# OpenClaw Bark Skills

Bark notification skills for OpenClaw - send push notifications and schedule reminders via Bark API.

## Skills

### 1. send-bark-message
Send push notifications via Bark API with POST requests and Markdown support.

**Features:**
- Send notifications with Markdown content
- Custom title, sound, and badge
- Best effort delivery mode

**Usage:**
```bash
# Check skill documentation
cat send-bark-message/SKILL.md
```

### 2. cron-bark-notification
Schedule Bark notifications using cron jobs with best effort delivery.

**Features:**
- Schedule notifications at specific times
- Use with cron-mastery skill for reliable scheduling
- Announce delivery summary

**Usage:**
```bash
# Check skill documentation
cat cron-bark-notification/SKILL.md
```

## Configuration

Configure Bark server in your OpenClaw TOOLS.md:

```markdown
### Bark 推送
- base_url: 192.168.x.x:13001
- key: your-api-key
- icon: https://example.com/icon.png
- group: MyApp
```

## Installation

These skills are designed for OpenClaw. Install via:

```bash
# Copy to your skills directory
cp send-bark-message /path/to/openclaw/skills/
cp cron-bark-notification /path/to/openclaw/skills/
```

## License

MIT
