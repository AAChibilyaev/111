# 15. Автоматизация с JavaScript API

## 1. Официальное API Obsidian
```javascript
// Создание новой заметки
app.vault.create('Daily/2025-06-20.md', `# ${new Date().toLocaleDateString()}`);

// Открытие заметки
app.workspace.openLinkText('2025-06-20', 'Daily');
```
- Безопасные методы работы с vault
- Полный список методов: `app.*` namespace
- Обработка ошибок

## 2. Работа с метаданными
```javascript
// Чтение frontmatter
const file = app.vault.getAbstractFileByPath('Note.md');
const frontmatter = app.metadataCache.getFileCache(file).frontmatter;

// Запись в frontmatter
app.fileManager.processFrontMatter(file, fm => {
    fm.updated = new Date().toISOString();
});
```

## 3. Плагины через JS
```javascript
// Доступ к плагинам
const dataview = app.plugins.plugins.dataview.api;
const tasks = dataview.pages('#task').where(t => !t.completed);

// Вызов команд
app.commands.executeCommandById('workspace:split-vertical');
```

## 4. Обработка событий
```javascript
// Подписка на события
this.registerEvent(app.vault.on('modify', file => {
    console.log(`Файл изменен: ${file.path}`);
}));

// Дебаг событий
app.workspace.on('layout-change', () => console.log('Layout changed'));
```

## 5. Безопасное выполнение
```javascript
try {
    await app.vault.modify(file, newContent);
} catch (err) {
    console.error('Ошибка записи:', err);
    new Notice('Ошибка сохранения!');
}
```
- Обязательная обработка ошибок
- Уведомления для пользователя
- Логирование операций

*Источник: Официальная документация Obsidian API v1.4+*

## Связанные руководства
[[00_Оглавление]] | [[15_Автоматизация_с_JavaScript]]
