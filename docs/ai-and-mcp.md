# AI-аналитика и MCP

Spy2Money даёт два способа анализировать данные с помощью AI: встроенный **AI Agent** в приложении и **MCP-сервер**, который подключает данные платформы к вашему собственному AI-ассистенту.

## AI Agent в приложении

[/app/ai-agent](https://app.spy2money.com/app/ai-agent) — чат-аналитик, который получает данные платформы на сервере. Попросите разобрать тикер, рыночный поток или darkpool-активность. Ответ отображается по мере генерации, в процессе видно, какие инструменты использует агент. История чата не сохраняется в браузере.

Многие карточки также предлагают AI-обзор текущего вида: агент получает тот же тикер, режим и фильтры, что вы видите на экране.

## AI в Strategy Builder

В меню [Strategy Builder](./widgets/strategy-builder.md) действие «Спросить AI» помогает подобрать опционную позицию: укажите направление, срок и допустимый убыток. При каждом сообщении помощник заново получает выбранную экспирацию и текущий состав модели. Предложенные ноги добавляются в модель **только после вашего подтверждения** и только для моделирования — брокерские ордера не отправляются.

## MCP-сервер Spy2Money

[Model Context Protocol](https://modelcontextprotocol.io/) — открытый стандарт подключения инструментов к AI-ассистентам. MCP-сервер Spy2Money даёт вашему агенту доступ к рыночным данным и вашему аккаунту в режиме **только чтения**.

**Адрес сервера:** `https://mcp.spy2money.com/mcp`

### Подключение

**Claude (claude.ai и Claude Desktop)**

1. Настройки → Connectors → Add custom connector.
2. Вставьте `https://mcp.spy2money.com/mcp` и сохраните.
3. Нажмите Connect, войдите в аккаунт Spy2Money и подтвердите доступ.

Подробнее — [инструкция Anthropic по custom connectors](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp).

**Claude Code**

```bash
claude mcp add --transport http spy2money https://mcp.spy2money.com/mcp
```

Затем в сессии выполните `/mcp` и пройдите авторизацию. См. [документацию Claude Code](https://docs.claude.com/en/docs/claude-code/mcp).

**Codex**

```bash
codex mcp add spy2money --url https://mcp.spy2money.com/mcp
```

```bash
codex mcp login spy2money
```

См. [документацию Codex](https://developers.openai.com/codex/mcp).

Клиент сам обнаружит вход через OAuth: откроется страница Spy2Money, где вы входите в аккаунт и подтверждаете перечисленные права. Пароль клиенту не передаётся.

### Права и безопасность

- Все инструменты **только читают** данные: агент не может торговать, менять настройки или дашборды.
- Права запрашиваются явно: рыночные данные, стратегии, ваши дашборды, история сигналов.
- Данные аккаунта (дашборды, подписки, сигналы) всегда привязаны к вашему аккаунту, а не к аргументу запроса.
- Подключить агента может любой аккаунт Spy2Money; рыночные данные выдаются по тем же правилам доступа, что и в приложении.
- **Отзыв доступа:** Профиль → «Подключённые агенты» — отзовите одного агента или всех сразу. Следующий запрос агента потребует повторной авторизации.

### Инструменты

| Группа | Инструменты |
| --- | --- |
| Анализ тикера | `analyze_ticker` — полный options-first отчёт по тикеру; `options_analysis`, `ticker_trade_ideas` |
| Поток по тикеру | `ticker_net_premium`, `ticker_net_prem_ticks`, `ticker_flow_chart`, `ticker_flow_by_strike`, `ticker_flow_per_expiry`, `ticker_expiry_breakdown`, `flow_summary` |
| Греки и Gamma | `ticker_greek_exposure`, `ticker_greek_flow`, `ticker_greek_spot`, `ticker_gamma_profile`, `ticker_gex_levels`, `ticker_max_pain` |
| Волатильность | `ticker_iv_term_structure`, `ticker_interpolated_iv` |
| Цепочки и контракты | `ticker_option_chains`, `ticker_atm_chains`, `ticker_option_contract_intraday`, `ticker_option_contract_surface` |
| Цена и уровни | `ticker_price_candles`, `ticker_levels_widget`, `support_resistance_levels` |
| Darkpool | `ticker_darkpool_premium`, `market_top_map_widget` (режим darkpool) |
| Рынок | `market_overview`, `market_tide`, `market_netflow_v2`, `market_expiry_flow`, `market_top_net_impact`, `market_sector_tide`, `market_sector_etfs`, `market_etf_tide`, `market_correlations`, `market_exposure_widget` |
| Поиск потока | `market_options_flow`, `options_flow_search`, `market_flow_alerts`, `market_flow_scanner_widget`, `market_multi_leg`, `market_option_screener`, `market_screener` |
| Крипто | `crypto_options_widget` — BTC/ETH: рынок, барометр, GEX, поток, волатильность |
| Новости и справка | `market_news`, `ticker_list` |
| Аккаунт | `my_dashboards`, `my_subscriptions`, `my_signal_history` |

Каждый ответ содержит данные, метку времени `as_of`, оценку качества и ссылки на методологию. Если данные устарели, имеют пропуски или помечены как `limited`, корректный агент не делает по ним направленный вывод.

### Примеры запросов

- «Проанализируй NVDA за сегодня по опционному потоку».
- «Какие сектора получают больше всего бычьей премии?»
- «Покажи уровни GEX для SPY и где максимальная концентрация Gamma».
- «Сравни волатильность BTC и ETH по срокам».
- «Какие у меня сохранены дашборды?»

> Агент формулирует наблюдения и гипотезы, а не торговые рекомендации. Проверяйте `as_of` и ограничения в ответе.
