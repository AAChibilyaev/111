# 03. Скрытые возможности Dataview

## 1. Продвинутые запросы
```dataview
TABLE WITHOUT ID
  file.link AS "Заметка",
  length(file.etags) AS "Кол-во тегов",
  dateformat(date(created), "yyyy-MM-dd") AS "Создано"
FROM #обзор
WHERE created >= date(today) - dur(7 days)
SORT created DESC
```
- Агрегация данных (length, count)
- Форматирование дат
- Условия времени (dur)

## 2. Работа с задачами
```dataview
TASK FROM #project/active 
WHERE !completed AND due <= date(today) + dur(3 days)
GROUP BY due
```
- Фильтрация по сроку выполнения
- Группировка задач по датам
- Специальный синтаксис TASK

## 3. Встроенные вычисления
```dataview
LIST "Прогресс: " + round((completed / (completed + active)) * 100) + "%"
FROM #project
```
- Математические операции
- Функция round()
- Конкатенация строк

## 4. Парсинг контента
```dataview
TABLE regexreplace(file.text, "#.*", "") AS "Текст без тегов"
FROM "Daily"
```
- Очистка текста (regexreplace)
- Работа с raw-контентом
- Извлечение данных

## 5. JS API для плагинов
```javascript
const notes = await app.plugins.plugins.dataview.api
  .pages('#book')
  .where(p => p.rating > 3);
```
- Использование в Templater
- Программный доступ к данным
- Комбинирование с другими плагинами

*Источники: forum.obsidian.md/t/dataview-plugin, документация Dataview*

## Связанные руководства
[[00_Оглавление]] | [[03_Секреты_Dataview]]
