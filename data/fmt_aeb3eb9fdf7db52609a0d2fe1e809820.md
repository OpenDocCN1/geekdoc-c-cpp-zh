
# 索引

- `main()`, 显示指针和数组, 16
- `main()`, 练习 `Vector` 类, 33
- `MPI`, `all2final()`, 456
- `MPI`, `all2all_final()`, 459
- `MPI`, `all2all_init()`, 458
- `MPI`, `bcast()`, 453
- `MPI`, `BlockDivide()`, 429
- `MPI`, `copywlda()`, 438
- `MPI`, `main()`, 373
- `MPI`, `mpi_all2all()`, 456
- `MPI`, `mpi_initialize()`, 376
- `MPI`, `read_mpi()`, 464
- `MPI`, `reducesum()`, 460
- `MPI`, `scatter_all()`, 455
- `MPI`, `transposeall()`, 435, 439
- `MPI`, `unsafe()`, 377
- `MPI`, `write_mpi()`, 461
- `mmreg`, 365
- `mult300x200x300()`, 263
- `mult4x200x12()`, 259
- `mult600x200x12()`, 261
- `mult600x200x300()`, 262
- `multJK()`, 176
- `multJK()`, 175
- `multJK()` 使用 C++, 179
- `multJKX()`, 176
- `OpenMP`, `addone()`, 328
- `OpenMP`, `addtwo()`, 328
- `OpenMP`, `blocktrans()`, 310
- `OpenMP`, `blocktran()`, 310
- `OpenMP`, `copy_onecore()`, 309
- `OpenMP`, `init_manycore()`, 306
- `OpenMP`, `ompfor()`, 295
- `OpenMP`, `opmpaster()`, 328
- `OpenMP`, `parallelA()`, 299
- `OpenMP`, `parallelfor()`, 293
- `OpenMP`, `printstuff()`, 298
- `OpenMP`, `sum_manycore()`, 308
- `OpenMP`, `sum_onecore()`, 308
- `OpenMP`, `write_onecore()`, 309
- `packA()`, 262
- `packB()`, 263
- `partialsum_client()`, 487
- `partialsum_server()`, 484
- `print_ipaddr()`, 480
- `print_spinlock()`, 321
- `print_info()`, 478
- `printseq()`, 22
- `Threads`, `addone()`, 324
- `Threads`, `addone_init()`, 325
- `Threads`, `assignwork()`, 337, 341
- `Threads`, `call_pthreads()`, 318
- `Threads`, `exitifn()`, 331, 336, 343
- `Threads`, `leibniz()`, 323
- `Threads`, `leblum()`, 323
- `Threads`, `manager()`, 323, 338, 345
- `Threads`, `shutdown()`, 340
- `Threads`, `shutdown_workers()`, 333
- `Threads`, `spawn_workers()`, 332
- `Threads`, `worker()`, 330, 336, 339, 343
- `randomp()`, 241
- `read_direct()`, 269
- `read_easy()`, 268
- `run()`, 365
- `run1()`, 361
- `run2()`, 362
- `run3()`, 364
- `run4x200x12()`, 260
- `saddlerlit()`, 477
- `server()`, 485
- `sincos()`, loop_fusion, 168
- `sinetable()`, 170
- `stride()`, 239
- `sum()`, 248
- `sum()`, basic template, 47
- `sum_arr()`, 359
- `sumstride()`, 250
- `sumstride()`, 249
- `testlu()`, 85
- `time_unit()`, 238
- `unitsstride()`, 238
- `unpack_()`, 261
- `verify_dir()`, 85
- `write_direct()`, 269, 273
- `write_easy()`, 268
- `write()`, 269
- `system()`, 86
- `Xeon Phi`, `homic_scale()`, 511
- `Xeon Phi`, `homic_sum()`, 511
- `Xeon Phi`, `leibniz()`, 514
- `Xeon Phi`, `leibniz_init()`, 511
- `Xeon Phi`, 516
- `Xeon Phi`, `munit()`, 532
- `Xeon Phi`, `xfer()`, 222

## 编译器的选择, 194

### 编译语法
- `-I` 指定头文件目录, 93
- `-MD` 和 `-MP` 依赖头文件, 93
- `-W` 选项, 93
- `-c` 仅编译, 90
- `-fopenmp`, `open.287`, 291
- `-mm` 用于 `Xeon Phi`, 499, 504
- `-prec-div` 和 `-nopt` 选项, 93
- `-restrict` 选项, 223
- `-restrict_option`, 159
- `-xHost`, `-O3 -fast` 优化, 23

`C++`, 50

`gcc/g++`, 586

在 `CUDA`, 557

`MPI`, 374

`pthreads`, 319

使用的选项, 159

### C/C++ 库函数
- `close()`, 269
- `fopen()`, 269
- `fread()`, 269
- `fwrite()`, 267
- `fseek()`, 272
- `write()`, 269
- `system()`, 86

### C/C++ 宏
- `#include`, `#ifndef`, `#define`, `#endif` 指令, 11
- `+plusplus`, 68
- `assert()`, 17, 29
- `asrt()`, 84

