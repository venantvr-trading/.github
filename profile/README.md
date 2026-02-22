# venantvr.trading

Plateforme de trading algorithmique crypto multi-exchange (Binance, Gate.io, KuCoin, OKX, Bybit) avec architecture événementielle.

## Repos

### Core

[![Python.Trading.Risk](https://img.shields.io/badge/Python.Trading.Risk-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Risk) <sup>privé</sup>
*Python / ccxt* — Bot de trading monolithique : allocation multi-pool, stop-loss/take-profit dynamique, sizing de position, gestion de sorties, intégration multi-exchange (ccxt), persistance SQLite, commandes Telegram. Configuration Pydantic, optimisation Optuna.

[![Python.PubSub.Risk](https://img.shields.io/badge/Python.PubSub.Risk-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.PubSub.Risk) <sup>privé</sup>
*Python / Socket.IO* — Refactoring événementiel du monolithe : **29 agents autonomes** (achat, vente, indicateurs, monitoring, capital...), **43 événements Pydantic** typés, orchestrateur pub/sub, 172 tests. Architecture CQRS avec agents spécialisés (BuyConditionEvaluator, SaleExecution, CapitalRefresh, PanicSellCommand...).

### Librairies

[![Python.Trading.Objects](https://img.shields.io/badge/Python.Trading.Objects-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Objects) <sup>public</sup>
*Python / Pydantic* — Value objects DDD immuables : Token, USD, Price, Percentage avec opérateurs arithmétiques surchargés, conversions automatiques, factory BotPair, sérialisation JSON. 73 tests unitaires.

[![Python.Trading.Indicators](https://img.shields.io/badge/Python.Trading.Indicators-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Indicators) <sup>public</sup>
*Python / pandas / numpy* — Indicateurs techniques modulaires : RSI multi-timeframe, VIX (volatilité), patterns de bougies (candlestick), détection de drops, passthrough. Classe abstraite Indicator extensible.

[![Python.Trading.Tools](https://img.shields.io/badge/Python.Trading.Tools-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Tools) <sup>public</sup>
*Python* — Utilitaires zéro dépendance : décorateurs de cache dynamique bi-format (JSON/Pickle avec chemins templates), logger structuré fichier/console, redirection de stdout pour capture.

[![Python.Trading.PubSub](https://img.shields.io/badge/Python.Trading.PubSub-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.PubSub) <sup>public</sup>
*Python / Flask / Socket.IO* — Client pub/sub spécialisé trading : routage par topics, handlers typés, file d'attente de messages thread-safe, reconnexion automatique, mode hybride HTTP/WebSocket. Module positions intégré.

### Monitoring Telegram

[![Python.Trading.Telegram.Declarative](https://img.shields.io/badge/Python.Trading.Telegram.Declarative-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Telegram.Declarative) <sup>public</sup>
*Python* — Framework Telegram déclaratif en Clean Architecture : composants séparés (Client, Sender, Receiver, Service), retry automatique avec backoff exponentiel, file de messages asynchrone, historique de conversations persisté.

[![Python.Trading.Telegram.Annotations](https://img.shields.io/badge/Python.Trading.Telegram.Annotations-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.Trading.Telegram.Annotations) <sup>public</sup>
*Python* — Bibliothèque Telegram par décorateurs `@command` : menus inline dynamiques, prompts multi-étapes, configuration par annotations, protocoles typés, gestion de sessions HTTP.

### Outillage événementiel

[![Python.PubSub.Scanner](https://img.shields.io/badge/Python.PubSub.Scanner-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.PubSub.Scanner) <sup>public</sup>
*Python* — Scanner d'introspection de code événementiel : analyse statique des agents et événements, génération de graphes DOT (flux, hiérarchie), détection d'anomalies, collections Postman automatiques, mode continu ou one-shot. CLI `pubsub-scanner`.

[![Python.PubSub.DevTools](https://img.shields.io/badge/Python.PubSub.DevTools-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://github.com/venantvr-trading/Python.PubSub.DevTools) <sup>public</sup>
*Python / Flask* — Suite DevTools complète en 4 modules : **record/replay** d'événements, **mock exchange** (simulation avec scénarios de marché), **chaos engineering** (injection de pannes, délais, corruption), **scenario testing** (assertions sur flux). Dashboard web intégré, CLI Click.

## Évolution architecturale

```mermaid
graph TD
    M[Python.Trading.Risk<br/><i>Monolithe</i>] -->|refactoring événementiel| E[Python.PubSub.Risk<br/><i>29 agents · 43 événements Pydantic</i>]

    E --> SC[Scanner<br/><i>Introspection du code → graphes DOT</i>]
    E --> DT[DevTools]

    DT --> R[Record / Replay]
    DT --> MX[Mock Exchange]
    DT --> CH[Chaos Engineering]
    DT --> ST[Scenario Testing]
```

## Stack

[![Stack](https://skillicons.dev/icons?i=python,docker,redis,rabbitmq,linux,git&theme=dark)](https://skillicons.dev)


- **Python** exclusivement, licences MIT
- **5 exchanges** supportés via ccxt : Binance, Gate.io, KuCoin, OKX, Bybit
- **Pydantic** pour le typage strict des 43 événements
- **Socket.IO** pour le messaging temps réel inter-agents
- **Telegram** pour le monitoring, le contrôle et les alertes
- **SQLite** pour la persistance des positions et de l'historique
