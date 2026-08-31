# Orion-Client

## 1. Project Summary

Orion-Client is the on-device C++17 daemon that turns Orion hardware-validation requests into executable IV&V work.

- It loads TOML configuration and connects to Orion-Server through a bidirectional gRPC stream.
- It accepts local `HalService` requests for SDK and integration callers.
- It dispatches module work through an adapter registry and returns structured `hal::TestResult` data.
- Transport, execution, persistence, and device access are separated so RPC handlers do not call hardware directly.

The registry contains 35 HAL-backed adapter translation units and a stub path for unavailable modules.

- `RunOrchestrator` stamps sequences and timestamps, batches results, and sends them to the stream.
- `Spool` uses SQLite WAL storage to buffer result and log batches during outages; `Janitor` removes acknowledged or expired data within configured limits.
- `LogCollector` tails configured files and ships log entries through the durable path.
- `DiagSocket` provides local JSON status, and the systemd unit runs the daemon as a service.

The repository includes protobuf/gRPC generated contracts, CMake and Make entry points, a Docker cross-build context, sample configurations, and two focused GoogleTest targets.

- Tests cover result serialization and orchestrator sequencing with an in-memory spool and no-op stream.
- Hardware-dependent adapter behavior is implemented but is not equivalent to hardware-in-the-loop verification.
- The commands below describe repository procedures and do not claim deployment verification.

## 2. Feature Status

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | C++17 daemon and TOML configuration | Implemented | Partial: orchestration tests | [ ] Manual verification required |
| 2 | Outbound bidirectional gRPC stream | Implemented | Unknown: no focused transport test found | [ ] Manual verification required |
| 3 | Local `HalService` endpoint | Implemented | Unknown: service code present | [ ] Manual verification required |
| 4 | 35 HAL-backed adapters and registry | Implemented | Partial: per-module targets exist; hardware unverified | [ ] Manual verification required |
| 5 | Stub adapter for unavailable modules | Implemented | Unknown | [ ] Manual verification required |
| 6 | Result serialization and sequencing | Implemented | Covered by `tests/test_result_serializer.cc` and `tests/test_run_orchestrator.cc` | [ ] Manual verification required |
| 7 | SQLite WAL result/log spool | Implemented | Partial: exercised through orchestrator tests | [ ] Manual verification required |
| 8 | Log collection and durable forwarding | Implemented | Unknown | [ ] Manual verification required |
| 9 | Janitor retention and spool maintenance | Implemented | Unknown | [ ] Manual verification required |
| 10 | Unix diagnostic socket and JSON status | Implemented | Unknown | [ ] Manual verification required |
| 11 | systemd installation and sample config | Implemented | Unknown | [ ] Manual verification required |

## 3. Build and Test

```bash
make build          # Docker cross-build (ARM64 target) — the default and only build path
make test           # ctest inside Docker (ARM64 via QEMU)
```

Docker cross-build helpers live under `docker/`; runtime settings are in `conf/client.conf.sample`.
