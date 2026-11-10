# Темы-триггеры

Архитектурное «мясо» — то, чем оперируешь, когда рисуешь систему на доске. Как работать с топиками — см. [README теории](../README.md).
Порядок: сначала **must** (всплывает почти в каждой задаче), потом **should**, **nice** — когда остаётся время или идёшь в staff+.

---

# Must

## Нефункциональные требования (NFR)
*На доске: колонка требований, этап 1.*
- latency / throughput
- SLA / SLO / availability
- scalability (вертикальная vs горизонтальная)
- consistency vs availability (CAP)
- cost awareness
- security & compliance

## Оценка нагрузки
*На доске: фрейм оценки нагрузки, этап 1.*
- MAU → DAU → RPS, средний vs пиковый
- объём данных и его рост
- соотношение чтение / запись
- шпаргалка — в [`playbook.md`](playbook.md#оценка-нагрузки-входит-в-этап-1)

## Базы данных
*На доске: выбор хранилищ на C2.*
- [выбор БД под задачу](https://system-design.space/chapter/database-selection-framework)
- OLTP vs OLAP
- read-heavy vs write-heavy
- когда индексы вредят
- composite indexes
- hot keys
- реплика лаг и его последствия
- шардинг: по чему и какие проблемы

## Кэширование
*На доске: кэш на C2 + горлышки.*
- где кэшировать: CDN / reverse proxy / app / DB
- write-through / write-back / cache-aside
- инвалидация кэша
- Redis vs Memcached

## Асинхронщина и очереди
*На доске: пунктирные стрелки и очереди на C2.*
Главное — модель мышления, а не список отличий.
- когда синхрон, когда async
- queue vs log (event streaming)
- ordering
- retention
- replay
- consumer groups
- exactly-once / at-least-once (почему exactly-once почти никогда нет)
- дедупликация задач
- идемпотентные воркеры

1. «У тебя события оплаты и уведомления. Какую очередь выберешь и почему?»

## Надёжность и отказоустойчивость
*На доске: этап «запас» — что будет при отказе каждого контейнера.*
- retries с backoff + jitter
- circuit breaker
- timeouts
- graceful degradation
- bulkheads
- хелсчеки и heartbeat

---

# Should

## API & контракты
*На доске: только если спросили или осталось время.*
- REST vs GraphQL vs gRPC
- версионирование API
- идемпотентность
- пагинация (offset vs cursor)
- rate limiting / throttling
- backward compatibility

## Observability
*На доске: этап «запас».*
- structured logs
- метрики (RED / USE)
- трассировка
- алерты: когда и на что

## Миграции и эволюция системы
- zero-downtime migrations
- feature flags
- blue/green vs canary
- как менять схему БД без даунтайма

---

# Nice

## Архитектурные подходы (DDD + event-driven)
1. Когда DDD — оверхед?
2. Как bounded context ложится на микросервисы?
3. Что делать, если бизнес-логика простая?
4. Repository на примере abstraction над storage: почему не дергать ORM напрямую?
5. Entity vs Value Object
6. Event vs Command: CreateOrder (command) vs OrderCreated (event)
7. PubSub: producer не знает consumer + слабая связность системы
8. Eventual Consistency: данные сходятся "не сразу" + между сервисами нет транзакций. Пример: пользователь создал заказ, но не видит его сразу — почему?
9. Outbox Pattern

Ссылочки, пока работают
- [ddd](https://vaadin.com/blog/ddd-part-1-strategic-domain-driven-design)
- [event-driven](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven)

## Kubernetes
- зачем вообще k8s
- pod vs deployment vs statefulset
- config & secrets
- liveness / readiness
- scaling стратегии
- как сервисы находят друг друга

1. Почему нельзя просто увеличить replicas и всё станет хорошо?

## Облака
- managed vs self-hosted
- vendor lock-in
- стоимость
- сети (VPC, private/public)
- IAM и безопасность

1. Что ты возьмёшь managed, а что оставишь самописным — и почему?
