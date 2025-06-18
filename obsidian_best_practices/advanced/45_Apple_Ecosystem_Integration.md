# 45. Глубокая интеграция с экосистемой Apple

## 1. Двусторонняя синхронизация с Reminders
### Конфигурация Shortcuts
```yaml
# Obsidian-Reminders.shortcut
input: Reminders List "Obsidian"
actions:
  - repeat with each item:
      text: "{{Repeat Item}}"
      prepend: ~/Obsidian/Tasks/{{CurrentDate}}.md
      format: "- [ ] {{text}} #reminder"
```

### Автоматизация через cron
```bash
*/15 * * * * /usr/bin/shortcuts run "Obsidian-Reminders-Sync"
```

## 2. Импорт из Apple Notes
```applescript
tell application "Notes"
  set allNotes to notes
  repeat with aNote in allNotes
    set noteContent to plaintext of aNote
    set noteTitle to name of aNote
    do shell script "echo " & quoted form of noteContent & " > ~/Obsidian/Imports/AppleNotes/" & quoted form of noteTitle & ".md"
  end repeat
end tell
```

## 3. Safari → Obsidian Workflow
### Закладка с JavaScript:
```javascript
javascript:(function(){
  let title=document.title;
  let url=location.href;
  let sel=window.getSelection().toString();
  prompt('Копируйте в Obsidian:',`[[${title}]]\nURL: ${url}\n\n${sel}`);
})();
```

## 4. Universal Control между устройствами
```yaml
# .obsidian/sync-settings.json
{
  "apple_continuity": {
    "handoff": true,
    "icloud_sync": "~/Library/Mobile Documents/iCloud~md~obsidian/Documents/"
  }
}
```

## 5. Интеграция с Focus Mode
```terminal
# Автоматическое переключение тем при фокусе
defaults write com.obsidian.macos FocusTheme -string "theme-dark"
```

## Лучшие практики:
1. Используйте **Share Extension** для быстрого сохранения из любого приложения
2. Настройте **Automator** для обработки PDF/веб-страниц
3. Включите **iCloud Keychain** для синхронизации API-ключей

*Требования: MacOS Ventura 13.4+, Obsidian 1.5+*