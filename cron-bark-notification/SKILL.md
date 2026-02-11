---
name: cron-bark-notification
description: Cron + Bark notification best practices using agentTurn with announce + bestEffort.
---

# Cron + Bark Notification Skill

**Reliable Cron + Bark notification solution**

## Recommended Approach

### delivery.mode = "announce" + bestEffort

Use `announce` mode + `bestEffort: true`, allowing missing delivery target without failure:

```json
{
  "name": "Water Reminder",
  "schedule": { "kind": "at", "atMs": <TIMESTAMP_MS> },
  "payload": {
    "kind": "agentTurn",
    "message": "curl -X 'POST' 'http://BARK_URL/KEY' -H 'Content-Type: application/json' -d '{\"title\": \"💧 Water Reminder\", \"body\": \"Time to drink water!\", \"level\": \"active\", \"sound\": \"minuet\"}'"
  },
  "sessionTarget": "isolated",
  "wakeMode": "now",
  "enabled": true,
  "delivery": {
    "mode": "announce",
    "bestEffort": true
  }
}
```

## Troubleshooting

### "cron delivery target is missing"

Use `bestEffort: true` to ignore this error without affecting task execution.

### No Bark notification received after task execution

1. Check Bark server: `curl http://BARK_URL/KEY`
2. Check task status: `cron runs --id <job-id>`
3. Check Bark app notification permissions

## Quick Commands

```bash
# View task list
cron list --includeDisabled true

# View execution history
cron runs --id <job-id>

# Delete task
cron remove <job-id>
```
