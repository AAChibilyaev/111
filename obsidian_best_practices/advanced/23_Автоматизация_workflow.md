# 23. Автоматизация рабочих процессов

## 1. Templater + QuickAdd
```javascript
// Автоматическое создание еженедельного отчета
module.exports = async (params) => {
  const date = params.date || moment().format("YYYY-MM-DD");
  await app.plugins.getPlugin('quickadd').createFile(
    `Reports/Weekly/${date}.md`,
    await tp.file.include("[[Templates/Weekly Report]]")
  );
};
```

## 2. Интеграция с Make/Integromat
```yaml
automation:
  - trigger: "new_file_in_folder"
    folder: "Inbox"
    actions:
      - "apply_template: Processing"
      - "move_to: Projects/{{category}}"
```

## 3. Работа с API
```javascript
// Автоматическая синхронизация с Notion
const response = await fetch('https://api.notion.com/v1/pages', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${API_KEY}` },
  body: JSON.stringify({
    parent: { database_id: DATABASE_ID },
    properties: { title: tp.file.title }
  })
});
```

## 4. Плагин DataviewJS
```markdown
```dataviewjs
// Автоматическое обновление статусов задач
dv.taskList(dv.pages().file.tasks
  .where(t => !t.completed && t.due <= date('today')))
```
```

## 5. Локальные скрипты
```bash
#!/bin/bash
# Ежедневный бэкап в 3:00 AM
obsidian-export vault/ backup/ --frontmatter=always
rclone sync backup/ drive:ObsidianBackup
```

*Источники: Официальная документация Templater, Make API*