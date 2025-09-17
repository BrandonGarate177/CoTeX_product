# Backend Architecture

The CoTeX backend is a high-performance Go service that powers real-time GitHub integration, subscriptions (Stripe), and WebSocket messaging for the desktop app.

## Tech Stack

| Area     | Choice                           |
| -------- | -------------------------------- |
| Language | Go 1.23+                         |
| DB       | Supabase (PostgreSQL + Realtime) |
| Auth     | Supabase JWT                     |
| Payments | Stripe (Checkout + Webhooks)     |
| Realtime | WebSocket hub (custom)           |
| Deploy   | Docker → Google Cloud Run        |
| Logs     | Zerolog (structured JSON)        |

## Architecture & Capabilities

* **GitHub Integration**

  * Secure webhook endpoints (HMAC SHA-256/SHA-1 validation)
  * Event storage (TTL \~2 weeks) + retrieval
  * Realtime broadcast to connected clients
  * Per-user repo subscriptions

* **Subscriptions**

  * Stripe Checkout session creation
  * Webhook handling for lifecycle events
  * Tiering: Free vs Pro (customer sync)

* **Realtime**

  * WebSocket hub with per-user channels
  * Origin validation + CORS
  * Ping/Pong health checks
  * Graceful client register/unregister

* **Security & Ops**

  * JWT verification (Supabase)
  * Rate limiting (configurable)
  * CORS allowlist
  * Graceful shutdown & health checks
  * Structured logs + request correlation

## REST API

### Public

| Method | Path                             | Description                                  |
| ------ | -------------------------------- | -------------------------------------------- |
| POST   | `/api/webhooks/github/{repo_id}` | GitHub webhook receiver (HMAC required)      |
| POST   | `/webhooks/stripe`               | Stripe webhook receiver (signature required) |

### Authenticated

| Method   | Path                                     | Description                          |
| -------- | ---------------------------------------- | ------------------------------------ |
| GET      | `/ws`                                    | WebSocket upgrade endpoint           |
| GET/POST | `/api/repos`                             | List / create tracked repos for user |
| GET      | `/api/github-events`                     | Paginated GitHub event history       |
| GET      | `/api/github-events/recent`              | Recent event IDs for polling         |
| GET      | `/api/github-events/event?id={event_id}` | Fetch specific event                 |
| POST     | `/api/checkout`                          | Create Stripe Checkout session       |

> Auth: Bearer token (Supabase JWT) for all **Authenticated** routes.


## WebSocket

* **Auth:** `Authorization: Bearer <SUPABASE_JWT>` header on the upgrade request
* **Events:** server broadcasts parsed GitHub events and subscription updates to user channels.


### License

All packaged builds are © 2025 Brandon Garate.
Distributed binaries are for personal or team use only. Please see the main CoTeX repository for source code licensing terms.

### Support

For issues, feature requests, or contributions, please visit [CoTeX.md/Contact](https://cotex-md.netlify.app/contact)
