# 49. Научные исследования в Obsidian (Python/R)

## 1. Интеграция Jupyter Notebook
### Конфигурация плагина
```yaml
# .obsidian/plugins/jupyter.json
{
  "python_path": "/opt/homebrew/bin/python3",
  "default_kernel": "obsidian",
  "auto_convert": {
    "ipynb_to_md": true,
    "preserve_outputs": true
  }
}
```

### Шаблон для анализа данных
````markdown
```python
# %% [markdown]
### {{title}}
**Дата анализа**: {{date}}

# %% [code]
import pandas as pd
data = pd.read_csv("{{input_file}}")
display(data.head())
```
````

## 2. Работа с R через RMarkdown
```r
# .obsidian/templates/analysis.Rmd
---
title: "Анализ: {{experiment_name}}"
date: "`r format(Sys.Date(), '%Y-%m-%d')`"
---

```{r setup}
library(ggplot2)
df <- read.csv("data/{{filename}}")
```

## Результаты
```{r plots}
ggplot(df, aes(x, y)) + geom_point()
```
```

## 3. Автоматизация отчетов
```bash
#!/bin/zsh
# Ежедневный отчет через cron
0 18 * * * /usr/local/bin/Rscript -e "rmarkdown::render('~/Obsidian/Lab/Report.Rmd', output_dir='~/Obsidian/Daily')"
```

## 4. Визуализация данных
| Инструмент          | Интеграция                          | Пример команды                     |
|---------------------|-------------------------------------|------------------------------------|
| **Matplotlib**      | Графики → Markdown                  | `plt.savefig('plot.png', dpi=300)` |
| **Plotly**          | Интерактивные визуализации          | `fig.write_html('viz.html')`       |
| **Observable**      | JS-визуализации в Obsidian          | `embed('https://observablehq.com')`|

## 5. Лучшие практики:
1. Используйте **Python/R Environments** через Conda:
   ```terminal
   conda create -n obsidian python=3.11 jupyter pandas
   ```
2. Настройте **Pandoc** для сложных конвертаций:
   ```terminal
   brew install pandoc-crossref
   ```
3. Включите **LaTeX** для научных формул:
   ```terminal
   tlmgr install physics chemformula
   ```

*Требования: Python 3.11+, R 4.2+, Jupyter 6.0+*