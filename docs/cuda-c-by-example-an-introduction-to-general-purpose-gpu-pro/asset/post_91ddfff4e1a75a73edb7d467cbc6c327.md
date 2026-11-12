
- resources, written
- CUDA U, 245-246
- forums, 246
- Programming Massively Parallel Processors, 244-245
- ripple, GPU
  - with graphics interoperability, 147-154
  - producing, 69-74
- routine()
  - allocating portable pinned memory, 232-234
  - using multiple CPUs, 226-228
- Russian nesting doll hierarchy, 164

## S

### scalable link interface (SLI), adding multiple GPUs
- with, 224

### scale factor, CUDA Julia Set, 49

### scientific computations, in early days, 6

### screenshots
- animated heat transfer simulation, 126
- GPU Julia Set example, 57
- GPU ripple example, 74
- graphics interoperation example, 147
- ray tracing example, 103-104
- rendered with proper synchronization, 93
- rendered without proper synchronization, 92

### shading languages, 6

### shared data buffers, kernel/OpenGL rendering
- interoperation, 142

### shared memory
- atomics, 167, 181-183
- bitmap, 90-93
- CUDA Architecture creating access to, 7
- dot product, 76-87
- dot product optimized incorrectly, 87-90
- dot synchronization, 75

### Silicon Graphics, OpenGL library, 4

### simulation
- animation of, 121-125
- challenges of physical, 117
- computing temperature updates, 119-121
- simple heating model, 117-118

### SLI (scalable link interface), adding multiple GPUs
- with, 224

### spatial locality
- designing texture caches for graphics with, 116
- heat transfer simulation animation, 125-126

### splitter blocks, see parallel blocks, splitting

### parallel threads

### standard C compiler
- compiling for minimum compute capability, 167-168
- development environment, 18-19
- kernel call, 23-24
- start event, 108-110
- start_thread(), multiple CPUs, 226-227
- stop event, 108-110

### streams
- CUDA, overview of, 192
- CUDA, using multiple, 198-205, 208-210
- CUDA, using single, 192-198
- GPU work scheduling, and, 205-208
- overview of, 185-186
- parallel look-up memory and, 186-192
- summary review, 211

### supercomputers, performance gains in, 3

### surfactants, environmental devastation of, 10

### synchronization
- of events, see cudaEventSynchronize()
- of streams, 197-198, 204
- of threads, 219

### synchronization, and shared memory
- dot product, 76-87
- dot product optimized incorrectly, 87-90
- dot product, 75
- shared memory bitmap, 90-93

### __syncthreads()
- dot product computation, 78-80, 85
- shared memory bitmap using, 90-93
- unintended consequences of, 87-90

## T

### task parallelism, CPU versus GPU applications, 185

### TechniScan Medical Systems, CUDA applications, 9

### temperatures
- computing temperature updates, 119-121
- heat transfer simulation, 117-118
- heat transfer simulation animation, 121-125

### Temple University research, CUDA applications, 10-11

### tex1Dfetch() compiler intrinsic, texture memory, 127-128, 131-132

### tex2D() compiler intrinsic, texture memory, 132-133

### texture, early days of GPU computing, 5-6

### texture memory
- animation of simulation, 121-125
- defined, 115
- heat transfer simulation, 117-118
- simulating heat transfer, 117-121
- summary review, 137
- two-dimensional, 131-137
- using, 125-131

### threadIdx variable
- 2D texture memory, 132-133
- dot product computation, 76-77, 85
- dot product computation with atomic locks, 255-256
- GPU hash table implementation, 272
- GPU Julia Set, 52
- GPU Julia Set using threads, 72-73
- GPU sum of a longer vector, 63-64
- GPU sums of arbitrarily long vectors, 66-67
- GPU vector sums using threads, 61
- histogram kernel using global memory atomics, 179-180
- histogram kernel using shared/global memory atomics, 182-183
- multiple CUDA devices, 200
- ray tracing using GPU, 102
- setting up graphics interoperability, 145
- shared memory bitmap, 91
- temperature update computation, 119-121
- zero-copy memory dot product, 221

### threads
- coding with, 38-41
- constant memory and, 106-107
- GPU tile size, 69-74
- GPU runs of a longer vector, 63-65
- GPU sums of arbitrarily long vectors, 65-69
- GPU vector sums using, 61-63
- hardware limit to number of, 63
- histogram kernel using global memory atomics, 179-181
- incorrect dot product optimization and divergence, 81-82
- multiple CPUs, 225-229
- overview of, 59-60
- ray tracing on GPU and, 102-104
- read-modify-write operations, 168-170
- shared memory and, see shared memory summary review, 94
- synchronizing, 219

### threadPerBlock
- Bloom filter, 76-77
- dot product computation, 79-87
- three-dimensional blocks, GPU sums of a longer vector, 63
- three-dimensional graphics, history of GPUs, 4-5
- three-dimensional scenes, ray tracing producing 2-D image of, 97

### tid variable
- blockIdx.x variable assigning value of, 44
- checking that it is less than N, 45-46
- dot product computation, 77-78
- parallelizing code on multiple CPUs, 40

### time, GPU ripple using threads, 72-74

### timer, event, see cudaEventElapsedTime()

### Toolkit, CUDA, 16-18

### two-dimensional blocks
- arrangement of blocks and threads, 64
- GPU Julia Set, 51
- GPU ripple using threads, 70
- grid_dim variable as, 63
- one-dimensional indexing versus, 44

### two-dimensional display accelerators, development of GPUs, 4

### two-dimensional texture memory
- defined, 116
- heat transfer simulation, 117-118
- overview of, 131-137

## U

### ultrafast imaging, CUDA applications for, 9

### unified shader pipeline, CUDA Architecture, 7

### university, CUDA, 245

## V

### values
- CPU hash table implementation, 261-267
- GPU hash table implementation, 269-275
- hash table concepts, 259-260

### vector dot products, see dot product computation

### verify_table(), GPU, 39-41
- CPU, 41-46
- GPU sums of arbitrarily long vectors, 65-69
- GPU sums of longer vector, 63-65
- GPU sums using threads, 61-63
- overview of, 38-39, 60-61

### verify_table(), GPU hash table, 270

### Visual Profiler, NVIDIA, 243-244

### Visual Studio C Compiler, 18-19

## W

### warps, reading constant memory with, 106-107

### while () loop
- GPU vector sums, 60
- GPU lock function, 253

### work scheduling, GPU, 205-208

## Z

### zero-copy memory
- allocating/using, 214-222
- defined, 214
- performance, 222-223
