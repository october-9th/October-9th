<h1 align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=32&duration=2200&pause=600&color=3ECF8E&center=true&vCenter=true&repeat=false&width=620&height=60&lines=Tran+Hoang+Viet;Arthur+Tran;Tran+Hoang+Viet+(Arthur)" alt="Tran Hoang Viet (Arthur)" />
</h1>

<p align="center"><code>BACKEND DEVELOPER · HO CHI MINH CITY</code></p>

<p align="center">
  <img src="https://img.shields.io/badge/LANGUAGES-Java%20·%20Python%20·%20Go-3ecf8e?style=flat-square&labelColor=212427" alt="Languages: Java, Python, Go" />
  <img src="https://img.shields.io/badge/STACK-Spring%20Boot%20·%20FastAPI%20·%20MySQL%20·%20RabbitMQ-c9975a?style=flat-square&labelColor=212427" alt="Stack: Spring Boot, FastAPI, MySQL, RabbitMQ" />
  <img src="https://img.shields.io/badge/CERTIFIED-AWS%20Cloud%20Practitioner-3ecf8e?style=flat-square&labelColor=212427" alt="AWS Certified Cloud Practitioner" />
</p>

---

Replaces fragile manual workflows with automated systems that hold under load.

Backend systems in Java/Spring Boot, Python/FastAPI, and Go — built with retries, rollback,
and CI coverage as first-class concerns, not afterthoughts.

`3+ years` · `Currently at Daoukiwoom Innovation` · `Ho Chi Minh City, Vietnam`

---

## § 01 — Measured results

| Metric | Before → After | What that means |
| :--- | :--- | :--- |
| `QUEUE PROCESSING` | 10–15 min → **2–5 min** | Each file clears the queue in minutes, not quarter-hours. |
| `TLS SETUP` | 5–10 min → **<10 sec** | New sites go live secure, without anyone touching a config file. |
| `DAILY THROUGHPUT` | 200–250/day manual → **350–400/day auto + 250/day manual** | Automated processing added new capacity without displacing the manual workflow already in place. |
| `CODE RELIABILITY` | manual QA only → **≥80% covered** | Automated tests catch problems before they reach a live customer. |

Every number above traces to a system I built or own. Nothing here is an estimate.

---

## § 02 — Diagnosing event-loop starvation in a production download queue

`PRODUCTION AUTOMATION` · `Python` `FastAPI` `asyncio`

A backlog of roughly 1,700 waiting tasks brought down to a steady 350–400 processed per day,
without losing retry or backoff guarantees.

The queue lived entirely in process memory with no bound, and task acceptance shared an event
loop with heavy file I/O — so long operations blocked the loop from servicing anything else.
I moved the queue into a database-backed table, kept the accept path thin, and ran the work in
a bounded worker pool.

**Trade-off:** a DB-backed queue costs a write-and-poll cycle per task versus a pure in-memory
hand-off. Durability across restarts and a boundable, visible queue depth were worth more here
than shaving milliseconds off intake. Adding workers alone was rejected — it would have raised
contention on the same unbounded queue instead of fixing the starvation.

`2–5 min per task` · `350–400 tasks/day` · `retry + backoff retained`

---

## § 03 — Designing a zero-touch TLS agent with safe rollback

`SYSTEMS & RELIABILITY` · `Go` `cron` `nginx/apache`

Manual SSL setup, at 5–10 minutes per domain, reduced to under 10 seconds — with unattended
reissue running as a cron-driven agent.

Every domain moves through explicit states — pending, validating, issuing, active, renewing —
so the agent always knows what is safe to do next. Private keys are generated and stored on the
host and never transit the network. Registry writes are atomic, so a crash mid-update can't
leave a domain half-recorded. If a config reload fails after a new certificate is applied, the
agent restores the previous working config automatically.

A simulation harness replays dozens of real-world config patterns — vhosts, aliases, wildcard
entries — without needing live customer domains. It runs in CI and gates merges at ≥80%
statement coverage.

`<10 sec setup` · `≥80% CI statement coverage` · `unattended fleet reissue`

---

## § 04 — Owning the primary operations API for a localization platform

`PLATFORM OWNERSHIP` · `Java 17` `Spring Boot` `MySQL` `RabbitMQ`

