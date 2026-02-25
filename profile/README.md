<p align="center">
  <strong>Analytics that tell the whole story.</strong><br>
  <sub>Events, logs, business data — one platform. The full picture.</sub>
</p>

## Why Tell

Five dimensions of data. One query layer.

- **Events** — what users do
- **Logs** — what systems do
- **Signals** — revenue, traffic, spend
- **Marks** — releases, campaigns, incidents
- **Direction** — what you're optimizing for

Tell connects all five. Query across them.


## Install
```bash
curl -sSfL https://tell.rs | bash
```

## Platform

### Data Layer
- **Events** — Track user actions, page views, sessions, revenue. Custom events with properties. Identify users, group by company, resolve identity across devices.
- **Logs** — Structured logging with 9 severity levels. Log volume, top logs, drill-down, anomaly detection. First-class, not bolted on.
- **Plugins** — Connect business tools — Shopify, GitHub, Stripe, Cloudflare, and more. Sandboxed and extensible.
- **Sources** — TCP, Syslog, HTTP, File, Modbus.
- **Routing** — Route logs to one place, events to another, internal traffic to archive — all from the same source.
- **Transforms** — Pattern matching, filtering, PII redaction, log clustering.
- **Sinks** — ClickHouse, Parquet, Arrow, Disk, and more.
- **SDKs** — Rust, TypeScript, Go, Swift, Flutter, C++. Track events, identify users, structured logging.

### Product Layer
- **Analytics** — Funnels, retention cohorts, lifecycle, segments, audiences, group analytics, formulas. Breakdowns by any field. Compare periods. Aggregations: sum, avg, min, max, median, p75–p99 — per event or per user.
- **Dashboards** — Boards with metrics, charts, and markdown notes. Shareable via URL. Teams with roles.
- **AI & ML** — Ask questions about your data in natural language. MCP server for AI assistants. Generative UI for LLM-built dashboards. Churn prediction, anomaly detection, auto segmentation, forecasting.
- **CLI** — Full product from the terminal. Interactive TUI, live streaming, SQL queries, metrics, and plugin management.
- **Privacy** — GDPR/CCPA compliant. No cookies. PII redaction. All data anonymized.
- **Auth** — API keys, roles, teams, workspace isolation, OAuth 2.0.

## Performance

Apple M4 Pro · 12 cores · 5 clients · batch 500<

### Ingest throughput (events/sec)

| Source | b500 | b100 | b10 | b3 |
|--------|------|------|------|------|
| TCP Binary | **64M** | 55M | 6.9M | 1.4M |
| HTTP FBS | 24M | 8.3M | 1.0M | 321K |
| HTTP JSON | 2.1M | 2.3M | 848K | 307K |
| Syslog TCP | 8.7M | 8.5M | 8.3M | 2.0M |

### Sink write throughput (10M events, realistic cardinality, unique payloads)

| Sink | Events/s | Time | Written | Ratio |
|------|----------|------|---------|-------|
| disk_binary | **33.0M** | 303ms | 639 MB | 0.36x |
| disk_binary_lz4 | 21.6M | 462ms | 145 MB | 0.08x |
| disk_plaintext | 1.4M | 7.37s | 2.7 GB | 1.53x |
| disk_plaintext_lz4 | 1.1M | 9.22s | 896 MB | 0.51x |
| arrow_ipc | 2.9M | 3.49s | 1.7 GB | 0.98x |
| parquet_snappy | 2.2M | 4.58s | 249 MB | 0.14x |
| parquet_lz4 | 2.6M | 3.81s | 251 MB | 0.14x |
| parquet_zstd | 2.3M | 4.38s | 171 MB | **0.10x** |
| parquet_uncompressed | 2.6M | 3.91s | 769 MB | 0.43x |
| vortex | 1.7M | 5.94s | 1.8 GB | 0.99x |

Ratio = bytes on disk / 1.8 GB input.

## Compared To

| | Tell | PostHog | Mixpanel | Vector |
|--|:----:|:-------:|:--------:|:------:|
| Events + funnels | **✓** | ✓ | ✓ | — |
| Logs | **✓** | — | — | ✓ |
| Business connectors | **✓** | — | — | — |
| SDKs (track, identify) | **✓** | ✓ | ✓ | — |
| Dashboards | **✓** | ✓ | ✓ | — |
| Multi-source pipeline | **✓** | — | — | ✓ |
| Routing + transforms | **✓** | — | — | ✓ |
| WASM plugins | **✓** | — | — | — |
| MCP (AI assistants) | **✓** | ✓ | ✓ | — |
| CLI (tail, query, ask) | **✓** | — | — | — |
| Self-host (one binary) | **✓** | Docker | — | ✓ |
| Throughput | **64M/s** | ~100K/s | — | 86 MiB/s |
| Language | **Rust** | Python | — | Rust |

---

## SDKs (all open source)

- [**tell-rs**](https://github.com/tell-rs/tell-rs) — Rust
- [**tell-js**](https://github.com/tell-rs/tell-js) — TypeScript
- [**tell-go**](https://github.com/tell-rs/tell-go) — Go
- [**tell-cpp**](https://github.com/tell-rs/tell-cpp) — C++
- [**tell-swift**](https://github.com/tell-rs/tell-swift) — Swift

Built by the founder of Logpoint (European SIEM, acquired)
