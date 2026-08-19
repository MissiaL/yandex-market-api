# yandex-market-api — Claude/Agent Skill для Yandex Market Partner API

Skill-репозиторий: полный официальный OpenAPI 3.0 спек партнёрского API Яндекс
Маркета (155 путей / 165 операций) + CLI для навигации по нему.

- [SKILL.md](SKILL.md) — точка входа для агента: авторизация, businessId vs campaignId,
  модели размещения, грабли.
- [references/yandex-market-openapi.json](references/yandex-market-openapi.json) — спек,
  собранный из ветки `main` официального репо
  `github.com/yandex-market/yandex-market-partner-api`,
  обогащённый `x-ym-section` (функциональный тег + модели размещения).
- [references/index.md](references/index.md) — плоский индекс всех эндпоинтов по разделам.
- [scripts/lookup_endpoint.py](scripts/lookup_endpoint.py) — `tags` / `search` / `show` по спеку.

## Обновление спека

Спек пересобирается скриптом из внешней обёртки (`../tools/build_spec.py`):

```bash
python3 ../tools/build_spec.py            # скачивает репо + npx @redocly/cli bundle
python3 ../tools/build_spec.py --bundled /path/to/bundled.json  # без сети и node
```

Для бандла мульти-файлового спека нужен Node.js (`npx @redocly/cli`).
