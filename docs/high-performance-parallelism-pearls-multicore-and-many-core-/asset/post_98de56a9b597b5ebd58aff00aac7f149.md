
Portable vectorization (Continued)
  SIMD vectorization, 464
  SIMD width, 465
  vector tail, 475
Power analysis
  NWPerf, 499–500
  OpenMP affinity, 488
  performance measure and usage, 487
  plots (see Plots, power analysis)
  power management features, 488
  power measurement options, 489–493
  power optimization, 487
  power savings, 4, 487–488
  waterfall charts, 500
Power management features
  idle states (C-states), 488
  performance states (P-states), 488
Power measurement options
  data collection, 492–493
  methodology, 489–492
  NPB EP benchmark, 489
Power wall, 463
pragma omp parallel, 353
#pragma SIMD, 129–130
Prefetching
  compiler settings, 410
  configuration, 410–411
  coverage, 407, 409f
  efficiency, 407–408, 409f
  event counters, 410, 410f
  formulation of, 410, 410f
  hardware prefetching, 403–404, 408
  importance, 401–402
  loop optimization report, 410, 411f
  OpenCL, 363–364, 363f
  out-of-order processor, 402–403, 416
  performance measurement, 408
  prefetching-enabled configurations, 408, 409f
  QphiX-CODEGEN, 162–163
  software prefetching, 403, 403f, 409
  tuning prefetching, 3, 405–407
Prefetch tuning, 3
Protein Data Bank (PDB), 56
PThreads threading model, 235–236, 235f
PyFR, 244
  advection-diffusion problems, 260
  offloading, 3, 261–262
  performance of, 267
  runtime code generation, 260–261, 263f
PYMIC_DEBUG, 250
pyMIC offload module, 245
  architecture of, 248f
decompression, 252f
design of, 244–245
DFT algorithm, 252–253
dgemm operation, 246, 247f
GPAW, 252–259
high-level interface, 245–248
kernel function, 246
low-level interface, 248–249
performance of, 264
singular value decomposition, 249–251
PYMIC_TRACE, 250
Python, 3, 243–268
  add-on packages, 243
  GPAW, 243–244, 252–259
  PyFR, 244, 260–262
  pyMIC offload module, 244–249
Q
QPhiX
  benefits, 166–168
  blocking, 153–154
  data layout for vectorization, 151–153, 152f
  data types in, 152, 152f
  definition, 151
  load balancing, 153–154f, 154–155
  loop structure, 157, 158f
  performance results for, 164–168
  SMT threads, 155–156, 156f
QphiX-CODEGEN, 157
  BAGEL generator, 159
  code generation, 163–164, 164f
  Dslash generation, 160–161, 161–162f
  implementations of instructions, 159–160
  objects, 159
  prefetching, 162–163
  structure of code, 159
Quantum chromodynamics (QCD), 139
Quantum simulations, multilevel parallelism in
  accurate approximate solutions, 335–337
  computational granularity, 353
  data locality, 353
  DGEMM experiments, 346–347
  diffusion, 350, 351–352f, 352
  ES applications, 338–340, 339f
  FFT experiments, 347
  load balance, 353
  multi-and many-core architectures for, 341–343
  reference application, 337–338
  setting up experiments, 343–347
  user code experiments, 347–352

## R
- Radio frequency ray tracing (RFRT)
  - advantages, 212
  - classical ray-based methods, 213, 214f
  - ispc, 224–225
  - Monte Carlo path tracing, 213, 213–214f
  - OpenMP, 218–224
  - optical ray tracing, 212
  - optimization, 217–225
  - ray paths connecting source and receiver are found, 212
  - StingRay, 211–216, 212f
  - wave equation, 212
- Ray tracing, 3, 211–212, 218
- Registered address space (RAS), 95, 98f
- Registered windows, 95
- Remote memory access (RMA)
  - mapping via scif_mmap(), 98, 99f
  - MPI'S interprocess shared memory extension, 306
- Reserved core, 4
  - coprocessor simulation (see Coprocessor-side simulation)
  - host-side simulation, 240, 241f
  - machine configuration, 237
  - PThreads, 235–236, 235f
  - scatter affinity pattern, 236, 236f
  - simulation configuration, 237
  - thread affinity pattern, 234–235
- Retail industry, visual search application, 197
- Reverse Monte-Carlo ray tracing (RMCRT), 230, 231–232f
- Right-looking Cholesky factorization, 290, 290f
- Rodinia benchmarks
  - BFS benchmark, 397
  - CFD, 395–396, 396f
  - HotSpot (see HotSpot benchmark)
  - LUD, 379, 394, 395f
  - NW, 397
- Root-mean-square deviation (RMSD), 64–66, 65–66f

## S
- Same instruction, multiple-thread (SIMT)
  - memory layout optimization, 360–361
  - Nvidia GPGPU-specific optimizations, 367
  - vectorization in OpenCL, 360
- Scalable heterogeneous computing molecular dynamics (SHOC MD) benchmark, 401–402
  - hardware prefetching, 417, 417–418f
  - intrinsic prefetches, 412–416, 413f, 415f
- Scalar optimization
  - American call options pricing, 121f
  - compiler invocation switches, 116–118
  - Intel Xeon processor impact, 120, 122f
  - reuse and reinvent, 119–120
  - subexpression evaluation, 120–121
  - transcendental functions, 119
