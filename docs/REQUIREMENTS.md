# Requirements & Scoping (v1.0)

## Problem Statement

Build a production ready system that demonstrates senior full stack engineering capabilities and learning AI software engineering by building.

## MVP Scope

By the end of v1.0 developement, a user shuold be able to do the following

- Register or log in
- browse a catalog
- search semantically
- add items to cart
- complete checkout with a simulated payment

## Explicitly deferred

Below are deferred features that can be completed after v1.0 developement

- reviews
- admin dashboard
- recommendation refinement
- multi-currency
- refunds

## Non functional Requirements (NFR)

| Requirement          | Target                                                 | Why it matters                                                            |
| -------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------- |
| Checkout latency     | p95 < 500ms                                            | Users abandon carts past this                                             |
| Catalog read latency | p95 < 150ms                                            | High-traffic, read-heavy path                                             |
| Availability         | 99.9% (=8.7h downtime/yr)                              | Realistic for a learning project and forces one to think about redundancy |
| Consistency          | Strong for payments, eventual for catalog/search index | Different parts of the system need different guarantees                   |

## Capacity Estimate

Assume: 10,000 daily active users, 5 catalog views/session, 1 search/session

- ~50,000 catalog reads/day, ~10,000 searches/day
- Average ~0.6 req/s, peak (10x average) ~6 req/s
- Catalog DB: 50,000 products \* 2KB = 100MB (fits comfortably in a single Postgres instance + cache)
- Orders: 500 orders/day \* 5KB = negligible storage; growth is linear, no sharding needed for years
