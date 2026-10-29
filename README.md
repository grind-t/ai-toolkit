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
├── hooks/
│   └── hooks.json         # общий для обоих агентов: SessionStart подгружает communication-principles
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
Хук плагина Codex не запускает без доверия: одобрите его через `/hooks`.
Локально: `codex plugin marketplace add ./ai-toolkit`.

Навыки доступны с префиксом плагина: `/toolkit:<skill-name>`, например `/toolkit:step-by-step`.

## Добавление навыка

1. Создайте `skills/<skill-name>/SKILL.md`.
2. Во frontmatter укажите `name` (kebab-case, совпадает с именем папки) и `description` — что делает навык и когда его применять.
3. Если навык должен вызываться только вручную, добавьте во frontmatter `disable-model-invocation: true` (Claude Code) и создайте `skills/<skill-name>/agents/openai.yaml` с `policy.allow_implicit_invocation: false` (Codex).
4. Поднимите `version` в обоих `plugin.json`.

```markdown
---
name: my-skill
description: Что делает навык и когда его использовать.
---

...
```

## Навыки

| Навык | Описание |
|---|---|
| `step-by-step` | Пошаговая работа: один шаг → обсуждение → выполнение после явного «ок» → следующий шаг (вызывается вручную) |
| `communication-principles` | Принципы общения: без угодничества, не бояться спорить, останавливаться и сообщать о препятствиях (Andon cord). Подгружается хуком в начале каждой сессии |
| `context-principles` | Принципы написания текста для LLM: ссылки на известные концепции вместо пояснений, принципы вместо запретов (pit of success) |
| `planning-principles` | Принципы планирования: выявить препятствия задачи по Prerequisite Tree Голдратта (вызывается вручную) |
