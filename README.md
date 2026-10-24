# ai-toolkit

Набор навыков (Agent Skills), который устанавливается как плагин в **Claude Code** и **Codex**.
Один и тот же каталог `skills/` используется обоими агентами.

## Структура

```
ai-toolkit/
├── .claude-plugin/
│   ├── plugin.json        # манифест плагина Claude Code
│   └── marketplace.json   # маркетплейс Claude Code
├── .codex-plugin/
│   └── plugin.json        # манифест плагина Codex
├── .agents/plugins/
│   └── marketplace.json   # маркетплейс Codex
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

## Установка

### Claude Code

```
/plugin marketplace add grind-t/ai-toolkit
/plugin install toolkit@toolkit
```

Локально: `/plugin marketplace add ./ai-toolkit`.

### Codex

```bash
codex plugin marketplace add grind-t/ai-toolkit
```

Затем установите `toolkit` из каталога плагинов (`/plugins` в Codex).
Локально: `codex plugin marketplace add ./ai-toolkit`.

Навыки доступны с префиксом плагина: `/toolkit:<skill-name>`, например `/toolkit:step-by-step`.

## Добавление навыка

1. Создайте `skills/<skill-name>/SKILL.md`.
2. Во frontmatter укажите `name` (kebab-case, совпадает с именем папки) и `description` — что делает навык и когда его применять.
3. Поднимите `version` в обоих `plugin.json`.

```markdown
---
name: my-skill
description: Что делает навык и когда его использовать.
---

# Инструкции
...
```

## Навыки

| Навык | Описание |
|---|---|
| `step-by-step` | Пошаговая работа: один шаг → обсуждение → выполнение после явного «ок» → следующий шаг |
