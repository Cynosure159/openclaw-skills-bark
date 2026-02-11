# Send Bark Message Skill

通过 Bark API 向 iOS 设备发送推送通知，支持 Markdown 格式。

## 功能特性

- ✅ POST 请求发送通知
- ✅ Markdown 格式支持（标题、加粗、斜体、列表等）
- ✅ 丰富的自定义选项（图标、铃声、分组、URL 跳转等）
- ✅ 通知优先级设置
- ✅ 历史记录保存

## 配置方法

### 方式一：写入 TOOLS.md

在工作区创建或编辑 `TOOLS.md`：

```markdown
### Bark 推送
- base_url: https://api.day.app
- key: 你的Bark设备key
```

### 方式二：环境变量

```bash
export BARK_BASE_URL="https://api.day.app"
export BARK_KEY="你的Bark设备key"
```

#### 可选配置

| 环境变量 | 说明 | 默认值 |
|----------|------|--------|
| `BARK_ICON` | 默认通知图标 URL | OpenClaw 头像 |
| `BARK_GROUP` | 默认通知分组 | OpenClaw |

```bash
export BARK_BASE_URL="https://api.day.app"
export BARK_KEY="你的Bark设备key"
export BARK_ICON="https://example.com/icon.png"
export BARK_GROUP="我的应用"
```

### 获取 Key

1. 打开 Bark App
2. 点击右上角「复制测试URL」
3. URL 格式示例：`https://api.day.app/xxxxxxxxxxxx`
   - `base_url` → `https://api.day.app`
   - `key` → `xxxxxxxxxxxx`

## 使用示例

### 简单通知

```bash
curl -X "POST" "https://api.day.app/你的key" \
  -H 'Content-Type: application/json' \
  -d '{"body": "Hello from Bark!"}'
```

### 带标题

```bash
curl -X "POST" "https://api.day.app/你的key" \
  -H 'Content-Type: application/json' \
  -d '{"title": "提醒", "body": "这是一条通知"}'
```

### Markdown 格式

```bash
curl -X "POST" "https://api.day.app/你的key" \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "日报摘要",
    "markdown": "## 今日完成\n\n- [x] 任务 A\n- [x] 任务 B\n\n**总计**: 5 个任务"
  }'
```

### 完整参数

```bash
curl -X "POST" "https://api.day.app/你的key" \
  -H 'Content-Type: application/json; charset=utf-8' \
  -d '{
    "title": "告警",
    "subtitle": "系统监控",
    "markdown": "CPU 使用率超过 90%",
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

## 参数说明

| 参数 | 类型 | 说明 |
|------|------|------|
| `title` | string | 通知标题 |
| `subtitle` | string | 通知副标题 |
| `body` | string | 纯文本内容 |
| `markdown` | string | Markdown 内容（优先级更高） |
| `level` | string | 中断级别：`critical`, `active`, `timeSensitive`, `passive` |
| `sound` | string | 通知铃声 |
| `badge` | number | 角标数字 |
| `icon` | string | 图标 URL（未指定时使用 BARK_ICON 默认值） |
| `image` | string | 图片 URL |
| `group` | string | 通知分组（未指定时使用 BARK_GROUP 默认值） |
| `url` | string | 点击跳转的 URL |
| `copy` | string | 指定复制的文本 |
| `isArchive` | number | 是否保存到历史（1=保存） |
| `id` | string | 通知 ID（相同 ID 可更新通知） |
| `delete` | string | 删除通知（1=删除，需搭配 id） |

## 常见问题

### Q: 通知没有声音？

检查 `level` 参数，设置为 `critical` 可在静音模式下响铃。

### Q: 如何更新已发送的通知？

使用相同的 `id` 参数再次发送。

### Q: Markdown 不生效？

确保 `markdown` 参数存在，它会覆盖 `body` 内容。

## 相关链接

- [Bark 官方文档](https://bark.day.app/)
- [Bark GitHub](https://github.com/Finb/Bark)