编译器优化，另见 依赖

循环融合, 169

循环交换, 176

循环展开, 166

手动循环展开, 166

循环体内的并行性, 165

未优化代码的缓慢, 161

展开并合并 `unroll and jam`, 172

### C/C++ 工作线程
`spawn_workers()`, 345

缓存内存, 222, 另见 内存优化、内存系统, 225, 230

缓存一致性, 234

缓存行 `64 字节`, 231

编译器不可预测性, 156

`CUDA`, 另见 `GPU/CUDA`

`CUDA/GPU*`.

`K20`, 微架构, 546

`AVX2` 指令的理论下限, 125

### 依赖
- 由循环携带, 182
- `RAW`, 181
- `RAW`, 181
- `WAR`, `WAR`, 181

解引用运算符 `*`, `Linux`

反汇编器，另见 `GNU/Linux,objdump`

`DRAM` 内存, 227, 另见 内存优化、内存系统

列表数组, 226

存储库, 227

拷贝带宽

`DDR` 双数据速率, 229

`DDR` 预取长度, 229

`MIMMs`, 226

发明, 224

延迟定义, 238

延迟估计, 245

延迟测量, 242

内存通道, 228

秩, 228

读取带宽, 249

与 `SRAM` 比较, 224

### FFTW 库
- 与 `MKL` 和 `Numerical Recipes` 的比较, 125
- 编译与链接语法, 94
- 归一化正变换, 127
- 一维复数间变换, 121

### Fortran, 72
- 不使用指针的数组, 53
- 字符的处理, 74
- 与 `C/C++` 链接, 64
- 比 `C/C++` 快, 53
- 引用传递语义, 54

### 一般原则
- 在高性能计算中, xiv
- 负载均衡, xv, 429
- 处理器与网络活动, 441

### GNU make, 另见 make 工具

`GNU/Linux`, xiv
- `/etc/services`, 482
- `alloc_pages()`, 281
- 清理页面缓存, 271
- 内核复杂度, 275
- 系统调用代价, 352
- 定义系统调用, 350
- 需需分页，首次触摸, 284
- `demycode` 命令, 228
- `exxec()` 系统调用, 110
- 提取拥塞窗口, 493
- `getconf` 命令, 235, 274
- `GIT`, 584
- `ibv_devinho` 命令, 388
- `ifconfig` 命令, 476
- 日志文件, 273
- `kmalloc()`, 281
- `ld.so` 动态链接器, 110
- `ldconfig` 命令, 110
- `lld` 命令, 109
- 线性映射内核内存, 280
- `lspci` 命令, 267
- `mmap()` 系统调用, 110
- `nm` 命令, 61
- `objdump` 命令, 200
- 页代码, 267
- `PAGE_OFFSET`, 276
- 用于打开管道的 `open()` 系统调用, 580
- `read()` 系统调用, 267
- 栈不收缩, 364
- `struct sk_buff`, 492
- 系统调用, 348
- `traceroute` 命令, 489
- `ulimit` 命令, 356
- 虚拟地址到线性地址, 282
- `vm area`, 358
- `vmalloc()`, 加载模块, 281
- `cuobjdump`, 539
- `DirectX`, `OpenGL`, 535
- 函数, `add()`, 567
- 函数, `atomicAddDouble()`, 559
- 函数, `copy()`, 567
- 函数, `leibniz()`, 559
- 函数, `leibniztotal()`, 558
- 函数, `mmult()`, 569
- 函数, `mmult_gemm()`, 568
- 函数, `mmult_stem()`, 570
- `functions.leibniz()`, 554
- 线程块网, 548, 550
- `gridDim.x`, 554
- 指令流水线优化, 566
- `K20`, 540
- `K20` 设备, 538
- 内核级调用, 556
- `launch_parameters()`, 553
- 内存带宽, 568
- 内存系统, 550
- `DirectX` 的模块化, 537
- `vcc`, 539
- `vcc` 语法, 567, 565
- 模块化较差, 538
- 编程更困难, 536
- `PTX`, 564
- 共享内存, 570
- 线程块, 548, 549
- `threadIdx.x`, 554
- `warp` 散散, 558
- `warps`, 549

### GPU/CUDA
- `_device_` 限定符, 553
- `_global_` 限定符, 553
- `_syncthreads()`, 539
- `atomicEx()`, 560
- `blockDIM.x`, 554
- `blockIdx.x`, 554
- `C++` 类, `cumult`, 573
- `C++` 类, `dhtmem`, 541
- `C++` 类, `hstimer`, 544
- 计算能力, 539
- `const_hh`, 552
- `cuBLAS`, 573
- `CUDA`, 530
- `cudaEventCreate()`, 545
- `cudaEventDestroy()`, 545
- `cudaEventElapsedTime()`, 545
- `cudaEventRecord()`, 545
- `cudaEventSynchronize()`, 545
- `cudaDeviceCount()`, 539
- `cudaGetDeviceProperties()`, 539
- `cudaMalloc()`, 543
- `cudaMemcpy()`, 539

