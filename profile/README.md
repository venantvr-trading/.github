# venantvr.trading

Plateforme de trading algorithmique crypto multi-exchange (Binance, Gate.io, KuCoin, OKX, Bybit) avec architecture événementielle.

## Repos

### Core

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Risk` | Python | Bot de trading monolithique : allocation multi-pool, stop-loss/take-profit dynamique, sizing de position, gestion de sorties, intégration multi-exchange (ccxt), persistance SQLite, commandes Telegram |
| `Python.PubSub.Risk` | Python | Refactoring événementiel du monolithe : **29 agents autonomes** (achat, vente, indicateurs, monitoring, capital...), **43 événements Pydantic** typés, orchestrateur pub/sub, 172 tests. Architecture CQRS avec agents spécialisés (BuyConditionEvaluator, SaleExecution, CapitalRefresh, PanicSellCommand...) |

### Librairies

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Objects` | Python | Value objects DDD immuables : Token, USD, Price, Percentage avec opérateurs arithmétiques surchargés, conversions automatiques, 73 tests unitaires |
| `Python.Trading.Indicators` | Python | Indicateurs techniques : RSI multi-timeframe, VIX, patterns de bougies (candlestick), détection de drops, passthrough. Basé sur pandas/numpy |
| `Python.Trading.Tools` | Python | Utilitaires partagés : cache dynamique bi-format (JSON/Pickle), logger structuré, redirection de stdout pour capture |
| `Python.Trading.PubSub` | Python | Client pub/sub Socket.IO spécialisé trading : handlers typés, file d'attente de messages, reconnexion automatique, module positions |

### Monitoring Telegram

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.Trading.Telegram.Declarative` | Python | Bot Telegram déclaratif : retry automatique, queuing de messages, historique de conversations persisté, notifications structurées |
| `Python.Trading.Telegram.Annotations` | Python | Bot Telegram par décorateurs Python : menus inline dynamiques, prompts multi-étapes, configuration par annotations, protocoles typés |

### Outillage événementiel

| Repo | Stack | Description |
|------|-------|-------------|
| `Python.PubSub.Scanner` | Python | Scanner d'introspection de code événementiel : analyse statique des agents et événements, génération de graphes DOT (flux, hiérarchie), collections Postman automatiques, mode continu ou one-shot |
| `Python.PubSub.DevTools` | Python | Suite DevTools complète : **record/replay** d'événements (enregistrement + rejeu configurable), **mock exchange** (simulation d'exchange avec scénarios), **chaos engineering** (injection de pannes), **scenario testing** (assertions sur flux), dashboard web |

## Évolution architecturale

```
Python.Trading.Risk (monolithe)
        │
        │ refactoring événementiel
        ▼
Python.PubSub.Risk (29 agents, 43 événements Pydantic)
        │
        ├── Scanner ─────── Introspection du code → graphes DOT
        │                   Analyse statique des flux d'événements
        │
        └── DevTools ────── Record/Replay d'événements
                            Mock Exchange (simulation)
                            Chaos Engineering (injection de pannes)
                            Scenario Testing (assertions)
```

## Stack

- **Python** exclusivement, licences MIT
- **5 exchanges** supportés via ccxt : Binance, Gate.io, KuCoin, OKX, Bybit
- **Pydantic** pour le typage strict des 43 événements
- **Socket.IO** pour le messaging temps réel inter-agents
- **Telegram** pour le monitoring, le contrôle et les alertes
- **SQLite** pour la persistance des positions et de l'historique
