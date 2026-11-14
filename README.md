# PRAXO-CORE for C++

C++20 implementation of the PRAXO-CORE agent contract. The normative contract is [`spec/`](spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core-cpp` |
| Registry | Source / CMake |
| Build | CMake source build (see README) |
| Source version | `0.7.0` |
| Published version | not published |
| Source tag | `cpp/v0.7.0` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/cpp/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native (transport seam)
- Anthropic model: native (transport seam)
- Gemini model: native (transport seam)
- MCP client: native (transport seam)
- Harmovela sink: native (transport seam)
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native (synchronous seam)
- Retriever: native

## Quick start

This implementation is source-only. Follow the build instructions in [`language/cpp/README.md`](language/cpp/README.md).

```cpp
#include "praxo/agent.hpp"

praxo::AgentOptions options(std::make_shared<praxo::StaticModel>("hello"));
auto result = praxo::run_agent(
    std::move(options),
    praxo::Session{"demo", {}},
    "hello",
);
std::cout << result.output << "\n";
```

See the [full C++ README](language/cpp/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native (transport seam) | `OpenAICompatible`; caller supplies HTTP transport |
| Anthropic model | native (transport seam) | `Anthropic`; caller supplies HTTP transport |
| Gemini model | native (transport seam) | `Gemini`; caller supplies HTTP transport |
| MCP client | native (transport seam) | `McpClient`; caller supplies `McpTransport` |
| Harmovela sink | native (transport seam) | `HarmovelaSink`; caller supplies HTTP transport |
| OpenTelemetry sink | native (transport seam) | `OtelSink`; caller supplies `OtelTransport` |
| Subagent delegation | native (synchronous seam) | `subagent_run`; no asynchronous manager |
| Retriever | native | `Document`, `Retriever`, `retrieve` |

## Examples

Runnable examples live under [`language/cpp/examples`](language/cpp/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/cpp/examples/checkpoint) | This example uses the C++ Core checkpoint allowlist to encode and decode only registered payload types. |
| [event-sink](language/cpp/examples/event-sink) | This example uses the C++ Core sink composition to fan out lifecycle and tool events and filter the tool-only stream. |
| [identity-policy](language/cpp/examples/identity-policy) | This example binds a trusted principal to C++ Core policy decisions and rejects missing, inactive, role-mismatched, and tenant-mismatched actions. |
| [mcp](language/cpp/examples/mcp) | This example uses a caller-owned in-process transport with the C++ MCP client. It covers initialize, `tools/list`, and `tools/call` without a server process. |
| [provider-fallback](language/cpp/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary error when both fail. |
| [retry](language/cpp/examples/retry) | This example retries a transient failure with a bounded attempt count and rethrows the final error when attempts are exhausted. |
| [service](language/cpp/examples/service) | This example defines a transport-neutral request handler boundary with health, principal, and run cases. Wire it into any C++ HTTP server. |
| [streaming](language/cpp/examples/streaming) | This example collects agent stream parts from the C++ Core and checks the `values` and `messages` lifecycle. |
| [structured-output](language/cpp/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Verify

Run the checks from `language/cpp`:

```bash
cd language/cpp
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
python api-snapshot.py --check
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/cpp/README.md`](language/cpp/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

## Repository layout

- `language/cpp/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/cpp
- Registry introduction: `language/cpp/REGISTRY.md`
- Machine-readable entry: `language/cpp/llms.txt` and `language/cpp/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-cpp
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical C++ source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
