# 43. Лучшие AI-флоу для Obsidian на MacOS

## 1. Сквозные AI-автоматизации
### Умный импорт контента (Safari → Obsidian)
```applescript
tell application "Safari"
  set pageTitle to name of front document
  set pageURL to URL of front document
  set selectedText to do JavaScript "window.getSelection().toString()" in front document
end tell

do shell script "echo '## " & pageTitle & "\\n\\nURL: " & pageURL & "\\n\\n### Выдержка:\\n" & selectedText & "\\n\\n### AI-резюме:\\n' > /tmp/import.md && /opt/homebrew/bin/llm -m llama3 --temp 0.7 -p 'Обобщи текст на русском:' < /tmp/import.md >> ~/Obsidian/Inbox/" & (do shell script "date '+%Y-%m-%d'") & "_" & (do shell script "echo " & quoted form of pageTitle & " | tr -s ' ' '_' | cut -c-50") & ".md"
```

---

## 2. Локальные AI-агенты
### Конфигурация Llama 3 + Text Generation WebUI
```yaml
# ~/Library/Application Support/obsidian/plugins/local-llm.json
{
  "model_path": "~/models/llama-3-8b-instruct.Q5_K_M.gguf",
  "prompt_template": "Ты ассистент Obsidian. Анализируй текст и отвечай на русском:\n{{input}}",
  "macos_optimization": {
    "metal": true,
    "threads": 8,
    "batch_size": 512
  }
}
```

---

## 3. Системные интеграции
### Глобальный AI-поиск (через Spotlight/Alfred)
```bash
#!/bin/zsh
# ~/Library/Services/Search_Obsidian.workflow/Contents/document.wflow
query=$(osascript -e 'text returned of (display dialog "AI-поиск в Obsidian:" default answer "")')
results=$(/opt/homebrew/bin/obsidian-cli search --ai "$query" --model llama3)
osascript -e "display notification \"${results//\"/}\" with title \"Результаты поиска\""
```

---

## 4. Автоматизированные workflow
### Ежедневный дайджест (через cron + Shortcuts)
```terminal
0 9 * * * /usr/bin/shortcuts run "Obsidian_Daily_Digest" && /opt/homebrew/bin/obsidian-cli ai --prompt "Сгенерируй дайджест из заметок за последние 24 часа, выдели 3 ключевые темы" --output ~/Obsidian/Daily/$(date +%Y-%m-%d).md
```

---

## 5. Лучшие комбинации инструментов
| Инструмент          | Использование                          | Пример команды                      |
|---------------------|----------------------------------------|-------------------------------------|
| **Keyboard Maestro**| Горячие клавиши для AI-действий       | `⌃⌥⌘S` → Отправить выделенное в ChatGPT |
| **Hammerspoon**     | Окно с AI-ассистентом                 | `hs.application.launchOrFocus("Obsidian")` |
| **Raycast**         | Быстрый AI-анализ                     | `/ai "Перефразируй текст" {{selected}}` |

---

## 6. Оптимизация производительности
```terminal
# Увеличиваем лимит памяти для LLM
sudo sysctl -w kern.memorystatus_highwater_enabled=1
sudo sysctl -w kern.memorystatus_highwater=12000
```

*Требования:*
- MacOS Sonoma 14.4+
- Obsidian 1.5+
- Установленные: `llama.cpp`, `obsidian-cli`, `Raycast AI`

> **Pro Tip:** Для максимальной скорости используйте [MLX](https://github.com/ml-explore/mlx) от Apple с поддержкой M-чипов.