# 44. Продвинутая настройка Quick View и горячих клавиш

## 1. Системные твики для Quick Look
```terminal
# Включаем Markdown-рендеринг в Quick Look
defaults write com.apple.finder QLEnableTextSelection -bool true
brew install qlmarkdown
qlmanage -r
```

## 2. Кастомные сочетания клавиш
```yaml
# .obsidian/hotkeys.json
{
  "quick-view": {
    "macos": {
      "open": "ctrl+cmd+q",
      "pin": "ctrl+cmd+shift+q"
    },
    "ai_actions": {
      "summarize": "ctrl+alt+s",
      "expand": "ctrl+alt+e"
    }
  }
}
```

## 3. Интеграция с Raycast
```javascript
// Скрипт для Raycast (показ превью с подсветкой синтаксиса)
app.commands.registerCommand({
  id: "enhanced-preview",
  name: "Enhanced Preview",
  callback: () => {
    const file = app.workspace.getActiveFile();
    execSync(`/usr/local/bin/glow ${file.path} | raycast --prompt "Preview"`);
  }
});
```

## 4. Автоматическое обновление превью
```applescript
tell application "Obsidian"
  activate
  tell application "System Events"
    keystroke "p" using {command down, shift down}
  end tell
end tell
```

## 5. Лучшие плагины для навигации
- **Quick Explorer**: ALT+Щелчок для мгновенного превью
- **Hover Editor**: Плавающие редактируемые окна
- **Advanced Navigation**: Горячие клавиши для ссылок

*Оптимизация для MacOS:*
```terminal
# Уменьшаем задержку Quick Look
defaults write -g QLPanelAnimationDuration -float 0.1
```

**Pro Tip:** Для мгновенного поиска по превью используйте `cmd+option+space` с интеграцией Spotlight.