| c0004209 | 1 | 0 | 1 |
| b72a37805 | 4 | 0 | 1 |
| b50409 | 2 | 0 | 1 |
| b52809 | 4 | 0 | 1 |
| b7731dc05 | 6 | 0 | 1 |
| bbec09 | 6 | 0 | 1 |
| bbfc09 | 6 | 0 | 1 |
| c6018105 | 4 | 0 | 1 |
| 772a1405 | 2 | 0 | 1 |
| 94a4209 | 1 | 0 | 1 |
| 77334a05 | 5 | 0 | 1 |
| 7733a209 | 1 | 0 | 1 |
| 773317405 | 2 | 0 | 1 |
| 772d6605 | 3 | 0 | 1 |
| a71409 | 2 | 0 | 1 |
| c1d409 | 2 | 0 | 1 |
| 772d4a05 | 5 | 0 | 1 |
| 77342c05 | 6 | 0 | 1 |
| 6c80f605 | 3 | 0 | 1 |
| 77320405 | 2 | 0 | 1 |
| 77323205 | 1 | 0 | 1 |
| 77323145 | 2 | 0 | 1 |
| 7ffe0215 | 1 | 0 | 2 |
| a5fc069 | 6 | 0 | 1 |
| 7735cc05 | 6 | 0 | 1 |

Notice that some entries in the working set are list pages (the ones with addresses greater than 0x0C000000), some are from system DLLs (the ones in the 0x7nnnnnn range), and some are from the code of Windbg.exe itself.

# # Balance set manager and wrapper

Working set expansion and trimming take place in the context of a system called the balance set manager (KeBalanceSetManager function). The balance set manager is created during system initialization. Although the balance set manager is technically part of the kernel, it calls the memory manager's working set manager (MmWorkingSetSetManager) to perform working set analysis and adjustment.

The balance set manager waits for two different events: an event that is signaled when a periodic timer set to once or twice per second expires and an internal working set manager signals at various points when it determines that working sets need to be adjusted. For example, if the system is experiencing a high page fault rate or if the list is too small, the memory manager wakes up the balance set manager so that it will call the working set manager to begin working sets. When memory is more plentiful, the working set manager permits fault processing to gradually increase the size of their working sets by paging back into memory. However, the working sets will grow only as needed.