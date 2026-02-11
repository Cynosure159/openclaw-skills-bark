# Send Bark Message Skill

Send push notifications to iOS devices via Bark API with Markdown support.

## Features

- ✅ POST request notifications
- ✅ Markdown formatting (title, bold, italic, lists, etc.)
- ✅ Rich customization options (icon, sound, group, URL, etc.)
- ✅ Notification priority levels
- ✅ History archive

## Configuration

### Method 1: Write to TOOLS.md

Create or edit `TOOLS.md` in your workspace:

```markdown
### Bark Push
- base_url: https://api.day.app
- key: your_Bark_device_key
```

### Method 2: Environment Variables

```bash
export BARK_BASE_URL="https://api.day.app"
export BARK_KEY="your_Bark_device_key"
```

#### Optional Configuration

| Environment Variable | Description | Default |
|----------------------|-------------|---------|
| `BARK_ICON` | Default notification icon URL | OpenClaw avatar |
| `BARK_GROUP` | Default notification group | OpenClaw |

```bash
export BARK_BASE_URL="https://api.day.app"
export BARK_KEY="your_Bark_device_key"
export BARK_ICON="https://example.com/icon.png"
export BARK_GROUP="MyApp"
```

### Getting Your Key

1. Open Bark App
2. Tap "Copy Test URL" in the top right
3. URL format: `https://api.day.app/xxxxxxxxxxxx`
   - `base_url` → `https://api.day.app`
   - `key` → `xxxxxxxxxxxx`

## Usage Examples

### Simple Notification

```bash
curl -X "POST" "https://api.day.app/your_key" \
  -H 'Content-Type: application/json' \
  -d '{"body": "Hello from Bark!"}'
```

### With Title

```bash
curl -X "POST" "https://api.day.app/your_key" \
  -H 'Content-Type: application/json' \
  -d '{"title": "Reminder", "body": "This is a notification"}'
```

### Markdown Format

```bash
curl -X "POST" "https://api.day.app/your_key" \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Daily Summary",
    "markdown": "## Completed Today\n\n- [x] Task A\n- [x] Task B\n\n**Total**: 5 tasks"
  }'
```

### Full Parameters

```bash
curl -X "POST" "https://api.day.app/your_key" \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d '{
    "title": "Alert",
    "subtitle": "System Monitor",
    "markdown": "CPU usage over 90%",
    "level": "critical",
    "sound": "alarm",
    "badge": 5,
    "icon": "https://example.com/icon.png",
    "image": "https://example.com/screenshot.png",
    "group": "alerts",
    "url": "https://example.com",
    "isArchive": 1
  }'
```

## Parameter Reference

| Parameter | Type | Description |
|-----------|------|-------------|
| `title` | string | Notification title |
| `subtitle` | string | Notification subtitle |
| `body` | string | Plain text content |
| `markdown` | string | Markdown content (higher priority than body) |
| `level` | string | Interrupt level: `critical`, `active`, `timeSensitive`, `passive` |
| `sound` | string | Notification sound |
| `badge` | number | Badge number |
| `icon` | string | Icon URL (uses BARK_ICON default if not specified) |
| `image` | string | Image URL |
| `group` | string | Notification group (uses BARK_GROUP default if not specified) |
| `url` | string | URL to open when tapped |
| `copy` | string | Custom copyable text |
| `isArchive` | number | Save to history (1=save) |
| `id` | string | Notification ID (same ID updates notification) |
| `delete` | string | Delete notification (1=delete, requires id) |

## FAQ

### Q: No notification sound?

Check the `level` parameter. Set to `critical` for sound in silent mode.

### Q: How to update a sent notification?

Use the same `id` parameter when sending again.

### Q: Markdown not working?

Ensure the `markdown` parameter exists - it overrides the `body` content.

## Links

- [Bark Documentation](https://bark.day.app/)
- [Bark GitHub](https://github.com/Finb/Bark)
