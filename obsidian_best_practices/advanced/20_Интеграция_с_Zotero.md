# 20. Полная интеграция с Zotero

## 1. Настройка плагина
```yaml
# .obsidian/plugins/zotero/data.json
{
  "libraryPath": "~/Zotero",
  "autoImport": true,
  "noteTemplate": "Templates/Zotero Note.md",
  "exportFormats": ["md", "pdf"]
}
```
- Поддержка нескольких библиотек
- Автоматическое обновление
- Кастомные шаблоны экспорта

## 2. Работа с цитатами
```markdown
Согласно исследованию [@doe2023, с. 45], 
основной вывод заключается в...

> "Ключевое открытие исследования" [@smith2022, с. 12]
```
- Автоматическое форматирование
- Поддержка стилей APA/MLA
- Перекрестные ссылки

## 3. Шаблоны для заметок
```markdown
# {{title}}

**Авторы**: {{authors}}
**Год**: {{year}}

## Основные тезисы
{{abstract}}

## Мои комментарии
{{annotations}}
```
- Динамические переменные
- Автозаполнение метаданных
- Поддержка LaTeX

## 4. Библиографические отчеты
```dataviewjs
dv.table(
  ["Работа", "Цитаты"],
  dv.pages('"Zotero"').map(p => [
    p.file.link,
    p.annotations.length
  ])
)
```

## 5. Экспорт в научные форматы
```javascript
await app.plugins.getPlugin('pandoc').export({
  format: "latex",
  template: "Academic",
  citations: true
});
```
- Генерация PDF через LaTeX
- Автоматическая библиография
- Поддержка сложных шаблонов

*Источник: Официальная документация Zotero Integration v3.2+*

## Связанные руководства
[[00_Оглавление]] | [[20_Интеграция_с_Zotero]]
