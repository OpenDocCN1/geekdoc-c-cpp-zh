# Leveraging the NVCC

The NVIDIA CUDA Compiler (NVCC) plays a central role in compiling CUDA code. It processes CUDA C files (.cu) and invokes the host compiler for C/C++ code. To achieve optimal performance, understanding and correctly utilizing NVCC options is essential. Below is an example of compiling a CUDA program with NVCC:

```
nvcc -O3 --gpu-architecture=compute_75 --gpu-code=compute_75,sm_75 example.cu -o example
```

In this command, the -O3 flag is used for aggressive optimizations, while -gpu-architecture and -gpu-code specify the target GPU architecture and code versions, respectively.