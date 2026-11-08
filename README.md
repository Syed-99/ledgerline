# Ledgerline

A subscription billing and payments engine for online businesses: multi-tenant accounts, a double-entry ledger, subscriptions, usage-based billing, invoices, webhooks, and an AI assistant that answers billing questions from a business's own data.

> Status: early development. Built in public, one module at a time.

## Why

Billing looks simple until money goes wrong: a double charge, a lost refund, a proration off by one day. Ledgerline is built around one rule: **every money movement is a balanced ledger entry, written once, safe to retry.**

## Modules and roadmap

| # | Module | What it does | Key engineering ideas | Status |
|---|---|---|---|---|
| 1 | Accounts & auth | Businesses (tenants), users, roles, API keys | Tenant isolation (Postgres RLS), RBAC, hashed API keys | In progress |
| 2 | Ledger & payments | Charges, refunds, payouts, balances | Double-entry ledger, row locks, idempotency keys | Planned |
| 3 | Subscriptions | Plans, trials, upgrades, downgrades, cancellations | Proration, state machines, time-based logic | Planned |
| 4 | Usage metering | Record usage events, bill per unit | High-volume ingestion, batching, aggregation | Planned |
| 5 | Invoices & tax | Monthly invoices, PDF, tax per country | Scheduled jobs, document generation, rounding rules | Planned |
| 6 | Webhooks & dunning | Event delivery to customers, retries for failed payments | Queues (BullMQ), exponential backoff, dead-letter queue, signatures | Planned |
| 7 | AI billing assistant | "Why was this customer charged twice?" answered from the business's own data | RAG (pgvector embeddings), tool calls, Python FastAPI service | Planned |
| 8 | Dashboard | Web panel for businesses | Auth flows, charts, API client | Planned |

## Stack

- **API:** TypeScript, Node.js, Fastify
- **Database:** PostgreSQL 16 + pgvector
- **Queues and cache:** Redis, BullMQ
- **AI service:** Python, FastAPI (module 7)
- **Tests:** Vitest
- **Local setup:** Docker Compose

## Run locally

```bash
cp .env.example .env
npm install
npm run db:up        # starts Postgres and Redis in Docker
npm run dev          # API on http://localhost:3000
npm test
```

Check: `GET http://localhost:3000/health` returns `{"status":"ok"}`.

## Data

All data is fake seed data. Ledgerline never stores real people's personal or card data.

## License

MIT
