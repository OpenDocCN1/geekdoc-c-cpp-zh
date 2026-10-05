# 8.1. Graphics coprocessor architecture

| Mem ctrl | Mem ctrl | Mem ctrl |
| :--- | :--- | :--- |
| L1/shared | Multiprocessor | L1/shared | Multiprocessor |
| L1/shared | Multiprocessor | L1/shared | Multiprocessor |
| L1/shared | Multiprocessor | L2 cache |
| L1/shared | Multiprocessor | L1/shared | Multiprocessor |
| L1/shared | Multiprocessor | L1/shared | Multiprocessor |
| L1/shared | Multiprocessor | L1/shared | Multiprocessor |
| Mem ctrl | Mem ctrl | Mem ctrl |

Figure 8.2: The Kepler microarchitecture consists of 13 multiprocessors and 6 memory controllers.