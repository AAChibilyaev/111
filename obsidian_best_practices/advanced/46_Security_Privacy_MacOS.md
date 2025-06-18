# 46. Безопасность и приватность в Obsidian (MacOS)

## 1. Шифрование хранилища
### APFS-шифрование
```terminal
# Включение шифрования для папки Obsidian
diskutil apfs encryptVolume /Volumes/ObsidianVault -user disk
```

### Конфигурация плагина Crypt
```yaml
# .obsidian/plugins/crypt.json
{
  "encryption_method": "aes-256",
  "auto_lock": {
    "enabled": true,
    "timeout": 300
  },
  "touch_id": true
}
```

## 2. Защита метаданных
### Очистка метаданных PDF перед импортом
```bash
#!/bin/zsh
# ~/Library/Services/Clean_Metadata.workflow
for file in "$@"
do
  exiftool -all= "$file"
  mv "$file" ~/Obsidian/Imports/
done
```

## 3. Системные ограничения
### Sandboxing через MacOS
```terminal
# Ограничение доступа плагинов
tccutil reset All com.obsidian.macos
```

## 4. Резервное копирование с проверкой целостности
```bash
#!/usr/bin/env bash
# Ежедневный скрипт проверки
backup_dir="/Volumes/EncryptedBackup/Obsidian_$(date +%Y%m%d)"
rsync -ac --delete --checksum ~/Obsidian/ "$backup_dir"
shasum -a 256 ~/Obsidian/* > "$backup_dir/checksums.sha256"
```

## 5. Плагины для безопасности
- **Secure Vault**: Аппаратное шифрование
- **Audit Log**: Трек изменений
- **Permission Checker**: Контроль доступа

## Лучшие практики MacOS:
1. Включите **FileVault** для полного дискового шифрования
2. Используйте **Touch ID** для плагинов через `biometric-auth`
3. Настройте **Privacy → Full Disk Access** для Obsidian
4. Регулярно проверяйте разрешения в `tccutil`

*Требования: MacOS Monterey 12.3+, Obsidian 1.4+*