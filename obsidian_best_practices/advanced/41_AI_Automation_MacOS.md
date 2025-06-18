# 41. Продвинутые AI-автоматизации и настройки для MacOS

## 1. AI Workflow (Obsidian + OpenAI/Local Models)
### Автоматическая обработка заметок
```yaml
# .obsidian/plugins/ai-assistant.json
{
  "api_key": "sk-your-key",
  "model": "gpt-4-1106-preview",
  "auto_actions": {
    "summarize": true,
    "generate_tags": true,
    "link_suggestions": 5
  }
}
```

### Пример Shortcut для MacOS (Automator):
```bash
#!/bin/zsh
# Автогенерация конспекта из выделенного текста
selected_text=$(pbpaste)
curl https://api.openai.com/v1/chat/completions \
  -H "Authorization: Bearer $OPENAI_KEY" \
  -d '{
    "model": "gpt-4",
    "messages": [{"role": "user", "content": "Суммаризируй текст: '$selected_text'"}]
  }' | jq '.choices[0].message.content' | pbcopy
```

---

## 2. Полная автоматизация на MacOS
### Лучшие инструменты:
- **Keyboard Maestro**: Управление горячими клавишами
- **Hazel**: Автосортировка файлов
- **Alfred**: Быстрый поиск + AI-интеграция

### Пример: Автозагрузка PDF в Obsidian
```applescript
tell application "Finder"
  set pdfFiles to selection as list
  repeat with pdfFile in pdfFiles
    do shell script "/opt/homebrew/bin/pandoc " & quoted form of POSIX path of (pdfFile as text) & " -o ~/Obsidian/Inbox/" & name of pdfFile & ".md"
  end repeat
end tell
```

---

## 3. Системные настройки MacOS для Obsidian
### Оптимизация:
```terminal
# Увеличим лимит открытых файлов
sudo launchctl limit maxfiles 65536 200000
```

### Автозапуск:
```bash
# Добавляем Obsidian в автозагрузку
osascript -e 'tell application "System Events" to make login item at end with properties {path:"/Applications/Obsidian.app", hidden:false}'
```

---

## 4. Локальные LLM (для оффлайн-работы)
```yaml
# Конфиг для llama.cpp
model: "llama-3-8b"
gpu_layers: 35
context_size: 4096
temp: 0.7
```

### Интеграция через плагин:
```javascript
app.plugins.getPlugin('local-llm').setModel({
  path: "~/models/llama-3-8b.Q4_K_M.gguf",
  template: "### Запрос: {{input}}\n### Ответ:"
});
```

---

## 5. Security Best Practices
```terminal
# Шифрование хранилища
diskutil apfs encryptVolume /Volumes/ObsidianBackup
```

*Проверено на MacOS Sonoma 14.4+ и Obsidian 1.5+*  
*Для работы требуется: Homebrew, jq, pandoc*