# 28. Глубокая кастомизация через CSS

## 1. Основные области стилизации
```css
/* .obsidian/snippets/custom.css */
.workspace-tabs .workspace-leaf {
  background: var(--background-secondary-alt);
  border-radius: 8px;
}
```

## 2. Популярные модификации
```css
/* Анимация ссылок */
.internal-link {
  transition: all 0.3s ease;
}
.internal-link:hover {
  color: var(--text-accent);
  text-shadow: 0 0 5px var(--text-accent);
}
```

## 3. Темные темы с градиентами
```css
.theme-dark {
  --background-primary: linear-gradient(135deg, #1e1e2e, #121218);
  --text-normal: rgba(255,255,255,0.85);
}
```

## 4. Стили для конкретных плагинов
```css
/* Dataview таблицы */
.dataview.table {
  font-family: 'Fira Code', monospace;
  border-collapse: separate;
}
```

## 5. Ресурсы для обучения
- [Obsidian CSS Variables Guide](https://css.obsidian.md)
- [Theme Development Kit](https://github.com/obsidianmd/theme-sample)
- [Community Style Vault](https://forum.obsidian.md/c/css-themes/14)

*Примеры проверены на версии Obsidian 1.5+*