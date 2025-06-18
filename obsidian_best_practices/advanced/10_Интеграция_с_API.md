# 10. Мощные интеграции с внешними API

## 1. Вебхуки для автоматизации
```javascript
<%*
const res = await fetch("https://api.example.com/webhook", {
  method: "POST",
  body: JSON.stringify({
    title: tp.file.title,
    content: tp.file.content
  })
});
%>
```
- Отправка данных при создании заметки
- Интеграция с IFTTT/Zapier
- Поддержка Templater

## 2. Импорт данных из Twitter
```yaml
plugins:
  - twitter-import:
      api_key: "YOUR_KEY"
      save_to: "Social/Twitter/"
      format: "[[{{date}}]] {{text}}"
```
- Плагин Twitter Importer
- Сохранение твитов как заметки
- Кастомные шаблоны

## 3. Синхронизация с Notion
```markdown
```notion-sync
database_id: abc123
filter: {property: "Status", select: {equals: "Done"}}
mapping:
  title: "Name"
  content: "Notes"
```
```
- Плагин Notion Sync
- Двусторонняя синхронизация
- Гибкое сопоставление полей

## 4. Работа с Google Calendar
```javascript
const events = await googleCalendar.getEvents({
  timeMin: tp.date.now("YYYY-MM-DD"),
  timeMax: tp.date.now("YYYY-MM-DD", 1)
});
```
- Плагин Google Calendar
- Импорт событий в ежедневные заметки
- Создание событий из задач

## 5. Интеграция с ChatGPT
```markdown
```ai-prompt
model: gpt-4
temperature: 0.7
prompt: >
  Суммаризируй текст ниже как маркированный список:
  {{content}}
```
```
- Плагин Text Generator
- Использование AI для обработки заметок
- Кастомизация промптов

*Источники: forum.obsidian.md/t/api-integrations, документация плагинов*

## Связанные руководства
[[00_Оглавление]] | [[10_Интеграция_с_API]]
