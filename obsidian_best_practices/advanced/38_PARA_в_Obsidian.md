# 38. Система PARA в Obsidian

## 1. Базовая структура
```yaml
Vault/
  ├── 1_Projects/
  │   ├── Website_Redesign
  │   └── Research_Paper
  ├── 2_Areas/
  │   ├── Health
  │   └── Finances
  ├── 3_Resources/
  │   ├── Articles
  │   └── Templates
  └── 4_Archives/
      ├── Completed_Projects
      └── Old_Resources
```

## 2. Автоматизация перемещения
```javascript
// Автоматическое перемещение в Archive
app.vault.on('modify', (file) => {
  if (file.tags.includes('#completed')) {
    file.move('4_Archives/Completed/' + file.name);
  }
});
```

## 3. Шаблон проекта
```markdown
```project-template
# {{name}}

**Статус**: {{status}}
**Дедлайн**: {{date}}

## Основные задачи
- [ ] Инициализация
- [ ] Исследование
- [ ] Реализация

## Ссылки
[[Ресурсы/{{topic}}]]
```
```

## 4. Дашборд PARA
```dataviewjs
dv.table(
  ["Тип", "Количество"],
  [
    ["Проекты", dv.pages('"1_Projects"').length],
    ["Области", dv.pages('"2_Areas"').length],
    ["Ресурсы", dv.pages('"3_Resources"').length]
  ]
)
```

## 5. Интеграции
- **Tasks**: Управление задачами
- **Calendar**: Планирование сроков
- **Kanban**: Визуализация workflow

*Источник: Методология Tiago Forte*