- Scale-and-vectorize approach, 44–45
- Scale-Invariant Feature Transform (SIFT)
  - keypoint descriptor, 195
  - keypoint localization, 195
  - orientation assignment, 195
  - scale-space extrema detection, 194–195
  - visual pattern matching using, 192–194, 194f
- Scale-space extrema detection, 194–195
- Scatter affinity pattern, 236, 236f, 239f
- scif_mmap()
  - buffer on coprocessor, 102f
  - data transfer using, 101f
  - memcpy, 101
  - producer-consumer model, 104f
  - remote memory mapping via, 98, 99f
  - write combining memory, 98, 102–104
- scif_register(), 95–98
- SciPy, 243
- Selective affinity pattern, 240f
- Self-consistent field method (SCF), 337–338
- SHAKE algorithm, 86
- Shared-memory parallelism, 10–11. See also OpenMP
- simdlen, 426–439, 460
- SIMD parallelism
  - arithmetic operations, 123
  - branch statements, 124–126
  - calling vector and scalar version, 126–128
  - C/C++ vector extension, 129–130
  - definition, 122
  - extension syntax, 122, 123f
  - function call, 124
  - intrinsic syntax, 122, 123f
  - #pragma SIMD, 129–130
  - source code annotation, 129, 130f
- Single instruction multiple data (SIMD). See also OpenMP
  - compiler options, 423, 429–430
  - instruction-level parallelism in, 43
  - instruction sets, 218
  - Intel AVX-512 vector instruction set, 430, 430f
  - multiple processor architecture support, 432–433, 433f
  - performance benefits, 422, 423f
  - processor(...) clause, 429–430, 432
  - vectorization, 422, 422f
  - and vectorization, 2
  - vectorization using, 46–47, 47f
  - YMM registers, 431, 431f
- Singular-value decomposition (SVD), 249–251

## 522 Subject Index

Smith-Waterman (SW) algorithm, 43, 44f, 53, 401–418, 412–413f, 417f
hardware prefetching, 416, 417f
prefetch distance tuning, 411–412, 412f
SMT threads, QPhiX, 155–156, 156f
Social interactions, visual search application, 197
StingRay, 211–212, 212f
components, 215–216, 215f
Extensible GUI, 216
pipelined rendering, 215, 216f
plug-in architecture, 215
simulation and visualization of, 213
traditional volume rendering techniques, 216, 217f
visual elements, 216
Streams, 3, 272
actions, 286–287
application programming interfaces, 288, 288f
benefits, 272
building blocks, 286–288
Cholesky factorization, 290–296
computing challenge, 271–272
definition, 272
FIFO stream abstraction, 289–290
framework, 284–290
heterogeneous architectures, 297
independent software vendors, 285–286
lack adequate data parallelism, 297–298
library, 284–290, 297–298
LU factorization, 296–297
matrix multiplication, 272–284, 301–304
offload program, 277–280, 294, 295f
source and sink-side application code, 289f
synchronization to asynchronization, 298
task-related parallelism, 285
working on, 297
Stream Triad, 357, 401–416, 404f, 409f, 411–412f
hardware prefetching, 416, 416f
prefetch distance, 410–411, 411f
prefetching metrics, 407–410, 409–410f
Structural bioinformatics, parallelism and, 56
Structure of Arrays (SoA), 360–361, 362f, 395
Surveillance, visual search application, 197
Symmetric Communication Interface (SCIF), 94–98
API, 94, 96f
client side of, 96f
registered address space, 98f
server side of, 97f
and user mode library, 95f

## T
Threading, 441, 442f
Threading Building Blocks (TBB) memory allocation, 73–74, 132, 132f
Threads
database level parallelism, 198–199, 198–199f
FLANN threads scaling, 204
in naive code, 147–148, 148f
optimal scheduling, loop nest, 175–177, 177f
parallelization, 130–133
Thread-safe timers, 2, 19
Transcendental functions, 119
Translation Lookaside Buffer (TLB), 392
Tuning prefetching, 401–402
indirect array access, 405, 407f
on Intel Xeon Phi Coprocessors, 402–404
prefetch distance, 407
SHOC MD, 405
Smith-Waterman algorithm, 405
strategies, 405
Stream Triad, 404–405, 404f

## U
Uintah computational framework (UCF)
ARCHES, 229
cross-compilation, 230, 233–234, 233f
ICE, 229
MPM, 230
MPM-ICE, 230
radiation modeling, 230

## V
VCLKNC, 374–376
Vc project, 373
Vector Class Library (VCL), 373
Vectorization, 422, 422f
arithmetic operations, 123
balancing overheads, 453
branch statements, 124–126, 126f
in C++, 434–438, 436–437f
calling vector and scalar version, 126–128
C/C++ vector extension, 129–130
in C, Interpolate() function, 383–385f, 423, 426
data layout for, 151–153
definition, 122
DL_MESO_LBE
Cartesian coordinate system, 443
3D_PhaseSeparation benchmark, 443, 443f
properties and features, 442–443
experimentation life cycle, 444–445, 445f
experiments, 460, 460–461f
explicit vectorization, 421, 449
extension syntax, 122, 123f
in Fortran, 438, 439f
function call, 124
gain and efficiency, 456–457
