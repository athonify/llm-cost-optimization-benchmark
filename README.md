# ⚡ Athonify LLM Cost Optimization Benchmark Suite

[![Official Athonify Benchmark](https://img.shields.io/badge/Athonify-Official_Benchmark-0052FF?style=flat-square&logo=github)](https://github.com/athonify/llm-cost-optimization-benchmark)
[![Audit Status](https://img.shields.io/badge/Audit_Status-VERIFIED_%26_PASSED-brightgreen?style=flat-square)](AUDIT_CHECKLIST.md)
[![Live Audit Report](https://img.shields.io/badge/Live_Audit_Report-20--Turn_SWE_Benchmark-0052FF?style=flat-square&logo=markdown)](results/live_audit_run_2026-08-10.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)
[![OpenAI SDK Compatible](https://img.shields.io/badge/OpenAI_SDK-100%25_Compatible-brightgreen?style=flat-square)](https://github.com/openai/openai-node)

> **Official open-source, reproducible, and auditable benchmark suite for measuring LLM API cost reduction, prompt caching efficiency, and latency improvements provided by Athonify.**

---

## 🎯 Benchmark Objective: Transparency & Auditability

Athonify operates as a **100% drop-in API proxy compatible with standard OpenAI SDKs**. By placing Athonify in front of your LLM requests (`https://athonify.com/v1`), your applications gain automatic **Prompt Caching** and **Asymmetric Model Routing** without changing your application code or prompt architectures.

This repository provides an open-source, verifiable benchmark tool allowing software engineers, AI developers, and finance teams to independently audit Athonify's cost savings claims against direct LLM provider endpoints.

For full technical compliance, dataset parity, and request ID verification criteria, review our formal [Audit & Quality Gate Checklist](AUDIT_CHECKLIST.md) and our latest [Live Production Audit Report (20-Turn Agent Session)](results/live_audit_run_2026-08-10.md).

### 📁 Audited Results Repository

All official benchmark executions are archived with full request metadata in the [`results/`](results/) directory:

- 📄 **[Live Production Audit Report (20-Turn SWE Agent Session)](results/live_audit_run_2026-08-10.md)** — **62.89% Net Savings** ($1.37 Baseline vs $0.50 Athonify) with 40 paired live Request IDs.

---

## ⚙️ How Athonify Works: Unified Provider-Native Optimizations

Athonify does not reinvent underlying provider caching protocols—it **unifies and automates provider-native optimization mechanisms** behind a single OpenAI-compatible API (`https://athonify.com/v1`). Developers write code once using standard SDKs, and Athonify handles cache markers, TTL lifecycle, and intent routing automatically in real-time.

### Provider-Native Optimization Matrix

- **Anthropic Claude Models** *(Haiku, Sonnet, Opus)*
  - **Native Mechanism**: Prompt Caching (90% discount on cached input tokens: $0.30/1M).
  - **Athonify Automation**: Automatic cache marker injection, TTL lifecycle management, and dynamic history tracking without manual code changes.
  - **Empirical Validation**: **62.89% net cost reduction** across 20-turn SWE agent sessions ([Live Audit Report](results/live_audit_run_2026-08-10.md)).

- **DeepSeek Models** *(Flash, Pro)*
  - **Native Mechanism**: Context Prefix & KV Cache Reuse.
  - **Athonify Automation**: Intent-based payload routing, pattern detection, and automatic cache key alignment.
  - **Empirical Validation**: High-throughput semantic ingestion with zero cold-start latency overhead.

- **OpenAI Models** *(GPT-4o, GPT-4o-mini)* — *[Roadmap / In Progress]*
  - **Native Mechanism**: Automatic Prompt Caching (50% discount on input tokens).
  - **Athonify Automation**: Transparent header propagation and multi-provider fallback routing.

> 💡 **Core Thesis**: Each major LLM provider builds outstanding native optimization features. Athonify provides the unified control plane that activates these features out-of-the-box with zero code changes.


## 📊 Benchmark Methodology

The benchmark simulates real-world multi-turn AI agent sessions (e.g., SWE coding agents, code reviewers, customer support bots, and analytical agents) carrying cumulative repository/context history across 3 consecutive turns.

### Tested Models & Cost Basis

| Environment | Model Tag | Base URL | Input Pricing (1M tokens) | Cache Discount |
| :--- | :--- | :--- | :--- | :--- |
| **Direct Baseline** | `claude-sonnet-5` | Direct Provider (Anthropic) | **$3.00** | 0% (Standard) |
| **Athonify** | `athonify-pro` | `https://athonify.com/v1` | **$0.30** (on cache hit) | **90% Discount** |

> ⚠️ **Note**: The 90% cache discount applies only to cached token hits (input tokens previously processed). Total realized savings vary by session length (12%–85% depending on context reuse patterns). See empirical results in the [Live Audit Report](results/live_audit_run_2026-08-10.md) for actual savings across real workloads.

---

## 🚀 Asymmetric Model Selection: Right Tool for Each Task

Athonify orchestrates models based on architectural specialization—maximizing performance, speed, and cost-efficiency without compromising output quality:

- **Read-Heavy Operations (Context Analysis & Pattern Detection)**
  - **Specialized Models**: DeepSeek V4 Flash / Claude Haiku
  - **Specialization**: Engineered for ultra-fast semantic understanding, high-throughput context ingestion, and pattern extraction.
  - **Value**: Delivers rapid analysis over massive context windows without latency bottlenecks.

- **Write-Heavy Operations (Code Generation & Complex Reasoning)**
  - **Frontier Models**: Claude Sonnet 5 / Claude Opus 5 / DeepSeek V4 Pro
  - **Specialization**: Engineered for high-fidelity code synthesis, deep architectural reasoning, and multi-file refactoring.
  - **Value**: Directs full model intelligence where precision is critical, amplified by native Prompt Caching on repeated context blocks.

**The Synergistic Result**: Better outputs by leveraging the optimal model per task + lower cumulative costs via model specialization and prompt caching.

---

## 📈 Measured Savings by Session Length Tiers

Based on empirical live API benchmark executions, cost savings scale directly as context history is reused across turns:

```text
+-------------------------------------------------------------------------+
|              MEASURED SAVINGS BY SESSION LENGTH                         |
+-------------------+--------------------+--------------------------------+
| Session Tier      | Turn Count         | Measured Real Savings (%)      |
+-------------------+--------------------+--------------------------------+
| Short Sessions    | 1 - 3 turns        | 27.16% (empirically tested)    |
| Medium Sessions   | 4 - 10 turns       | ~40% - 50% (estimated trajectory)|
| Long / Agentic    | 15+ turns (SWE)    | 62.89% (empirically tested)    |
+-------------------+--------------------+--------------------------------+
```

> 💡 **Empirical Proof**: **27.16%** measured in our 3-turn baseline audit; **62.89%** measured in our 20-turn SWE agent production audit. Medium tier is estimated via linear interpolation between tested empirical benchmarks. See the [Live Audit Report](results/live_audit_run_2026-08-10.md) for full raw telemetry.

---

## 🚀 Quickstart Guide: How to Run the Benchmark

Anyone can clone this repository and verify the benchmark within 60 seconds.

### 1. Clone the Repository

```bash
git clone https://github.com/athonify/llm-cost-optimization-benchmark.git
cd llm-cost-optimization-benchmark
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables (Optional for Live API Calls)

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Edit `.env` to insert your credentials:

```env
# --- DIRECT PROVIDER KEYS (For Baseline Comparison) ---
ANTHROPIC_API_KEY=your_anthropic_key_here

# --- ATHONIFY CREDENTIALS ---
ATHONIFY_API_KEY=your_athonify_key_here
ATHONIFY_BASE_URL=https://athonify.com/v1
```

> 💡 **Note**: If no API keys are configured, the benchmark automatically runs in **Simulation Demo Mode**, demonstrating exact token math, latency reduction, and CLI report rendering out of the box!

### 🔄 Execution Modes

The benchmark suite supports two seamless modes of execution:

1. **Demo Simulation Mode (Default)**:
   - Requires no API keys.
   - Runs an empirical simulation out of the box using measured token heuristics, cache hit progressions, and realistic latency differentials.
   - Perfect for quick CLI visual evaluation and auditing the underlying math.

2. **Live API Execution Mode**:
   - Activated automatically when valid keys are provided in `.env`.
   - Sends live HTTPS requests to direct provider endpoints and the Athonify (`https://athonify.com/v1`).
   - Measures real-time round-trip network latency (ms) and inspects returned payload usage metadata (`usage.prompt_tokens_details.cached_tokens`).

### 4. Execute the Benchmark

```bash
npm run benchmark
```

---

## 🖥️ Example Terminal Scorecard Output

```text
========================================================================
       ATHONIFY OFFICIAL LLM COST OPTIMIZATION BENCHMARK SUITE          
========================================================================

Dataset: enterprise-e-commerce-backend-swe-context
Approx Context Size: 38,500 tokens
Simulated Turns: 20

 [LIVE API MODE ACTIVE]
   Direct Baseline: Official Anthropic API (claude-sonnet-5)
   Athonify:  https://athonify.com/v1 (athonify-pro)

Executing Multi-Turn Agentic Chat Simulation...

---> Executing Turn 1/20: "Analyze the codebase above..."
     ✔ [Direct Baseline] Req ID: msg_011CduqfXKR3GurA9yuXMyQG | Model: claude-sonnet-5 | Out Tokens: 2500
     ✔ [Athonify]  Req ID: d3ecda53-d7e7-4970-9f40-b5dc38826735 | Model: athonify-pro | Out Tokens: 1500
       └─ [Athonify Intent Routing]: Write/Refactor Confirmed ➔ Dynamically routed to Claude Sonnet 5 (Prompt Caching Active)
...
---> Executing Turn 20/20: "Provide final architectural deployment documentation..."
     ✔ [Direct Baseline] Req ID: msg_011Cdurbun2obUu3YszA3DYv | Model: claude-sonnet-5 | Out Tokens: 2500
     ✔ [Athonify]  Req ID: 5c435849-4f3c-4cf6-ad16-a99be5718c79 | Model: athonify-pro | Out Tokens: 1500
       └─ [Athonify Intent Routing]: Write/Refactor Confirmed ➔ Dynamically routed to Claude Sonnet 5 (Prompt Caching Active)

========================================================================
                    FINAL BENCHMARK SCORECARD                          
========================================================================
  Baseline Total Cost (claude-sonnet-5): $1.37277
  Athonify Total Cost (athonify-pro):     $0.50948
  Net Cost Reduction ($):                              $0.86328
  Net Savings (%):                                      62.89% 🔥
  Global Prompt Cache Hit Rate:                        92.0%  🚀
  Average Response Latency Reduction:                  37.7%  ⚡
========================================================================
```

> 📄 For the complete 20-turn execution matrix and all 40 paired production Request IDs, see the [Live Production Audit Report](results/live_audit_run_2026-08-10.md).

---

## 🛠️ Integration Code Snippet

Swapping your application from direct calls to Athonify requires changing only `baseURL` and `defaultHeaders` or model tag:

```javascript
import OpenAI from 'openai';

// Before: Direct API Call
// const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });

// After: Optimized Athonify
const openai = new OpenAI({
  apiKey: process.env.ATHONIFY_API_KEY,
  baseURL: 'https://athonify.com/v1'
});

const response = await openai.chat.completions.create({
  model: 'athonify-pro', // Triggers automatic Prompt Caching + Asymmetric Routing
  messages: [ /* your context & prompt */ ]
});
```

---

## 📜 License

MIT © [Athonify Team](https://athonify.com)
