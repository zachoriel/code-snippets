## Table of Contents

### C# Snippets
- [ArenaAllocator.Allocate – Manual Allocation with Alignment and Logging](#-arenaallocatorallocate--manual-allocation-with-alignment-and-logging)
- [ArenaUtil.GetNextPowerOfTwo – Fast Power-of-Two Round-Up Utility](#-arenautilgetnextpoweroftwo--fast-power-of-two-round-up-utility)
- [ArenaArray<T> Constructor – Type-Safe Unmanaged Array Allocation](#-arenaarrayt-constructor--type-safe-unmanaged-array-allocation)
- [Benchmark Cycle Loop – Allocation, GC Profiling, and Logging](#-benchmark-cycle-loop--allocation-gc-profiling-and-logging)
- [ArenaLog.Log – Custom Structured Logging with Severity and Formatting](#-arenaloglog--custom-structured-logging-with-severity-and-formatting)
- [ArenaMonitor.PrintSummary – Memory Diagnostics and Alignment Analysis](#-arenamonitorprintsummary--memory-diagnostics-and-alignment-analysis)

### Ruby Snippets *(coming soon!)*
- *TBD*

## Code Snippets

### 📌 `ArenaAllocator.Allocate` – Manual Allocation with Alignment and Logging

This method manually allocates memory from a preallocated byte arena, honoring custom alignment requirements using bitwise math. It includes:

- **Power-of-two validation** to enforce safe alignment boundaries.
- **Offset alignment logic** using efficient bitmasking operations.
- **Overflow protection** with clear error logging if an allocation would exceed arena capacity.
- **Tracking** of alignment padding (i.e., wasted bytes to meet alignment constraints).
- **Structured telemetry** through centralized logging and custom allocation monitoring tools.

> *Skills demonstrated:* low-level memory management, bitwise arithmetic, runtime safety, diagnostic logging, and performance-aware systems design.

![ArenaAllocationLogic](https://github.com/user-attachments/assets/1d278ff9-ce71-4147-b7b1-308c3a502877)

### 📌 `ArenaUtil.GetNextPowerOfTwo` – Fast Power-of-Two Round-Up Utility

This method efficiently computes the next power of two greater than or equal to a given value using bitwise operations. It’s particularly useful for calculating safe memory alignment sizes in custom allocators or performance-critical systems.

- **Bitwise rounding**: Uses shift-and-OR techniques to round up with minimal CPU overhead.
- **Clamping support**: Accepts an optional maximum value to avoid overshooting (defaults to 64).
- **Robust design**: Guarantees a minimum return value of 1, with safe handling of edge cases like non-positive input.

> *Skills demonstrated:* bit-level optimization, utility function design, numerical edge-case handling, and memory-alignment strategy.

![PowerOfTwoUtility](https://github.com/user-attachments/assets/316838b1-9489-4efd-af68-9dd6c29510bd)

### 📌 `ArenaArray<T>` Constructor – Type-Safe Unmanaged Array Allocation

This constructor allocates a fixed-size, unmanaged array from a custom memory arena, enforcing strict runtime guarantees on usage and safety:

- **Generic type constraint enforcement** using `UnsafeUtility.IsUnmanaged<T>()` ensures only unmanaged value types are accepted.
- **Fail-fast parameter checks** for invalid lengths or unsupported types.
- **Size and alignment calculation** based on the underlying type, using power-of-two rounding for alignment safety.
- **Hard allocation failure handling**, including clear exception messaging if the memory arena is exhausted.

> *Skills demonstrated:* generic programming with runtime validation, type safety in low-level memory contexts, robust constructor design, and defensive programming.

![CustomArrayConstructor](https://github.com/user-attachments/assets/4d12a356-71c9-445b-8c8d-02f0909857e5)

### 📌 Benchmark Cycle Loop – Allocation, GC Profiling, and Logging

This block is part of a larger function that benchmarks performance and memory usage of dynamically allocated buffers over multiple frames, with optional Burst compilation:

- **Controlled memory allocation** using custom unmanaged arrays (`ArenaArray<float>`) inside a deterministic loop.
- **Branching logic** for toggling Burst vs. non-Burst noise generation, testing performance deltas.
- **Garbage collection tracking** via `GC.CollectionCount()` before and after the operation.
- **Timing and telemetry** captured with `Time.realtimeSinceStartup` and stored in structured `BenchmarkRecord`s.
- **All data points**—timing, memory, GC pressure—are appended to a log for later analysis/export.

> *Skills demonstrated:* performance instrumentation, real-time metrics tracking, Burst-aware conditional logic, and systems benchmarking.

![BenchmarkHarness](https://github.com/user-attachments/assets/f47640d3-68dd-4f34-8d7d-01955ee204ac)

### 📌 `ArenaLog.Log` – Custom Structured Logging with Severity and Formatting

A centralized logging method that formats debug output with color-coded severity, optional source tagging, and conditional logging controls:

- **Color-coded log levels** (Info, Warning, Error, Success) for easy scanning in Unity’s console.
- **Dynamic prefix generation** based on the object type or name of the source emitter.
- **Formatted output** using inline rich text markup (e.g. `<color=#FF0000>`), tailored for Unity’s log viewer.
- **Conditional activation** based on a runtime config flag (`EnableLogging`).
- **Persistent logging** via appending formatted messages to an internal output list for potential saving or reporting.

> *Skills demonstrated:* structured diagnostics, visual clarity in debug tooling, flexible logging system design, and runtime customization.

![CustomLogging](https://github.com/user-attachments/assets/7ff5bf70-9a63-43d0-920f-e872e3b5c7a1)

### 📌 `ArenaMonitor.PrintSummary` – Memory Diagnostics and Alignment Analysis

Generates a formatted summary of all recorded memory allocations across live arenas, including over-alignment statistics and optional tagging.

- **Allocation introspection**: Iterates over tracked arenas to compute per-instance over-alignment waste ratios.
- **Per-record breakdown**: Outputs details for each allocation, including offset, size, alignment, and optional tags.
- **Memory efficiency analysis**: Reports percentage of arena capacity lost to alignment padding, enabling tuning of allocator behavior.
- **Human-readable formatting**: Produces a structured summary string for logging or export.

> *Skills demonstrated:* runtime analytics, memory instrumentation, log formatting, and tooling to support performance-critical systems.

![PrintSummary](https://github.com/user-attachments/assets/3d06cfaf-fe47-4ca5-88d2-41e67858f58a)
