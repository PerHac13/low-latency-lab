# Low-Latency Lab

A hands-on C++ systems programming laboratory for learning the fundamentals behind low-latency and quantitative trading systems.

The repository contains a sequence of progressively harder projects.

The objective is not to build production software immediately.

The objective is to understand:

- memory
- CPU caches
- allocation
- data structures
- atomics
- memory ordering
- concurrency
- serialization
- networking
- event-driven architecture
- latency measurement
- performance optimization

After completing the learning projects, the knowledge will be applied to the QX quantitative trading platform.

---

# Learning Philosophy

Every project follows:

```text
Learn
  ↓
Design
  ↓
Implement simple version
  ↓
Write tests
  ↓
Benchmark
  ↓
Profile
  ↓
Research alternatives
  ↓
Optimize
  ↓
Benchmark again
  ↓
Document findings
```

Do not optimize before measuring.

The purpose of this repository is to understand the relationship between:

```text
Code
 ↓
Compiler
 ↓
CPU
 ↓
Memory
 ↓
Operating System
 ↓
Network
```

---

# Project Roadmap

## Phase 1 — Memory & Data Structures

### 01. Ring Buffer

Learn:

- circular arrays
- head/tail indices
- fixed capacity
- wrap-around
- full/empty states
- contiguous memory
- cache locality
- O(1) insertion/removal

Deliverables:

- basic single-threaded ring buffer
- tests
- benchmark
- capacity/full/empty behavior
- performance notes

Time: ~1 week

---

### 02. SPSC Lock-Free Queue

Learn:

- `std::atomic`
- producer/consumer model
- acquire/release semantics
- memory ordering
- false sharing
- lock-free design

Deliverables:

- single-producer/single-consumer queue
- correctness tests
- multi-threaded tests
- throughput benchmark
- latency benchmark
- comparison with mutex-based queue

Time: ~1–2 weeks

---

## Phase 2 — Memory Management

### 03. Object / Memory Pool

Learn:

- dynamic allocation
- allocation overhead
- object lifetime
- free lists
- memory reuse
- fragmentation

Deliverables:

- fixed-size object pool
- allocate/free
- object reuse
- benchmark against `new/delete`
- benchmark under high allocation pressure

Time: ~1–2 weeks

---

### 04. Custom Allocator

Learn:

- alignment
- raw memory
- allocator design
- free lists
- fragmentation
- allocation strategies

Deliverables:

- basic allocator
- aligned allocation
- free-list allocator
- benchmark
- fragmentation experiment

Time: ~2 weeks

---

## Phase 3 — Financial & Performance Foundations

### 05. Fixed-Point Price Type

Learn:

- floating-point limitations
- integer representation
- precision
- rounding
- financial arithmetic

Example:

```text
$123.4567

stored as:

1234567 ticks
```

Deliverables:

- `Price`
- `Quantity`
- arithmetic operators
- comparison
- conversion
- tests for precision
- benchmark against floating point

Time: ~3–5 days

---

### 06. Benchmarking & Latency Lab

Build a reusable benchmarking framework.

Learn:

- `std::chrono`
- CPU cycle measurement
- warm-up
- distributions
- p50
- p95
- p99
- p99.9
- maximum latency
- throughput
- benchmark methodology

Deliverables:

```text
benchmark/
├── timer
├── statistics
├── runner
├── reporter
└── exporters
```

Every later project should use this framework.

Time: ~1–2 weeks

---

# Phase 4 — Concurrency

### 07. MPSC / MPMC Queues

Learn:

- multiple producers
- multiple consumers
- contention
- atomic CAS
- memory ordering
- ABA problem
- scalability

Start with:

```text
SPSC
 ↓
MPSC
 ↓
MPMC
```

Do not jump directly to a complicated production-grade queue.

Compare:

```text
mutex queue
    vs
SPSC
    vs
MPSC
    vs
MPMC
```

Measure:

- throughput
- latency
- CPU usage
- contention

Time: ~2–3 weeks

---

# Phase 5 — Networking

### 08. Custom Binary Protocol

Learn:

- serialization
- deserialization
- binary layouts
- endianness
- alignment
- framing
- checksums
- versioning

Example message:

```text
HEADER
├── version
├── message_type
├── sequence
└── payload_size

PAYLOAD
└── message-specific data
```

Build:

```text
Encoder
Decoder
Frame Parser
Validator
```

Time: ~1–2 weeks

---

### 09. Event Loop

Learn:

- non-blocking I/O
- file descriptors
- epoll
- readiness events
- event-driven architecture
- system calls
- timers

Start with:

```text
socket
  ↓
non-blocking
  ↓
epoll
  ↓
event loop
  ↓
handler
```

Later experiment with:

```text
epoll
vs
poll
vs
select
```

Time: ~2–3 weeks

---

# Phase 6 — Trading-System Primitive

### 10. Market Data Feed

Combine the previous projects.

Build a simulated market-data system:

```text
Market Data Generator
        ↓
Binary Encoder
        ↓
UDP/TCP
        ↓
Event Loop
        ↓
Feed Handler
        ↓
Decoder
        ↓
SPSC Queue
        ↓
Consumer
```

Messages:

```text
ADD_ORDER
CANCEL_ORDER
MODIFY_ORDER
TRADE
BOOK_UPDATE
```

Include:

- sequence numbers
- dropped-message detection
- replay
- latency measurement
- throughput measurement
- deterministic test data

Time: ~3–4 weeks

---

# Final Phase — QX

After completing the ten projects:

```text
Low-Latency Lab
       ↓
       ↓
       ↓
      QX
       ↓
Limit Order Book
       ↓
Matching Engine
       ↓
Market Data
       ↓
Strategies
       ↓
Risk
       ↓
Backtesting
       ↓
Performance Optimization
```

QX should reuse concepts learned in this repository rather than introducing everything from scratch.

---

# Global Definition of Done

A project is not complete merely because the code works.

Each project should have:

- [ ] README
- [ ] design notes
- [ ] implementation
- [ ] unit tests
- [ ] edge-case tests
- [ ] benchmark
- [ ] performance measurements
- [ ] profiling where appropriate
- [ ] comparison with a baseline
- [ ] research notes
- [ ] lessons learned

---

# Research Rule

For every important optimization:

```text
Hypothesis
    ↓
Experiment
    ↓
Measurement
    ↓
Result
    ↓
Explanation
```

Example:

> Hypothesis: avoiding dynamic allocation will reduce tail latency.

Measure:

```text
new/delete
vs
object pool
```

Report:

```text
p50
p95
p99
p99.9
max
throughput
allocations
```

Then explain why the result occurred.

---

# Time Philosophy

The timeline is an estimate, not a deadline.

Expected total:

```text
~14–21 weeks
```

assuming this is done as a single-developer learning/research project alongside other responsibilities.

A project can take longer if the research produces useful findings.

Depth is more important than speed.

---

# Completion Goal

The ultimate goal is not:

> "I built ten C++ projects."

The goal is:

> "I understand the systems primitives used to build low-latency software and can measure, reason about, and optimize them."

Only after reaching that point should QX become the primary project.
