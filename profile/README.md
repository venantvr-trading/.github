# venantvr.trading

Plateforme de trading algorithmique crypto multi-exchange (Binance, Gate.io, KuCoin, OKX, Bybit).

## Repos

### Core

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Risk` | Python | Bot de trading : allocation multi-pool, stop-loss/take-profit, sizing dynamique, SQLite |
| `Python.PubSub.Risk` | Python | Version event-driven : 29 agents autonomes, 43 events Pydantic, 172 tests |

### Librairies

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Objects` | Python | Value objects DDD (Token, USD, Price), opérateurs arithmétiques, 73 tests |
| `Python.Trading.Indicators` | Python | RSI, VIX, patterns de bougies, détection de drops (pandas/numpy) |
| `Python.Trading.Tools` | Python | Cache dynamique (JSON/Pickle), logging avancé, redirection stdout |
| `Python.Trading.PubSub` | Python | Client pub/sub Socket.IO pour la communication inter-composants |

### Monitoring

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Telegram.Declarative` | Python | Bot Telegram déclaratif : retry, queuing, historique de conversations |
| `Python.Trading.Telegram.Annotations` | Python | Bot Telegram par décorateurs : menus inline, prompts multi-étapes |

### Outillage event-driven

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.PubSub.Scanner` | Python | Scanner de code : détection d'events, graphes DOT, collections Postman |
| `Python.PubSub.DevTools` | Python | Visualisation de flux, record/replay, mock exchange, chaos engineering |

## Évolution architecturale

```
Python.Trading.Risk (monolithe)
        |
        | refactoring event-driven
        v
Python.PubSub.Risk (29 agents, 43 events)
        |
        +-- Scanner (introspection du code)
        +-- DevTools (visualisation, replay, mock, chaos)
```

## Stack

- **Python** exclusivement, MIT-licensed
- **5 exchanges** supportés : Binance, Gate.io, KuCoin, OKX, Bybit
- **Pydantic** pour le typage des events
- **Socket.IO** pour le messaging temps réel
- **Telegram** pour le monitoring et le contrôle
