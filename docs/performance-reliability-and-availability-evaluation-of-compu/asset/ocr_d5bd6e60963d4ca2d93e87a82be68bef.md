# Performance Measuring

383

```
system--bo--io--cpu--id--wa--st--timestamp
--swap--swap--cache--memory--free--swapped--procs
2 0 106000 281400 523548 523548 0 2020-05-05 15:33:12
1 0 106000 208896 523548 523548 0 2020-05-05 15:33:17
1 0 106000 208896 523548 523548 0 2020-05-05 15:33:22
1 0 106000 208688 523556 523556 0 2020-05-05 15:33:27
1 0 106000 280688 523556 523556 0 2020-05-05 15:33:32
1 0 106000 280688 523556 523556 0 2020-05-05 15:33:37
```

The vmstat output is divided into five sections: procs, memory, swap, io, system and cpu. The cpu section has the following identifications:

+   * r - The number of processes in a wait state.
* b - The number of processes that were in sleep mode.
* w - The number of processes that have been swapped out by memory management and virtual memory subsystems and have yet yet to run.