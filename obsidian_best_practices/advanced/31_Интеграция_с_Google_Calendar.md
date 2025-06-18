# 31. Полная интеграция с Google Calendar

## 1. Настройка плагина
```yaml
# .obsidian/plugins/google-calendar.json
{
  "client_id": "your-client-id",
  "api_key": "your-api-key",
  "calendars": ["work", "personal"],
  "syncInterval": 15
}
```

## 2. Синхронизация событий
```markdown
```gcal-event
date: {{date}}
event: Совещание по проекту {{title}}
details: [[Проектные заметки]]
reminder: 15m
```
```

## 3. Автоматическое создание заметок
```javascript
// При создании события в календаре
onGCalEventCreated((event) => {
  app.vault.create(
    `Meetings/${event.date}_${event.name}.md`,
    `# ${event.name}\n\n**Время**: ${event.time}`
  );
});
```

## 4. Виджет календаря
```css
/* Стилизация виджета */
.gcal-widget {
  font-family: var(--font-text);
  border: 1px solid var(--background-modifier-border);
}
```

## 5. Требования
- Плагин Google Calendar 2.0+
- API ключ Google Cloud
- OAuth 2.0 аутентификация

*Источник: Официальная документация плагина*