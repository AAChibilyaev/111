# 34. Интеграция Python с Obsidian

## 1. Настройка окружения
```python
# requirements.txt
obsidianmd>=1.5.0
python-dotenv
markdown2
```

## 2. Базовый API доступ
```python
import os
from obsidianmd import Vault

vault = Vault(path="~/ObsidianVault")
note = vault.get_note("Project Ideas.md")
print(note.content[:100])
```

## 3. Автоматическая обработка
```python
# Автоматическое добавление метаданных
for note in vault.notes:
    if "статья" in note.tags:
        note.frontmatter["type"] = "research"
        note.save()
```

## 4. Сложные преобразования
```python
# Конвертация таблиц Dataview в CSV
from mdutils import MdUtils
import pandas as pd

table = vault.query("TABLE file.name FROM #project")
pd.DataFrame(table).to_csv("projects.csv")
```

## 5. Планировщик задач
```python
# Ежедневный бэкап в 3:00 AM
import schedule

def backup():
    vault.export_backup(format="zip")

schedule.every().day.at("03:00").do(backup)
```

*Требуется: Python 3.10+, obsidianmd-py 2.0+*