# 36. Полная интеграция с GitHub

## 1. Настройка Git-плагина
```yaml
# .obsidian/plugins/git.json
{
  "remote": "git@github.com:username/obsidian-notes.git",
  "branch": "main",
  "autoPull": true,
  "autoPush": true,
  "commitMessage": "Autosave: {{date}}"
}
```

## 2. GitHub Actions для автоматизации
```yaml
# .github/workflows/sync.yml
name: Obsidian Sync
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Pandoc Export
        run: |
          pandoc README.md -o README.pdf
      - uses: actions/upload-artifact@v3
        with:
          name: obsidian-export
          path: README.pdf
```

## 3. Совместная работа
```markdown
```git-collab
Участники:
- @user1: Ведущий разработчик
- @user2: Контент-менеджер
- @user3: Редактор

Правила:
1. Коммиты только в feature-ветки
2. Pull Request для изменений
3. Регулярный rebase с main
```
```

## 4. Резервное копирование Issues
```python
# Скрипт экспорта Issues в Markdown
import requests
import json

issues = requests.get("https://api.github.com/repos/username/repo/issues")
for issue in issues.json():
    with open(f"GitHub/{issue['number']}.md", "w") as f:
        f.write(f"# {issue['title']}\n\n{issue['body']}")
```

## 5. Лучшие практики
- `.gitignore` для временных файлов
- Частые мелкие коммиты
- Ветвление по feature-модели
- Регулярный sync с удаленным репозиторием

*Требуется: Git 2.30+, GitHub аккаунт*