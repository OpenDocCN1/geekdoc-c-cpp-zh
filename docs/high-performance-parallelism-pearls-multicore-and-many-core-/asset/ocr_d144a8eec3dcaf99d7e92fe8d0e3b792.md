| Override macro flags | Architecture | Compiler | Target flag |
|---|---|---|---|
| `-D_OV_NOAUTO -D_OV_MIC` | Intel KNC KNF | Intel C++ | `-m mic` |
| `-D_OV_NOAUTO -D_OV_AVX` | Intel AVX | Intel C++ | `-xAVX` |
| `-D_OV_NOAUTO -D_OV_AVX2` | Intel AVX 2 | Intel C++ | `-xCORE-AVX2` |
| `-D_OV_NOAUTO -D_OV_AVX512` | Intel AVX 512 | Intel C++ | `-xCORE-AVX512` |
| `-D_OV_NOAUTO -D_OV_AVX` | Intel AVX | g++/llvm | `-mavx` |
| `-D_OV_NOAUTO -D_OV_AVX2` | Intel AVX 2 | g++/llvm | `-mavx2` |
| `-D_OV_NOAUTO -D_OV_SSE` | Intel SSE | g++/llvm | `-msse` |
| `-D_OV_NOAUTO -D_OV_SSE4` | Intel SSE4 | g++/llvm | `-msse4` |
| `-D_OV_NOAUTO -D_OV_SSE` | Intel SSE | Intel C++ | `-xSSE` |
| `-D_OV_NOAUTO -D_OV_SSE4` | Intel SSE4 | Intel C++ | `-xSSE4.1` |
| `-D_OV_NOAUTO -D_OV_NEON` | ARM Neon | g++/llvm | `-mfpu=neon` |
| `-D_OV_NOAUTO -D_OV_NEON` | ARM Neon 64 bit | g++/llvm | — |
| `-D_OV_NOAUTO -D_OV_ALTIVEC` | IBM Altivec | g++ | `-mvsx -maltivec` |
| `-D_OV_NOAUTO` | Any (scalar) | Any | Any |

# FIGURE 24.12

Compiler flags.

In all of our tests auto-detection worked fine so we found no need to use override macro flags. With the Intel Parallel Studio Compiler suite, you can use -xHOST to get the highest architecture set optimization for the machine that’s compiling the code.

OpenVec is C89 compliant but some provided C examples use loop initial declarations which require the -std=c99 flag. The macro ov_restrict is defined and works as a C99 restrict modifier, so it can be used both in C and C++ codes.

# REAL-WORLD EXAMPLE

Modern seismic acoustic imaging techniques like reverse time migration (RTM) and full waveform inversion are based on computing finite difference (FD) to model and generate the image of geological volumes, which in turn are used to find new reserves of oil and gas. Hence, optimizing this type of computations leads to performance improvements in seismic imaging processing.