A multi-module Spring Boot platform that a localization team opens every day to run production
workflows. I own it end to end: schema design, authentication model, integration layer, and
ongoing operational support.

Its core feature assigns tasks to employees automatically based on capability, availability, and
a configurable rule set. That logic originally lived in MySQL stored procedures written by a
previous developer — hard to read, test, or change safely. I redesigned it into the Java service
layer, which cut task assignment from nearly 10 minutes to about 30 seconds and made the rules
extensible as operations change.

Separate JWT flows cover internal service calls and partner-facing access, so one compromised
credential set can't reach everything. RabbitMQ decouples slow downstream work like Sheets sync
from the request path; Pusher sends state changes to internal dashboards instead of making teams
poll for status.

`~30 sec assignment, down from ~10 min` · `daily production use` · `4 systems integrated`

---

## § 05 — Streaming large files through an async processing API

`DATA PROCESSING` · `Go` `Docker` `OpenAPI`

A Go API that processes ZIP/PSD asset bundles on Synology NAS, sustaining 200–300 requests per
minute at roughly 250ms p99 latency, and cutting manual handling time by more than 95%.

Uploads return a job ID immediately and extraction runs in the background, so large files never
block the request. Files are processed as streams rather than loaded whole into memory, and
batch PSD-to-JPG conversion runs in chunks — memory stays flat regardless of file size. Endpoints
are JWT-secured with an OpenAPI spec so consuming teams have a real contract, and Docker keeps
deployment consistent across environments.

`~35 sec per conversion, down from ~2 min` · `~250ms p99` · `200–300 req/min` · `flat memory`

---

## § 06 — Other work

**HR Intake Platform** — `FastAPI` `Next.js` `MongoDB` `Celery`
Routes Vietnamese and Korean forms into separate Google Sheets pipelines via a shared FastAPI backend.

Earlier work: insurance operations backend (`Spring MVC`), municipal services platform (`Spring Boot` · `React`).

---

## § 07 — Capabilities

**`01` Designing reliable, scalable backend systems**
Architecting services in Java/Spring Boot, Python/FastAPI, and Go that keep working as load and data volume grow.
→ Queue redesign cut per-task time from 10–15 min to 2–5 min, sustaining 350–400 tasks/day

**`02` Building secure APIs and service integrations**
Designing authenticated, documented APIs that connect cleanly to the systems around them.
→ Dual JWT auth, RabbitMQ, Google Sheets, and NAS integrations shipped to production

**`03` Improving performance, stability, and observability**
Finding where a system is actually spending its time, then removing the bottleneck.
→ Removed a 1,700-task backlog by fixing the bottleneck, not adding hardware

**`04` Diagnosing and resolving production issues**
Tracing symptoms — backlogs, memory pressure, slow responses — back to their root cause under real load.
→ Traced event-loop starvation to an unbounded in-memory queue and fixed it at the source

**`05` Designing efficient data-processing pipelines**
Building database-backed queues and streaming I/O that handle high volume without blocking.
→ NAS file API sustains 200–300 requests/minute, cutting manual handling time over 95%

**`06` Making practical engineering trade-offs**
Weighing latency, durability, cost, and delivery time to pick the option that fits the constraint, not the trendiest one.
→ Chose a bounded DB-backed queue over "just add more workers" to fix root cause, not symptoms

**`07` Working across product, ops, and engineering teams**
Shipping backend systems that non-engineering teams — localization, HR, operations — depend on directly.
→ Ops and intake platforms in daily use by localization and HR teams, in Vietnamese and Korean

---

## § 08 — Contact

Let's talk about what you're building.

- Email — [dev@hermesxai.com](mailto:dev@hermesxai.com)
- LinkedIn — [viet-tran-179bb9218](https://www.linkedin.com/in/viet-tran-179bb9218/)
- Location — Ho Chi Minh City, Vietnam

---

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=October-9th&layout=compact&langs_count=8&hide=html,css,scss&title_color=3ecf8e&text_color=e6e6e6&icon_color=c9975a&bg_color=111214&hide_border=true&custom_title=Most%20used%20languages" alt="Most used languages" />
</p>

<p align="center"><sub><code>TRAN HOANG VIET — BACKEND DEVELOPER — © 2026</code></sub></p>
<p align="center"><sub>Case studies omit proprietary code and client data.</sub></p>
