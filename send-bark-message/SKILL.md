---
name: send-bark-message
description: Send push notifications via Bark API with POST requests and Markdown support. Use when you need to send notifications to iOS devices via Bark.
---

# Bark Notification Skill

## Overview

This skill sends push notifications to iOS devices using the Bark API with POST requests and full Markdown support.

## Configuration Required

Users must configure before first use:
- `base_url`: Bark server URL (e.g., `https://api.day.app`)
- `key`: Bark device key

### Optional Default Configuration

Users can configure default values for icon and group:

| Variable | Description | Default |
|----------|-------------|---------|
| `BARK_ICON` | Default notification icon URL | OpenClaw avatar |
| `BARK_GROUP` | Default notification group | OpenClaw |

**Example in .env:**
```bash
BARK_BASE_URL="https://api.day.app"
BARK_KEY="your_key"
BARK_ICON="https://example.com/icon.png"
BARK_GROUP="MyApp"
```

### Configuration Methods

**Option 1: Write to TOOLS.md**
```markdown
### Bark Push
- base_url: https://api.day.app
- key: 你的Bark设备key
```

**Option 2: Environment variables**
```bash
export BARK_BASE_URL="https://api.day.app"
export BARK_KEY="your_Bark_device_key"
```

**Option 3: .env file (workspace)**
Create `.env` file in OpenClaw workspace directory:
```bash
BARK_BASE_URL="https://api.day.app"
BARK_KEY="your_Bark_device_key"
BARK_ICON="https://example.com/icon.png"
BARK_GROUP="MyApp"
```

### Getting Your Key

1. Open Bark app
2. Tap "Copy Test URL"
3. URL format: `https://api.day.app/your_key`
   - Base URL: `https://api.day.app`
   - Key: the part after `/`

## Sending Notifications

### Basic POST Request

Send a notification using JSON body:

```bash
curl -X "POST" "{base_url}/{key}" \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d '{
    "title": "Notification Title",
    "body": "Notification content here",
    "markdown": "## Markdown Content\n\n**Bold text** and *italic text*"
  }'
```

### URL Path Variants

```bash
# Body only
https://{base_url}/{key}/{body}

# Title and body
https://{base_url}/{key}/{title}/{body}

# Title, subtitle, and body
https://{base_url}/{key}/{title}/{subtitle}/{body}
```

### POST Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `title` | string | Notification title |
| `subtitle` | string | Notification subtitle |
| `body` | string | Plain text content |
| `markdown` | string | Markdown formatted content (overrides body) |
| `level` | string | Interrupt level: `critical`, `active`, `timeSensitive`, `passive` |
| `sound` | string | Notification sound name |
| `badge` | number | Badge number |
| `icon` | string | Icon URL (uses BARK_ICON env default if not specified) |
| `image` | string | Image URL to display |
| `group` | string | Notification group (uses BARK_GROUP env default if not specified) |
| `url` | string | URL to open when tapped |
| `copy` | string | Custom copyable text |
| `autoCopy` | string | Set to "1" for auto-copy |
| `isArchive` | number | Set to 1 to save notification |
| `id` | string | Notification ID for updates |
| `delete` | string | Set to "1" to delete notification |

### Example with Full Options

```json
{
  "title": "Alert",
  "subtitle": "Subtitle here",
  "markdown": "# Title\n\n- Item 1\n- Item 2",
  "level": "active",
  "sound": "minuet",
  "badge": 5,
  "icon": "https://example.com/icon.png",
  "image": "https://example.com/image.png",
  "group": "alerts",
  "url": "https://example.com",
  "copy": "Copied text",
  "isArchive": 1
}
```

## Quick Examples

**Simple notification:**
```bash
curl -X "POST" "{base_url}/your_key" \
  -H 'Content-Type: application/json' \
  -d '{"body": "Hello from Bark!"}'
```

**With title:**
```bash
curl -X "POST" "{base_url}/your_key" \
  -H 'Content-Type: application/json' \
  -d '{"title": "Hello", "body": "World"}'
```

**Markdown content:**
```bash
curl -X "POST" "{base_url}/your_key" \
  -H 'Content-Type: application/json' \
  -d '{"title": "Report", "markdown": "## Summary\n\n**Total**: $100"}'
```

## Best Practices

1. Always URL-encode path parameters in GET requests
2. Use markdown for rich formatting (overrides body)
3. Set appropriate `level` based on urgency
4. Use `group` to organize notifications in notification center
5. Configure `isArchive` to save important notifications
