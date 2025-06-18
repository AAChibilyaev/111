# 33. Профессиональный экспорт в Microsoft Word

## 1. Настройки Pandoc
```yaml
# .obsidian/plugins/export.json
{
  "pandoc_path": "/usr/local/bin/pandoc",
  "defaults": {
    "reference_doc": "Templates/word_template.docx",
    "filters": ["pandoc-crossref"]
  }
}
```

## 2. Базовый экспорт
```markdown
```export-to-word
format: docx
template: academic
styles:
  heading1: "Heading 1,14pt"
  code: "Source Code,11pt"
```
```

## 3. Расширенные параметры
```javascript
// Программный экспорт с кастомизацией
await app.plugins.getPlugin('advanced-export').export({
  format: 'docx',
  files: ['Research/**/*.md'],
  output: 'Thesis_Chapters.docx',
  toc: true,
  numberSections: true
});
```

## 4. Поддержка академических форматов
- Автоматическое оглавление
- Нумерация разделов
- Перекрестные ссылки
- Библиография (Zotero/BibTeX)

## 5. Решение проблем
```troubleshooting
Проблема: Не сохраняются формулы LaTeX
Решение: Установить пакет pandoc-math
```

*Требуется: Pandoc 3.0+, Microsoft Word 2019+*