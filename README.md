<div align="center">
  <a href="https://github.com/harshpahurkar">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&duration=4000&pause=1000&color=58A6FF&center=true&vCenter=true&multiline=true&random=false&width=640&height=80&lines=Harsh+Pahurkar;Backend+engineer" alt="Harsh Pahurkar, backend engineer" />
  </a>
</div>

<p align="center">
  <em>Payments, AI infrastructure, and the reliability work that keeps both running.</em>
</p>

<p align="center">
  <a href="https://www.harshpahurkar.com"><img src="https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=About.me&logoColor=white" alt="Portfolio" /></a>&nbsp;
  <a href="https://linkedin.com/in/harshpahurkar"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>&nbsp;
  <a href="https://github.com/harshpahurkar?tab=repositories"><img src="https://img.shields.io/badge/Repositories-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositories" /></a>
</p>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=harshpahurkar&label=Profile%20Views&color=58A6FF&style=flat" alt="Profile views" />
</p>

---

Software Developer at the Government of Ontario. CPA Honours at Seneca Polytechnic, finishing December 2025. Based in Toronto.

I build backend services that have to be right when money, models, or uptime are involved: a billing service that talks to Stripe in 39 currencies, a checkpoint pipeline that catches hallucinated code before it merges, and a daemon that restarts build runners before anyone notices they stalled. Each repo below has a quickstart you can run from a fresh clone.

## Work by industry

### Fintech and payments

**[Global Billing Service](https://github.com/harshpahurkar/global-billing-service)**
Subscription billing for SaaS products: create, upgrade, downgrade, cancel, and reactivate, with trials and end-of-period cancellation. Stripe Checkout and payment intents, refunds, and webhook verification. 39 currencies with per-currency minimum charges and zero-decimal handling, sequential invoice numbering with tax and discounts, API-key auth, structured logging. Ships with Docker, CI/CD, and an AWS ECS Fargate deployment. 27 tests at 92% coverage.
`Python` `FastAPI` `PostgreSQL` `SQLAlchemy` `Stripe` `Docker` `AWS ECS`

### AI engineering

**[agent-trace-gate](https://github.com/harshpahurkar/agent-trace-gate)**
Runtime checkpoints for code written by Claude Code and Cursor. Five stages per file: provenance, an import scan that checks unresolved names against PyPI and npm, a type check, a sandboxed smoke run, and a contract check on the return value. Every stage is an OpenTelemetry span you can open in Jaeger, and the whole thing runs as a git hook that blocks the merge. `agenttrace demo` seeds eight samples with planted bugs and exits nonzero unless each one is caught by the stage it was planted for.
`Python` `Node` `OpenTelemetry` `Jaeger` `pyright` `tsc`

**[RAG Evaluation Platform](https://github.com/harshpahurkar/rag-evaluation-platform)**
Retrieval backend built to answer one question: when the bot is wrong, which chunk won and why. Hand-rolled BM25 fused with pgvector search, a token-overlap reranker, a 54-case QA harness that catches retrieval regressions, and Langfuse traces on every query. Runs offline by default; add a key and a Postgres URL for production backends. Includes a React workbench for score tables and traces.
`Python` `FastAPI` `pgvector` `Langfuse` `React`

**[Multi-Agent Research System](https://github.com/harshpahurkar/multi-agent-research-system)**
A LangGraph pipeline (planner, researcher, evaluator, writer, finalizer) that produces sourced company briefs. The evaluator scores evidence quality and sends the researcher back for a broader pass below 0.70, so the writer never runs on junk. Async job API with per-node event streaming, fixture providers for offline runs, OpenAI and Tavily when configured.
`Python` `LangGraph` `FastAPI` `Redis` `React`

**[MCP Task Server](https://github.com/harshpahurkar/mcp-task-server)**
A read-only Model Context Protocol server so an agent can query local SQLite tasks and notes without any way to change them. Six tools with Zod schemas, a fixed query allowlist instead of string-built SQL, input guards on every call, a hand-rolled HTTP bridge with per-IP rate limiting, and a stdio contract test that exercises each tool end to end.
`TypeScript` `Node 22` `SQLite` `Zod` `MCP`

### Infrastructure and reliability

**[outage-watcher](https://github.com/harshpahurkar/outage-watcher)**
A node health daemon for task workers and build runners, written after a fleet of GCE runners kept stalling under load. It classifies each target as missing, stalled, or bloated, recovers with the action you configure (re-run a command, systemctl, Restart-Service, or a GCE reset) under a rate limit that prevents restart loops, and debounces with hysteresis so one bad tick never kills anything. Prometheus metrics, alert rules, a Grafana dashboard, Slack webhooks, incidents in SQLite. Same package on Linux, Windows, and Google Cloud.
`Python` `Prometheus` `Grafana` `systemd` `GCP`

### Cloud content platforms

**[Fragments](https://github.com/harshpahurkar/fragments)**
Authentication-first content microservice for text, JSON, and images, scoped per user with Basic Auth or Cognito JWTs. Returns fragments in their native format or converted (Markdown to HTML, PNG to JPEG), with a storage layer that swaps between memory, DynamoDB, and S3. Deployed on AWS ECS with Docker and CI.
`Node.js` `Express` `AWS S3` `DynamoDB` `Cognito` `Jest`

### Search

**[Redis Search Engine](https://github.com/harshpahurkar/redis-search-engine)**
TF-IDF search on Redis sorted sets: tokenization and stop-word filtering at index time, IDF-weighted `ZUNIONSTORE` at query time, negative terms (`search -redis`), pipelined bulk loading from JSON, and a CLI with `index`, `search`, `remove`, and `stats`.
`Python` `Redis`

### Smaller tools

[Force144Hz-v2](https://github.com/harshpahurkar/Force144Hz-v2) keeps Windows displays at 144Hz after a monitor reconnects. [fltk-text-editor](https://github.com/harshpahurkar/fltk-text-editor) is a cross-platform editor in C++17 with find and replace and an auto-save timer. [ShelfStack](https://github.com/harshpahurkar/ShelfStack) is a C++11 library system built around polymorphic publications and STL containers.

## How I build

Failure cases get a runnable demo rather than a sentence in the README: the trace gate refuses to pass unless its planted bugs are caught, and the watcher ships a leaking fake worker you can point it at and watch get restarted. The AI services run offline against fixture providers, so the tests need no API keys. Health endpoints separate "process alive" from "actually working", logs are structured, and anything that restarts something else is rate limited so it cannot loop.

## Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat-square&logo=opentelemetry&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)

---

<p align="center">
  Open to backend roles in Toronto or remote. More at <a href="https://www.harshpahurkar.com">harshpahurkar.com</a>; the fastest way to reach me is <a href="https://linkedin.com/in/harshpahurkar">LinkedIn</a>.
</p>
