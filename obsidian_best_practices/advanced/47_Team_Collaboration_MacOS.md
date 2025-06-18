# 47. Командная работа в Obsidian (MacOS-оптимизировано)

## 1. Настройка общего хранилища
### Конфигурация Git для команд
```terminal
# Автоматический разрешение конфликтов
git config --global merge.obsidian.driver "macos_merge_tool --auto"
```

### Конфиг плагина Sync
```yaml
# .obsidian/plugins/sync.json
{
  "team_mode": true,
  "conflict_resolution": "smart",
  "macos_notifications": true,
  "file_lock_timeout": 300
}
```

## 2. Режим реального времени
### Использование локальной сети
```bash
# Общий доступ через mDNS
dns-sd -P "Obsidian Sync" _obsidian._tcp local 52424 $(hostname)
```

## 3. Интеграция с Messages
```applescript
tell application "Messages"
  send "Новая версия документа [[Project Plan]] готова к проверке" to chat "Team Chat"
  attach "/Users/Shared/Obsidian/Project Plan.md"
end tell
```

## 4. Системные инструменты для коллаборации
| Инструмент          | Командное использование              | Пример команды                      |
|---------------------|--------------------------------------|-------------------------------------|
| **Screen Sharing**  | Совместное редактирование           | `open vnc://teammate@local`         |
| **Notes**           | Быстрые черновики                   | `notes://showNote?identifier=ABC123`|
| **Time Machine**    | Восстановление версий               | `tmutil restore ~/Obsidian`         |

## 5. Безопасность в команде
```terminal
# Автоматическая проверка подписей
codesign --verify --verbose ~/Obsidian/*.md
```

## Лучшие практики:
1. Используйте **MacOS ACL** для тонкого контроля доступа:
   ```terminal
   chmod +a "teamuser allow read,write" ~/Shared/Obsidian/
   ```
2. Настройте **Automator workflow** для уведомлений об изменениях
3. Включите **Universal Clipboard** для быстрого обмена контентом

*Требования: MacOS Ventura 13.0+, Obsidian 1.5+*