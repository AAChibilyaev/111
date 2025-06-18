# 06. Продвинутая работа с PDF-документами

## 1. Встраивание PDF
````markdown
```pdf
path: Assets/papers/study.pdf
page: 3
highlight: "важный термин"
```
````
- Плагин PDF Highlights
- Навигация по страницам
- Поиск и подсветка текста

## 2. Аннотирование PDF
```javascript
// Автоматическое извлечение аннотаций
const annotations = await pdfExtract("Research.pdf");
tR += annotations.map(a => `> ${a.text}\n-- стр. ${a.page}`).join("\n\n");
```
- Плагин Annotator
- Экспорт заметок в Markdown
- Связь с исходным документом

## 3. Полнотекстовый поиск
```yaml
plugins:
  - pdf-text:
      index_folder: "Academic/"
      exclude: ["drafts/"]
```
- Индексация содержимого PDF
- Поиск по тексту внутри файлов
- Фильтрация по папкам

## 4. Конвертация в Markdown
```bash
pandoc -s paper.pdf -o paper.md --wrap=none
```
- Использование Pandoc
- Сохранение структуры документа
- Дальнейшая обработка в Obsidian

## 5. Синхронизация с Zotero
```markdown
```zotero
collection: "Исследования"
tags: ["важно"]
```
````
- Плагин Zotero Integration
- Автоматический импорт метаданных
- Связь с библиографией

*Источники: forum.obsidian.md/t/pdf-workflows, документация плагинов*

## Связанные руководства
[[00_Оглавление]] | [[06_Работа_с_PDF]]
