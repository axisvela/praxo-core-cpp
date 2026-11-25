# PRAXO-CORE for C++

C++20 implementation of the PRAXO-CORE agent contract. The normative contract is [`spec/`](spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core-cpp` |
| Registry | Source / CMake |
| Build | CMake source build (see README) |
| Source version | `0.9.0` |
| Published version | not published |
| Source tag | `cpp/v0.9.0` |
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
| OpenAI-compatible model | native (transport seam) | `OpenAICompatible`; caller supplies HTTP and streaming transports; `OpenAICompatibleStreamTransport` reassembles SSE content, tool calls, usage, and finish reason |
| Anthropic model | native (transport seam) | `Anthropic`; caller supplies HTTP and streaming transports; Anthropic SSE reassembly |
| Gemini model | native (transport seam) | `Gemini`; caller supplies HTTP and streaming transports; Gemini SSE reassembly |
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
| [consumer](language/cpp/examples/consumer) | This example runs a deterministic model against the C++ Core, registers one `record(target)` tool, applies an explicit tool scope plus policy, and checks that an allowed call pr... |
| [event-sink](language/cpp/examples/event-sink) | This example uses the C++ Core sink composition to fan out lifecycle and tool events and filter the tool-only stream. |
| [hitl](language/cpp/examples/hitl) | This example demonstrates a write tool that requires human approval: |
| [identity-policy](language/cpp/examples/identity-policy) | This example binds a trusted principal to C++ Core policy decisions and rejects missing, inactive, role-mismatched, and tenant-mismatched actions. |
| [live-model](language/cpp/examples/live-model) | This example connects the C++ Core to an OpenAI-compatible endpoint through the existing `OpenAICompatible` adapter and registers one low-risk `get_time(zone)` tool. The model m... |
| [mcp](language/cpp/examples/mcp) | This example uses a caller-owned in-process transport with the C++ MCP client. It covers initialize, `tools/list`, and `tools/call` without a server process. |
| [provider-fallback](language/cpp/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary error when both fail. |
| [retry](language/cpp/examples/retry) | This example retries a transient failure with a bounded attempt count and rethrows the final error when attempts are exhausted. |
| [service](language/cpp/examples/service) | This example defines a transport-neutral request handler boundary with health, principal, and run cases. Wire it into any C++ HTTP server. |
| [session-checkpoint](language/cpp/examples/session-checkpoint) | This example saves and restores a conversation history across two agent turns using the Core checkpoint allowlist. |
| [streaming](language/cpp/examples/streaming) | This example collects agent stream parts from the C++ Core and checks the `values` and `messages` lifecycle. |
| [structured-output](language/cpp/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Scenario Tutorials

Scenario-oriented tutorials live under `language/cpp/Tutorial`.

| Path | What it shows |
| --- | --- |
| [Tutorial](language/cpp/Tutorial) | Bounded C++ examples built on the native Core. Each tutorial is a small, runnable slice with explicit non-goals and an application-owned boundary; none is a complete industry pr... |
| [bom-review](language/cpp/Tutorial/bom-review) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [construction-safety](language/cpp/Tutorial/construction-safety) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [container-yard](language/cpp/Tutorial/container-yard) | A bounded first slice of TL-02, not a terminal operating system. It replans fixed synthetic container jobs under resource constraints and drafts a review-only schedule. No crane... |
| [drone-fleet-plan](language/cpp/Tutorial/drone-fleet-plan) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [dubbing-plan](language/cpp/Tutorial/dubbing-plan) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [eda-placement](language/cpp/Tutorial/eda-placement) | A bounded first slice of OG-05, not a foundry-valid physical-design flow. It reads a fixed synthetic placement grid and drafts a review-only placement with stated PPA proxies. N... |
| [fleet-map](language/cpp/Tutorial/fleet-map) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [household-robot](language/cpp/Tutorial/household-robot) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [industrial-edge](language/cpp/Tutorial/industrial-edge) | A scoped industrial tutorial over the native MIT C++ Core. It reads one fixed `edge-100` snapshot through an application-owned `DeviceAdapter` interface and drafts an operator m... |
| [materials-design](language/cpp/Tutorial/materials-design) | A bounded first slice of SC-04, not a validated materials-discovery pipeline. It evaluates fixed synthetic candidate properties and drafts the next review-only simulation. No va... |
| [mesh-review](language/cpp/Tutorial/mesh-review) | A bounded first slice of MD-05, not a CAD kernel or manufacturing-certification flow. It compares fixed synthetic mesh descriptors against stated constraints and drafts a review... |
| [mining-slope](language/cpp/Tutorial/mining-slope) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [molecule-screen](language/cpp/Tutorial/molecule-screen) | A bounded first slice of SC-02, not drug discovery. It ranks fixed synthetic molecular descriptors under stated constraints and drafts a review-only assessment. No efficacy, tox... |
| [ocean-routing](language/cpp/Tutorial/ocean-routing) | A bounded first slice of TL-03, not a navigation or fuel-optimization system. It compares fixed synthetic route/weather costs and drafts a review-only route. No navigation comma... |
| [production-scheduling](language/cpp/Tutorial/production-scheduling) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [quant-risk](language/cpp/Tutorial/quant-risk) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [storyboard-previs](language/cpp/Tutorial/storyboard-previs) | A bounded tutorial slice over the native C++ Core. It reads one fixed fixture, enforces scope and drafts a review-only result. No production write or external system access. |
| [traffic-signal-plan](language/cpp/Tutorial/traffic-signal-plan) | A bounded first slice of CT-01, not a traffic-control system. It reads fixed junction queues, drafts a review-only green-time plan and checks it against deterministic limits. No... |

## Reference Applications

Complete AI-native reference applications live under `language/cpp/application`.

| Path | What it shows |
| --- | --- |
| [application](language/cpp/application) | A C++ edge integration where the agent drives the primary device-diagnosis workflow: an operator submits an incident intent, the agent reads application-owned device telemetry t... |

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
- LinkedIn: <https://www.linkedin.com/company/axisvela/>
- Facebook: <https://www.facebook.com/profile.php?id=61596905732406>
- YouTube: <https://www.youtube.com/@axisvela>
- Discord: <https://discord.com/channels/1575163993767809064/1575164343148875977>
- GitHub Discussions: <https://github.com/axisvela/praxo-core/discussions>
- GitHub Issues: <https://github.com/axisvela/praxo-core/issues>
- Documentation: <https://axisvela.github.io/praxo-core/>
- Architect: <https://axisvela.architect.pub>

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
