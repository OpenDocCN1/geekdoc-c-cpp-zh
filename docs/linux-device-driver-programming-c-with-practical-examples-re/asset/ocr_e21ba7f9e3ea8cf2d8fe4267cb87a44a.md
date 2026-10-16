+   - Requires careful configuration to avoid performance overhead.

# LTTng

LTTng is a more advanced tracing framework that provides better scalability and flexibility.

# Features:

+   - Supports multiple tracepoints and buffers.
+   - Offers filtering and aggregation capabilities.
+   - Can be used for user-space and kernel-space tracing.

Usage: LTTng requires configuration and compilation of the kernel with LTTng support.

Bash

```
lttng create session my_session
lttng enable-channel my_channel
lttng start
```

# Profiling

Profiling measures the performance of a program by determining how much time is spent in different parts of the code.

Perf

Perf is a built-in kernel tool for performance analysis.

+   - Basic Usage:

Bash

```
perf record -e cycles,cache-misses ./my_program perf report
```

This records cycle counts and cache misses for the specified program.

+   - Kernel Events: Perf can measure various kernel events, such as CPU cycles, cache misses, page faults, and more.