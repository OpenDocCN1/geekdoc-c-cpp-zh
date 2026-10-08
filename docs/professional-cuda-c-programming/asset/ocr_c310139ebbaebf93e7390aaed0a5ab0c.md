simpleMethAos.cu, 180–181

SIMT (Single Instruction, Multiple Thread), 8, 68
warps, 80

single-precision floating-point values, 306–308

SISD (Single Instruction Single Data), 6
SM (Streaming Multiprocessors), 68

CUDA cores, 71–72
parallelism, arithmetic utilization, 92
shared memory, 70–71
thread blocks, 70

gm function, 335
SMEM (see shared memory)
SOA (structure of arrays), 171–176
spatial locality, 210
square shared memory

column-major order, 218–220
column-major order reading, 220–221
dynamic memory, 221–222
dynamically declared, padding, 223–225
performance, 225

row-major order, 218–220
row-major order reading, 220–221
statically declared, padding, 223

SRAM (static random access memory), 137
stalled warps, 89
standard functions, 303–304
visualizing, 309–311
static global, 143–145
statically declared, padding, 223

stencils
2D wave equation, multi-GPU, and 400–401,
403–405

constant memory, 250–253
stream callbacks, 295–297
stream priorities, 273
streams, 268–269
asynchronous, 275
blocking streams, 275–276
default, blocking behaviors, 287–288
dispatching operations, OpenMP and, 283–284
environment variables, 284–286
events, 273–274
false dependencies, 284
Fermi GPUs, 281–283

grid level concurrency, and 268
inter-stream dependencies, 288–289
non-blocking, 276
NULL, 269
coarse-grain concurrency, 269
NULL, 269
scheduling, 271
false dependencies, 272
HHyper-Q, 272
synchronization, 275–276
blocking streams, 275–276
event configuration, 278
explicit, 277–n8non-blocking streams, 275–276
synchronous, 275
str(),(), 27
suggested reading, 489–492
sumArrayGPU-small-case.cu, 40–42
sumArrayGPU(), function, 39
sumArrayGPU-timer.cu, 45–46
sumArrayZerocopy.cu, 151–156
sumArrayZerocopyUVA, 162
sumMatrix, 100–101
sumMatrix, 99
sumMatrixGPU, 446
sumMatrixManaged, 195, 205–206
sumMatrixGPU-1d-grid-block.cu, 58
sumMatrixGPU2D, 98
sumMatrixGPU2D-2d-grid-block.cu,
54–56
sumArrayHost() function, 53–54
sv, 333
witch-case structure, 121
synchronization, 275–276
multi-GPUs, 392–393
warps, 96–98
synchronous behavior of functions, 268
synchronous streams, 275
blocking streams, 275–276
events, configuration, 278
explicit, 277–278
implicit, 276–277