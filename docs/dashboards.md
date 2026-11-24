# Рабочие разделы платформы

Все разделы находятся в защищённой части [app.spy2money.com](https://app.spy2money.com/login) и требуют входа. Общая шапка содержит поиск тикера, профиль и действия текущей страницы: период, сетку, добавление виджетов и обновление.

| Раздел | Адрес | Для чего |
| --- | --- | --- |
| Опционы | [/app/options](https://app.spy2money.com/app/options) | Рыночный опционный поток, карты ордеров, сканер, топ по Net Premium |
| Страница тикера | `/app/options/ticker/<ТИКЕР>` | Поток, страйки, греки, GEX, IV и цена одного инструмента |
| Поток | [/app/flow](https://app.spy2money.com/app/flow) | Сравнение потока премии нескольких тикеров |
| Уровни | [/app/levels](https://app.spy2money.com/app/levels) | Расчётные уровни цены |
| Darkpool | [/app/darkpool](https://app.spy2money.com/app/darkpool) | Внебиржевые сделки акций и ETF |
| Скринер | [/app/screener](https://app.spy2money.com/app/screener) | Отбор тикеров по опционной активности |
| Крипто | [/app/crypto](https://app.spy2money.com/app/crypto) | BTC/ETH опционы, Gamma, волатильность, интрадей |
| Страница монеты | `/app/crypto/ticker/<МОНЕТА>` | График, крипто-виджеты и скринер монет |
| Стратегии | [/app/strategies](https://app.spy2money.com/app/strategies) | Торговые стратегии, статистика, сделки, подписки |
| AI Agent | [/app/ai-agent](https://app.spy2money.com/app/ai-agent) | Чат-аналитик по данным платформы |
| Интеграции | [/app/integrations](https://app.spy2money.com/app/integrations) | Портфель подключённых брокеров |
| Профиль | [/app/profile](https://app.spy2money.com/app/profile) | Аккаунт, подписка, Telegram, уведомления, подключённые AI-агенты |
| Оплата | [/app/payment](https://app.spy2money.com/app/payment) | Продление подписки |

## Опционы

Главный дашборд для обзора рынка опционов США. Типичный порядок работы: оценить общий поток в [Market Netflow V2](./widgets/market-netflow-v2.md) → найти тикеры с концентрацией премии на [картах ордеров](./widgets/options-map.md) и в [топе по Net Premium](./widgets/market-top-net-impact.md) → проверить конкретные сделки в [сканере](./widgets/options-order-flow.md).

## Страница тикера

Открывается из поиска в шапке или по клику на тикер в карточках. Набор карточек по умолчанию: [Ticker Net Prem](./widgets/ticker-net-prem.md), [Ticker Overview Strikes](./widgets/ticker-overview-strikes.md), [Greek Flow](./widgets/ticker-greek-flow.md), [Greek Spot](./widgets/ticker-greek-spot.md), [GEX Levels](./widgets/ticker-gex-levels.md), [Gamma Profile](./widgets/ticker-gamma-profile.md), [IV Term Structure](./widgets/ticker-iv-term-structure.md), [Trade Ideas](./widgets/ticker-trade-ideas.md), [Option Contract](./widgets/ticker-option-contract.md) и [ценовой график](./widgets/ticker-tradingview.md). Состав и размеры карточек можно менять.

## Поток

Карточки потока премии по нескольким тикерам рядом. Каждая карточка сама выбирает свой тикер и период; дата-окно задаётся общим календарём страницы.

## Уровни

[Графики уровней](./widgets/level-chart.md) сопоставляют цену с рассчитанными уровнями: удобно наблюдать удержание, пробой и возврат.

## Darkpool

Внебиржевые сделки акций и ETF: [карты денежного потока](./widgets/darkpool-map.md), [TOP BUY](./widgets/market-darkpool-top-net-map-call.md) / [TOP SELL](./widgets/market-darkpool-top-net-map-put.md), [сканер принтов](./widgets/market-darkpool-flow.md) и [график по тикеру](./widgets/ticker-darkpool-net-prem.md). Денежные показатели относятся к сделкам с акциями, а не к опционам.

## Скринер

[Скринер настроений](./widgets/sentiment-screener.md) сравнивает тикеры по агрегатам опционной активности. Над таблицей есть чипы числовых фильтров; фильтр можно открыть и из заголовка колонки. Пустое значение никогда не проходит активный числовой фильтр.

## Крипто

Дашборд BTC/ETH: [обзор рынка](./widgets/crypto-market.md), [барометр волатильности](./widgets/crypto-radar.md), [Gamma по страйкам](./widgets/crypto-gex.md), [опционный поток](./widgets/crypto-flow.md), [терм-структура IV](./widgets/crypto-volatility.md) и [Crypto Intraday](./widgets/crypto-intraday.md). Страница монеты (`/app/crypto/ticker/BTC` и др.) показывает [график Vela](./widgets/crypto-vela-price.md) и [скринер криптовалют](./widgets/crypto-coin-screener.md); раскладка сохраняется отдельно для каждой монеты.

## Стратегии

Список торговых стратегий со статистикой, историей сделок и подпиской на сигналы.

## Собственные дашборды

Создайте собственный экран и добавьте любые виджеты каталога. Порядок, размеры и настройки сохраняются в аккаунте и синхронизируются между устройствами.

## Ссылка на виджет

В меню «…» любой карточки есть «Копировать ссылку» и «Открыть отдельно». Ссылка открывает один виджет на всю ширину с теми же тикером и периодом. Получателю нужен собственный аккаунт и доступ к платформе; ссылка не передаёт ваши учётные данные или дашборд.

## Период и календарь

- **Относительные пресеты** («Сегодня», «Вчера», «5 дней» и т. д.) пересчитываются при каждом открытии.
- **«По сегодня»** сохраняет только дату начала: конец окна всегда сегодняшний день.
- **Фиксированный диапазон** остаётся неизменным.
- Без полного доступа пресеты привязываются к последнему доступному дню задержанных данных.