图形处理器单元，参见 `GPU/CUDA`

- 硬盘, 224
- 带宽, 273
- 与 `DRAM` 相比, 268
- 延迟, 272
- `Infiniband`, 381, 另见 网络 `Networks`
- 完成队列, 391
- 数据包格式, 387
- 主机通道适配器, 389

### 索引

#### 593
- `ib_allocate_pd()`, 390
- `ib_deallocate_pd()`, 390
- `ib_post_recv()`, 390
- `ib_post_send()`, 390
- `ib_read_bw`, 394
- `ib_read_lat`, 394
- `ib_write_bw`, 394
- `ib_write_lat`, 394
- `ib_devreg_mr()`, 392
- `ib_devinfo_command`, 388
- `ib_devreg_mr()`, 392
- `MTU`, 388
- 分包化, 386
- 保护域, 390
- 队列对, 391
- `RDMA`, 382
- `RDMA` 延迟和带宽, 394
- `RDMA`, 293
- `RDMA` 写, 393
- 目标通道适配器, 389
- `Verb` 层, 390
- 指令流水线, 186
- 消除依赖关系, 189
- `Haswell`, 190
- `Nehalem/Westmere`, 190
- `RAW` 依赖, 189
- 指令流水线优化, 186
- 通用讨论, 136
- 几年来收益的快速增长, 138
- 指令级并行, 164
- `Intel MIC`, *参见* `Xeon Phi`
- `Intel MKL` 库, *参见* `MKL` 库
- 互联网, 472, *另见* `TCP/IP`
- 密歇根与得克萨斯之间的带宽, 492
- 带宽，与硬盘, `DRAM` 相比, 474
- 在科学计算中, xviii
- 密歇根与得克萨斯之间的延迟, 498
- 雅比迭代, 417
- `LAPACK`, *参见* `BLAS/LAPACK`
- 数组的主维, 73
- 莱布尼茨级, 4
- 库, xv, 58, *另见* `BLAS/LAPACK`, `FFTW`, `MKL`
- 共享库的*共享选项*, 107
- 用于构建静态库的 `ar` 工具, 108
- 全局链接表, 111
- `dd.so` 动态链接器, 110
- `LD_LIBRARY_PATH`, 108
- `ldconfig` 工具, 110
- `dd` 工具, 109
- 过程链接表, 111
- 共享库的搜索顺序, 110
- 链表
    - 基础示例, 45
    - 优化, 135, 248
    - 与数组相比, xvii
- 链接
    - 寻找 `Fortran` 运行时库, 67
    - `Fortran` 到 `C++`, 67
    - `C` 语言 `Fortran`, 64
    - 链接器做了什么, 62
    - 链接语法
    - 指定目录的 `-L` 选项, 94
    - `-FPIC` 选项, 108
    - `-fopenmp,-openmp`, 287, 291
    - `-lpthread`, 319
    - `icpc` 中的 `-mkl=sequential`, 80
    - 输出到文件的 `-o` 选项, 90
    - *共享选项*, 107
    - `C`, 24
    - `C++`, 50
    - `gcc/g.`, 586
    - `MPI`, 375
    - `Linux`, *参见* `GNU/Linux`
    - 负载均衡, xv
    - 对数级数, 5

#### 594

索引

- 循环展开, 参见 编译器优化
- `lustre` 文件系统, 401, 465
- `- lfs` 条, 466
- `lfssetstripe`, 668
- `- 页缓存`, 470
- 使用的机器, 578
- `Sangagra`, 4, 168
- `make` 工具, xv, 81
- 自动变量, 94
- 默认后缀, 95
- 头文件依赖关系, 100
- 依赖图, 87
- 内置和包含指令, 101
- `make` 的限制性, 103
- `make` 变量, 92
- 规则, 94, 95
- 像 `clean` 的目标, 98
- 前提, 87
- 配方, 88
- 递归 `make`, 99
- 简单 `Makefile`, 88
- 特殊 `tabs`, 89
- 目标, 87
- 两遍结构, 89
- 矩阵乘法，参见 内内核, 209
- 矩阵转置, 251, 310, 431
- 内存分配, 236
- `__malloc()`, 122, 200
- `malloc()`, 40
- 内存 `fence`, 300, 333
- 内存优化, 参见 `Cache`
- 内存系统, 223, *另见* `Threads and shared memory`
- 阻塞, 247, 253
- 缓存利用率, 178, 246, 250
- 更改格式到 `TLB`
- 缓存缺失, 257
- 多级 `TLB` 和缓存, 259
- 链表和延迟, 248
- 矩阵乘法, 256
- 2, 255
- 为什么阻塞有帮助, 254
- 内存金字塔, 221
- 内存系统, 参见 `DRAM`, `Cache`
- 内存优化, textual
- 对 `FFT` 计数的影响, 124
- 到缓存的延迟, `DRAM`, 226
- 暴露的链表, 226
- 内存控制器, 228
- 并行性, 225
- 段错误, xviii, 394
- 分页系统, 357
- 到 `DRAM` 的典型带宽, 249
- 消息传递接口，参见 `MPI`
