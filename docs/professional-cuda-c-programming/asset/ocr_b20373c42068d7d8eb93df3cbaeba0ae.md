single-precision CUDA cores, 64 double-precision units, 32 special function units (SFU), and 32 load/store units (LD/ST) (shown in Figure 3-7).

| Instruction Cache |
| Warp Scheduler | Warp Scheduler | Warp Scheduler |
| Dispatch | Dispatch | Dispatch | Dispatch | Dispatch | Dispatch |
| Register File (65,536 & 32-bit) |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP Unit SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit DP/ SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit LD/ SFU |
| Core Core DP Unit Core Core DP Unit DP Unit SFU Core Core DP Unit Core Core DP Unit LD/ SFU |
| Interconnect Network |
| 64 KB Shared Memory / L1 Cache |
| 48 KB Read-Only Data Cache |
| Tex Tex Tex Tex Tex Tex Tex Tex |
| Tex Tex Tex Tex Tex Tex Tex Tex |

FIGURE 3-7

Each Kepler SM includes four warp schedulers and eight instruction dispatchers, enabling four warps to be issued and executed concurrently on a single SM. The Kepler K20X architecture (compute capability 3.5) can schedule 64 warps per SM for a total of 2,048 threads resident in