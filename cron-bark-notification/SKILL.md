---
name: cron-bark-notification
description: Cron + Bark notification best practices using agentTurn with announce + bestEffort.
---

# Cron + Bark Notification Skill

**使用 Cron 发送 Bark 通知的可靠方案**

## 推荐方案

### delivery.mode = "announce" + bestEffort

使用 `announce` 模式 + `bestEffort: true`，允许缺失 delivery target 但不失败：

```json
{
  "name": "喝水提醒",
  "schedule": { "kind": "at", "atMs": <TIMESTAMP_MS> },
  "payload": {
    "kind": "agentTurn",
    "message": "curl -X 'POST' 'http://BARK_URL/KEY' -H 'Content-Type: application/json' -d '{\"title\": \"💧 喝水提醒\", \"body\": \"该喝水啦！\", \"level\": \"active\", \"sound\": \"minuet\"}'"
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

## 错误排查

### "cron delivery target is missing"

使用 `bestEffort: true` 可以忽略此错误，不影响任务执行。

### 任务执行后没有收到 Bark 通知

1. 检查 Bark 服务器：`curl http://BARK_URL/KEY`
2. 查看任务状态：`cron runs --id <job-id>`
3. 检查 Bark 应用的通知权限

## 快速命令

```bash
# 查看任务列表
cron list --includeDisabled true

# 查看执行历史
cron runs --id <job-id>

# 删除任务
cron remove <job-id>
```
