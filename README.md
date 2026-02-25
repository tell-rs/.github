<p align="center">
  <strong>Analytics that tell the whole story.</strong><br>
  <sub>Events, logs, business data — one platform. The full picture.</sub>
</p>

---

```bash
curl -sSfL https://tell.rs | bash
```

---

## Why Tell

Five types of data. Every company generates all five. No tool connects them.

| Data | Today | The problem |
|------|-------|-------------|
| **Events** — what users do | Mixpanel, Amplitude, PostHog | Isolated from logs and revenue |
| **Logs** — what systems do | Datadog, Splunk, Elastic | Can't correlate with user behavior |
| **Business signals** — revenue, ads, traffic | Supermetrics, spreadsheets | Disconnected from product |
| **Marks** — releases, campaigns, incidents | Wikis, if at all | No link to impact |
| **Direction** — north stars, targets | Nowhere | Can't measure what matters |

Tell collects all five. One data model. Everything queryable together.

---

## Platform

| Layer | What | How fast |
|-------|------|----------|
| **Ingest** | TCP, Syslog, HTTP, File, Modbus | 64M events/sec |
| **Plugins** | WASM connectors — GitHub, Shopify, Resend, Cloudflare | Sandboxed, hot-loadable |
| **Routing** | Content-aware `when` guards, fan-out, CIDR | O(1) batch evaluation |
| **Transforms** | Pattern match, Filter, Redact, Reduce | 10.9M events/sec PII scrubbing |
| **Sinks** | ClickHouse, Parquet, Arrow, Vortex, Disk | 33M events/sec write |
| **Query** | SQL via `tell query` | ClickHouse or local Polars |
| **Tap** | Live stream via `tell tail` | Workspace/source/type filters |
| **AI** | `tell ask` · `tell skill` · MCP server | Workspace-scoped, streaming |
| **Blocks** | Generative UI — charts, tables, callouts | TUI, web, and native |
| **Auth** | API keys · JWT/RBAC · OAuth 2.0/PKCE | Workspace isolation |
| **Audit** | 40 typed actions, zero-copy builder | Every write recorded |
| **Web** | React + Shadcn dashboards | REST API |

---

## Performance

<sub>Apple M4 Pro · 12 cores · 5 clients · batch 500</sub>

### Ingest throughput (events/sec)

| Source | b500 | b100 | b10 |
|--------|------|------|------|
| TCP Binary | **64M** | 55M | 6.9M |
| HTTP FlatBuffers | 24M | 8.3M | 1.0M |
| Syslog TCP | 8.7M | 8.5M | 8.3M |
| HTTP JSON | 2.1M | 2.3M | 848K |

### Sink write throughput (10M events)

| Sink | Events/sec | Compression |
|------|------------|-------------|
| disk_binary | **33.0M** | 0.36× |
| disk_binary_lz4 | 21.6M | 0.08× |
| arrow_ipc | 2.9M | 0.98× |
| parquet_zstd | 2.3M | **0.10×** |
| parquet_lz4 | 2.6M | 0.14× |

---

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
| MCP (AI assistants) | **✓** | — | — | — |
| CLI (tail, query, ask) | **✓** | — | — | — |
| Self-host (one binary) | **✓** | Docker | — | ✓ |
| Throughput | **64M/s** | ~100K/s | — | 86 MiB/s |
| Language | **Rust** | Python | — | Rust |

---

## SDKs <sub>(all open source)</sub>

| | Language | Install |
|--|----------|---------|
| [**tell-rs**](https://github.com/tell-rs/tell-rs) | Rust | `cargo add tell` |
| [**tell-js**](https://github.com/tell-rs/tell-js) | TypeScript | `npm i @tell-rs/tell` |
| [**tell-go**](https://github.com/tell-rs/tell-go) | Go | `go get tell.rs/sdk` |
| [**tell-cpp**](https://github.com/tell-rs/tell-cpp) | C++ | Header-only |

--- 

Built by the founder of Logpoint (acquired).
