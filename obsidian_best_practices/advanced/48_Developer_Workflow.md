# 48. Obsidian для разработчиков (MacOS-оптимизировано)

## 1. Интеграция с VS Code
### Конфигурация Live Preview
```json
// .vscode/settings.json
{
  "obsidian": {
    "server": "http://localhost:27123",
    "autoRefresh": true,
    "macosDeepLinks": true
  }
}
```

### Автоматическая синхронизация сниппетов
```bash
#!/bin/zsh
# Синхронизация сниппетов VSCode → Obsidian
rsync -av ~/Library/Application\ Support/Code/User/snippets/ ~/Obsidian/Code/Snippets/
```

## 2. Работа с Git через CLI
### Alias для Obsidian-Git
```zsh
# ~/.zshrc
alias ogit='cd ~/Obsidian && git'
alias olog='ogit log --pretty=format:"%C(yellow)%h %C(blue)%ad %C(green)%s" --date=short'
```

## 3. Интеграция с Docker
### Контейнер для плагинов
```dockerfile
FROM node:18
WORKDIR /obsidian
COPY package*.json .
RUN npm install -g obsidian-plugin-cli
VOLUME /plugins
CMD ["opc", "watch"]
```

## 4. Системные инструменты разработчика
| Инструмент          | Назначение                          | Пример использования               |
|---------------------|-------------------------------------|------------------------------------|
| **iTerm2**          | Терминальная интеграция             | `open obsidian://search?query=API` |
| **Postman**         | Документирование API                | Коллекции → Obsidian-экспорт       |
| **TablePlus**       | Работа с базами данных              | SQL-запросы → Markdown-таблицы     |

## 5. Полезные плагины для разработки
- **CodeMirror**: Продвинутое редактирование кода
- **API Viewer**: Документирование API
- **Dev Tools**: Встроенная консоль разработчика

## Лучшие практики MacOS:
1. Используйте **Quick Look** для просмотра JSON/XML:
   ```terminal
   qlmanage -p snippet.json
   ```
2. Настройте **Xcode Command Line Tools** для сборки плагинов:
   ```terminal
   xcode-select --install
   ```
3. Включите **Rosetta** для совместимости с ARM/x86

*Требования: Xcode 15+, Node.js 18+*