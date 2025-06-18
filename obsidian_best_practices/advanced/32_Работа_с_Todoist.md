# 32. Синхронизация с Todoist

## 1. Настройка API
```yaml
plugins:
  todoist-sync:
    api_key: "your_api_key_here"
    project_map:
      "Inbox": "Входящие"
      "Work": "Работа"
```

## 2. Синтаксис задач
```markdown
```todoist-task
content: Завершить документ {{title}}
due: today 18:00
priority: 1
labels: work, urgent
```
```

## 3. Двусторонняя синхронизация
```javascript
// Автоматическое создание задач из заметок
app.workspace.on('file-open', (file) => {
  if (file.tags.includes('#task')) {
    app.plugins.getPlugin('todoist-sync').createTask({
      content: `Обработать: ${file.basename}`,
      due: 'today'
    });
  }
});
```

## 4. Виджет списка задач
```markdown
```todoist-query
filter: "today | overdue"
show: 5
```
```

## 5. Полезные команды
- `Todoist: Sync Now` - Принудительная синхронизация
- `Todoist: Create Task` - Быстрое создание задачи
- `Todoist: View Completed` - Просмотр выполненных задач

*Требуется Todoist Premium для полного функционала*