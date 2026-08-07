<h1 align="center">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=30&duration=2200&pause=600&color=3ECF8E&center=true&vCenter=true&repeat=false&width=560&height=52&lines=Tran+Hoang+Viet;Arthur+Tran;Tran+Hoang+Viet+(Arthur)" alt="Tran Hoang Viet (Arthur)" />
</h1>

<p align="center"><code>BACKEND DEVELOPER&nbsp; ·&nbsp; HO CHI MINH CITY&nbsp; ·&nbsp; 3+ YEARS</code></p>

<p align="center"><b>Replaces fragile manual workflows with automated systems that hold under load.</b></p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/Go-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/Python-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/Spring_Boot-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/FastAPI-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/MySQL-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/RabbitMQ-212427?style=flat-square" />
  <img src="https://img.shields.io/badge/Docker-212427?style=flat-square" />
</p>

<br />

### Measured results

| | Before | After |
| :--- | :--- | :--- |
| Queue processing | 10–15 min | **2–5 min** per task |
| TLS setup | 5–10 min | **<10 sec**, unattended |
| Daily throughput | 200–250 manual | **+350–400 automated** |
| Code reliability | manual QA only | **≥80%** CI coverage |

<sub>Every number traces to a system I built or own. No estimates.</sub>

<br />

### Selected work

<details>
<summary><b>Event-loop starvation in a production download queue</b> &nbsp;<code>Python · FastAPI · asyncio</code></summary>

<br />

A 1,700-task backlog brought down to a steady 350–400 processed per day, with retry and backoff intact.

The queue lived in process memory with no bound, and task acceptance shared an event loop with heavy file I/O — long operations blocked the loop from servicing anything else, including its own bookkeeping. I moved the queue into a database-backed table, kept the accept path thin, and ran the work in a bounded worker pool.

**Trade-off** — a DB-backed queue costs a write-and-poll cycle per task versus a pure in-memory hand-off. Durability across restarts and a boundable, visible queue depth were worth more than shaving milliseconds off intake. Adding workers alone was rejected: it raises contention on the same unbounded queue instead of fixing the starvation.

`2–5 min per task` &nbsp;`350–400 tasks/day` &nbsp;`retry + backoff retained`

</details>

<details>
<summary><b>Zero-touch TLS agent with safe rollback</b> &nbsp;<code>Go · cron · nginx/apache</code></summary>

<br />

Manual SSL setup at 5–10 minutes per domain, reduced to under 10 seconds — with unattended reissue running as a cron-driven agent.

Every domain moves through explicit states (pending → validating → issuing → active → renewing), so the agent always knows what is safe to do next. Private keys are generated and stored on the host and never transit the network. Registry writes are atomic, so a crash mid-update can't leave a domain half-recorded. If a config reload fails after a new certificate is applied, the previous working config is restored automatically.

A simulation harness replays dozens of real config patterns — vhosts, aliases, wildcards — without touching live customer domains. It runs in CI and gates merges at ≥80% statement coverage.

`<10 sec setup` &nbsp;`≥80% CI coverage` &nbsp;`unattended fleet reissue`

</details>

<details>
<summary><b>Primary operations API for a localization platform</b> &nbsp;<code>Java 17 · Spring Boot · MySQL · RabbitMQ</code></summary>

<br />

A multi-module Spring Boot platform a localization team opens every day to run production workflows. I own it end to end: schema, auth model, integration layer, ongoing operational support.

Its core feature assigns tasks to employees automatically by capability, availability, and a configurable rule set. That logic originally lived in MySQL stored procedures written by a previous developer — hard to read, test, or change safely. I redesigned it into the Java service layer: task assignment went from nearly 10 minutes to about 30 seconds, and the rules became extensible as operations change.

Separate JWT flows cover internal and partner-facing access, so one compromised credential set can't reach everything. RabbitMQ decouples slow downstream work like Sheets sync from the request path; Pusher sends state changes to internal dashboards instead of making teams poll.

`~30 sec assignment, from ~10 min` &nbsp;`daily production use` &nbsp;`4 systems integrated`

</details>

<details>
<summary><b>Streaming large files through an async processing API</b> &nbsp;<code>Go · Docker · OpenAPI</code></summary>

<br />

A Go API processing ZIP/PSD asset bundles on Synology NAS at 200–300 requests/minute, ~250ms p99, cutting manual handling time by more than 95%.

Uploads return a job ID immediately and extraction runs in the background, so large files never block the request. Files are processed as streams rather than loaded whole into memory, and batch PSD-to-JPG conversion runs in chunks — memory stays flat regardless of file size. Endpoints are JWT-secured with an OpenAPI spec so consuming teams get a real contract; Docker keeps deployment consistent across environments.

`~35 sec per conversion, from ~2 min` &nbsp;`~250ms p99` &nbsp;`200–300 req/min` &nbsp;`flat memory`

</details>

<br />

### What I do

| | Proof |
| :--- | :--- |
| Reliable, scalable backend systems | Queue redesign: 10–15 min → 2–5 min per task, 350–400/day sustained |
| Secure APIs and service integrations | Dual JWT auth, RabbitMQ, Sheets, and NAS integrations in production |
| Performance, stability, observability | Cleared a 1,700-task backlog by fixing the bottleneck, not adding hardware |
| Production diagnosis under real load | Traced event-loop starvation to an unbounded queue and fixed it at the source |
| Efficient data-processing pipelines | NAS file API at 200–300 req/min, >95% less manual handling |
| Practical engineering trade-offs | Chose a bounded DB-backed queue over "just add more workers" |
| Cross-team delivery | Ops and intake platforms used daily by localization and HR, in Vietnamese and Korean |

<br />

### Also

**HR Intake Platform** `FastAPI · Next.js · MongoDB · Celery` — routes Vietnamese and Korean forms into separate Google Sheets pipelines through one shared backend.

Earlier: insurance operations backend `Spring MVC` · municipal services platform `Spring Boot · React`

<br />

### Contact

Let's talk about what you're building. &nbsp;[**Email**](mailto:dev@hermesxai.com) &nbsp;·&nbsp; [**LinkedIn**](https://www.linkedin.com/in/viet-tran-179bb9218/) &nbsp;·&nbsp; Ho Chi Minh City, Vietnam

<br />

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=October-9th&layout=compact&langs_count=6&hide=html,css,scss&title_color=3ecf8e&text_color=e6e6e6&icon_color=c9975a&bg_color=111214&hide_border=true&custom_title=Most%20used%20languages" alt="Most used languages" />
</p>

<p align="center"><sub><code>TRAN HOANG VIET — BACKEND DEVELOPER — © 2026</code> &nbsp;·&nbsp; Case studies omit proprietary code and client data.</sub></p>
