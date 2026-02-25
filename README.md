<p align="center">
  <strong>Analytics that tell the whole story.</strong><br>
  <sub>Events, logs, business data — one platform. The full picture.</sub>
</p>

<p align="center">
  <a href="https://tell.rs">tell.rs</a> ·
  <img src="https://img.shields.io/badge/status-alpha-orange" alt="Alpha">
</p>

---

Product analytics, logs, and business data — unified. Track events and funnels. Ingest structured logs. Connect sources like GitHub and Shopify. Query everything. Build dashboards.

- **Stupid fast.** 64M events/sec on batched TCP. High-performance Rust pipeline with sub-millisecond latency.
- **Connect everything.** Product events, structured logs, business data (GitHub, Shopify, more). Query them together — that's the point.
- **One binary.** No containers. No Docker Compose. Runs on a VPS or your enterprise cluster.
- **Yours forever.** Self-hosted. Your data never leaves your servers. No cloud dependency.

## Quick install 
```bash
curl -sSfL https://tell.rs | bash
```

## Platform

## Platform

- **Sources** — TCP (high-throughput), Syslog (TCP/UDP), HTTP (JSON/FBS), File (lines, JSONL, binary — preserves timestamps and source IP for re-import and migration), Modbus (industrial protocol proxy).
- **Routing** — Content-aware routing with `when` guards. Route logs to ClickHouse, events to Parquet, internal traffic to archive — all from the same source. Multi-match fan-out, IP-range routing (CIDR), O(1) batch-level evaluation
- **Transformers** — Pattern matching for log clustering, Filter, Redact (10.9M events/sec PII scrubbing), Reduce. Binary guards skip irrelevant batches at ~2ns and scan fields at ~20ns — 18x faster for selective transforms
- **Sinks** — ClickHouse, Parquet, Arrow IPC, Vortex (columnar, cascading compression), Disk (binary/plaintext, optional LZ4), Forwarder, Stdout
- **Tap** — Live streaming with `tell tail`. Filter by workspace, source, type. Sampling and rate limiting built in
- **Query** — SQL queries via `tell query`. ClickHouse for production, Polars for local Arrow IPC files
- **MCP** — Model Context Protocol server for AI assistants. Workspace-scoped queries, board CRUD, data exploration, ML insights
- **Blocks** — Generative UI format. Streaming JSONL for LLM-generated dashboards — metrics, charts, tables, callouts. Renders in TUI, web, and native
- **AI** — `tell ask` to query an LLM about your data. `tell skill` for custom LLM skills from markdown files
- **Auth** — API keys with workspace isolation. JWT with RBAC. OAuth 2.0 ("Sign in with Tell") with PKCE. OS keyring for CLI credentials
- **Audit** — Structured audit logging. 40 typed actions, zero-copy builder, every write and auth event recorded
- **Config** — TOML with sensible defaults. Validation catches mistakes before you run
- **API & Web** — Rust API server. REST API for analytics, dashboards, sharing, workspace management. React + Shadcn UI frontend
- **SDKs** — Rust, TypeScript, Go, Swift, Flutter, C++

## Performance

Apple M4 Pro | 12 cores | 5 clients | batch 500 | null sink

| Source | b500 | b100 | b10 | b3 |
|--------|------|------|------|------|
| TCP Binary | **64M** | 55M | 6.9M | 1.4M |
| HTTP FBS | 24M | 8.3M | 1.0M | 321K |
| HTTP JSON | 2.1M | 2.3M | 848K | 307K |
| Syslog TCP | 8.7M | 8.5M | 8.3M | 2.0M |

Sink write throughput (10M events, realistic cardinality, unique payloads):

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

## Compared to

| | Tell | PostHog | Mixpanel | Vector |
|--|------|---------|----------|--------|
| Events | ✓ | ✓ | ✓ | ✗ |
| Logs | ✓ | ✗ | ✗ | ✓ |
| Business connectors | ✓ | ✗ | ✗ | ✗ |
| SDKs (track, identify) | ✓ | ✓ | ✓ | ✗ |
| Dashboards | ✓ | ✓ | ✓ | ✗ |
| Multi-source pipeline | ✓ | ✗ | ✗ | ✓ |
| Routing + transforms | ✓ | ✗ | ✗ | ✓ |
| WASM plugins | ✓ | ✗ | ✗ | ✗ |
| Multiple sinks | ✓ (CH, Arrow, Parquet, Vortex, disk) | ClickHouse | ✗ | ✓ |
| MCP (AI assistants) | ✓ | ✗ | ✗ | ✗ |
| CLI (`tail`, `query`) | ✓ | ✗ | ✗ | ✗ |
| Self-host (one binary) | ✓ | Docker Compose | ✗ | ✓ |
| Throughput | 64M/s | ~100K/s | — | 86 MiB/s |
| Language | Rust | Python | — | Rust |
| Source available | ✓ | ✓ | ✗ | ✓ |

## Team

Built by the founder of Logpoint (acquired).
