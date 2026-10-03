# Low-Latency Lab

A hands-on C++ systems programming laboratory focused on the fundamentals of low-latency software and quantitative trading systems.

This repository is a learning and research project built by a single developer.

The projects are intentionally implemented from first principles before introducing more advanced optimizations or third-party implementations.

---

## Objective

Learn how low-latency systems work from the bottom up.

```text
Memory
  ↓
Data Structures
  ↓
Allocation
  ↓
Atomics
  ↓
Concurrency
  ↓
Serialization
  ↓
Networking
  ↓
Event Loops
  ↓
Market Data
  ↓
QX
```

---

## Projects

| # | Project | Focus |
|---|---|---|
| 01 | Ring Buffer | Circular buffers & memory |
| 02 | SPSC Queue | Lock-free programming |
| 03 | Memory Pool | Allocation & object lifetime |
| 04 | Custom Allocator | Memory management |
| 05 | Fixed-Point Price | Deterministic financial arithmetic |
| 06 | Benchmarking | Latency & performance measurement |
| 07 | MPSC/MPMC Queue | Concurrent data structures |
| 08 | Binary Protocol | Serialization & wire formats |
| 09 | Event Loop | Non-blocking I/O |
| 10 | Market Data Feed | Networking + trading-system primitives |

---

## Development Philosophy

Every project follows:

```text
Understand
    ↓
Implement
    ↓
Test
    ↓
Benchmark
    ↓
Profile
    ↓
Optimize
    ↓
Measure Again
    ↓
Document
```

Performance claims should be supported by measurements.

---

## Performance Metrics

Where applicable, projects measure:

- throughput
- p50 latency
- p95 latency
- p99 latency
- p99.9 latency
- maximum latency
- CPU usage
- memory usage
- allocations

---

## Repository Structure

```text
projects/
├── 01-ring-buffer/
├── 02-spsc-queue/
├── 03-memory-pool/
├── 04-custom-allocator/
├── 05-fixed-point-price/
├── 06-benchmarking/
├── 07-mpsc-mpmc-queue/
├── 08-binary-protocol/
├── 09-event-loop/
└── 10-market-data-feed/

experiments/
docs/
benchmarks/
tools/
qx/
```

---

## Technology

### Core

- C++20
- CMake
- GoogleTest
- Google Benchmark

### Systems

- Linux
- POSIX APIs
- TCP
- UDP
- epoll
- atomics
- threads

### Analysis

- perf
- Valgrind
- heaptrack
- FlameGraph
- Python
- NumPy
- Pandas
- Matplotlib

---

## Research

This repository is not only an implementation exercise.

Important questions are investigated experimentally.

Examples:

- Why is a contiguous structure faster?
- What causes cache misses?
- How expensive is dynamic allocation?
- How does false sharing affect throughput?
- What does acquire/release actually guarantee?
- When does lock-free programming help?
- How much does serialization cost?
- What is the effect of system calls?
- How does network latency affect an event-driven system?

Results are recorded under:

```text
experiments/
docs/research/
```

---

## Roadmap

See [`ROADMAP.md`](ROADMAP.md).

---

## Final Objective

After completing these projects, the concepts will be applied to:

**QX — Low-Latency Quantitative Trading Platform**

The goal is to build QX with an understanding of the underlying systems primitives rather than treating the trading system as a collection of high-level components.

---

## Status

Currently learning and implementing the projects sequentially.

This repository intentionally favors understanding and reproducible measurements over rapid completion.
