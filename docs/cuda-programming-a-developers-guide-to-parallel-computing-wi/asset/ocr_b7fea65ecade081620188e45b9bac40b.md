![](bbox=[0.226, 0.113, 0.752, 0.535])

# **FIGURE 9.53** Halo cells needed.

```
else if (bottom row)
else if (left row)
else (must be centre element)
```

Particularly, control complex algorithms are not well suited to GPUs. If each thread runs the same kernel, the center elements have nine conditions to test before the thread does any work on them. Reversing the order of the tests, so the center elements are tested first, means we need four boundary tests. This would be an improvement, but is still far from optimal. The solution is to write customized kernels for each special case or let the CPU handle these complex conditionals.

The type of problem here is a stencil one, where cells N levels from the center contribute in some way to the result. In this simple example, N is 1, as the immediate neighbors are used. As N is increased, typically some factor is applied, as values that are a long way from the center often do not contribute as much to the result.

As each cell will need values from the surrounding cells, each cell value will be read multiple times. Thus, a common approach to such problems is to use many threads to read a tile of data into shared memory. This allows for high-performance coalesced access to global memory, both when