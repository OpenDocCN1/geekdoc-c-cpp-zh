# Matrix Addition with Unified Memory

| KERNEL OR RUNTIME FUNCTIONS | WITH MANAGED MEMORY | WITHOUT MANAGED MEMORY |
|---|---|--|
| CPU data initialization | 5930.17 | 1835.07 |
| CPU matrix Addition | 504.63 | 474.37 |
| CPU timer on Matrix Kernel | 25.203 | 20.226 |

Matrix Size: 4096 x 4096; Unit: milliseconds

Inspecting Unified Memory is fully supported by both nvvp and nvprof. Profilers allow you to measure unified memory traffic for each GPU in system. This feature is turned off by default. Passing the following flag to nvprof enables unified memory-related metrics.

```
$ nvprof --unified-memory-profiling per-device /managed
```

--device-gpu= will also provide information on Unified Memory behavior. The report is exported from the results on a Kepler 40.

```
=28893= Unified Memory profiling result:
Device "Tesla K40m (0)"
| | Count Avg Min Max |
|---|---|---|---|--|
Host To Device (bytes) | 8 | 13422.08 | 0 | 2.68e+08 |
Device To Host (bytes) | 507 | 549050.86 | 0 | 4.03e+08 |
CPU Page Faults | 507 | 48909.01 | 0 | 98+04 |
```

Note that CPU page faults are reported alongside device-to-host transfer. A page fault occurs when a host application requests an address in CPU memory that is not in physical memory. Unified memory uses page faults to trigger device-to-host transfers when the CPU requires access to managed memory. The number of page faults is measured relative to data size. Try running the program with a small matrix of 256 x256 elements:

```
$ nvprof --unified-memory-profiling per-device /managed 8
```

The results are as follows. Note that the number of page faults is reduced greatly.

```
=29464= Unified Memory profiling result:
Device "Tesla K40m (0)"
| | Count Avg Min Max |
|---|---|---|---|--|
Host To Device (Bytes) | 2 | 524288.00 | 0 | 1048576 |
Device To Host (Bytes) | 9 | 505628.44 | 0 | 1572864 |
CPU Page Faults | 9 | 123.44 | 0 | 384 |
```

You can also check memory behavior visually using nvvp. Launch nvvp on the managed memory implementation as follows:

```
$ nvvp /managed
```

In the Executables tab labeled "Create New Session," enter 14 in the "Arguments" field to test a large matrix, and select "Next.\ Then select the "Enable unified memory profiling" box, as shown in Figure 4-32.

Figure 4-33 illustrates the timeline for the managed memory. You can see from the figure that host page faults are closely correlated with Dto Data Migration. Unified memory optimizes