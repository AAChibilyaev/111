# 04. Глубокая кастомизация через CSS

## 1. Темные темы с акцентами
```css
.theme-dark {
  --accent: #ff79c6;
  --text-selection: rgba(255, 121, 198, 0.3);
}
```
- Кастомизация цветовых переменных
- Плавные выделения текста
- Сочетание с существующими темами

## 2. Адаптация под мобильные устройства
```css
@media screen and (max-width: 900px) {
  .workspace-tabs { padding: 0 5px; }
  .markdown-preview-view { font-size: 14px; }
}
```
- Медиа-запросы для разных экранов
- Оптимизация пространства
- Увеличение читаемости

## 3. Стилизация редактора
```css
.cm-line {
  font-family: "Fira Code", monospace;
  line-height: 1.8;
}
.cm-active { background: var(--background-modifier-active); }
```
- Кастомные шрифты для кода
- Улучшенные межстрочные интервалы
- Подсветка активной строки

## 4. Виджеты для плагинов
```css
.dataview table {
  border-collapse: collapse;
  width: 100%;
}
.dataview th { background: var(--background-primary-alt); }
```
- Улучшение таблиц Dataview
- Стилизация заголовков
- Адаптивные таблицы

## 5. Анимации и переходы
```css
.modal {
  animation: fadeIn 0.3s ease-out;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
```
- Плавные появления модалок
- Микроанимации интерфейса
- Улучшение UX

*Источники: forum.obsidian.md/c/css-themes, репозитории популярных тем*

## Связанные руководства
[[00_Оглавление]] | [[04_Кастомизация_CSS]]
