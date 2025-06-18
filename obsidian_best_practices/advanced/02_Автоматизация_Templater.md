# 02. Мощная автоматизация с Templater

## 1. Динамические шаблоны
```javascript
<%* 
const project = tp.file.title.split("_")[0];
tR += `#${project}`
%>
```
- Генерация контента на основе названия файла
- Поддержка JavaScript-логики

## 2. Работа с метаданными
```javascript
<%*
const date = tp.date.now("YYYY-MM-DD");
tp.file.rename(`${date}_Отчет`);
tp.frontmatter["status"] = "черновик";
%>
```
- Автопереименование файлов
- Динамическое заполнение frontmatter

## 3. Интеграция с задачами
```javascript
<%*
const tasks = await tp.system.prompt("Введите задачи через запятую");
tR += tasks.split(",").map(t => `- [ ] ${t.trim()}`).join("\n");
%>
```
- Интерактивные prompt-окна
- Преобразование текста в задачи

## 4. Парсинг веб-страниц
```javascript
<%*
const url = await tp.system.prompt("URL статьи");
const content = await tp.user.scrape_article(url);
tR += content;
%>
```
- Использование пользовательских скриптов
- Интеграция с Web Scraper

## 5. Условная логика
```javascript
<%*
if (tp.file.exists(tp.file.title + "_Ресурсы")) {
    tR += `[[${tp.file.title}_Ресурсы]]`;
}
%>
```
- Проверка существования файлов
- Условная генерация контента

*Источники: forum.obsidian.md/t/templater, плагин Templater Docs*

## Связанные руководства
[[00_Оглавление]] | [[02_Автоматизация_Templater]]
