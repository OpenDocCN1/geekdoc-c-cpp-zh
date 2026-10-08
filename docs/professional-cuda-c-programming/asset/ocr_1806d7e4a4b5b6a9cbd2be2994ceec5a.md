# LISTING 10-1 (continued)

```
CFLAGS      += -std=c39
INCLUDES    += # specify include path for host code

GPU_CARD     := -arch=sm_35 # specify your device compute capability
NVCC_FLAGS   += -O3 -dc # separate compilation
NVCC_FLAGS   += -xcompiler -fopennm
CUDA_LINK_FLAGS := -dlink # device linker option

EXEC         := test # test your executable name
CUDA_LINK_OBJ := cuLink.o

all: $(EXEC)
	$(OBJS) $(CUDA_OBJS)
	$(NVCC) $(GPU_CARD) $(CUDA_LINK_FLAGS) -o $(CUDA_LINK_OBJ) $(CUDA_OBJS)
	$(LD) -o $@ $(OBJS) $(CUDA_OBJS) $(CUDA_LINK_OBJ) $(CUDA_LIB)

%.o: %.c
	$(CC) -o $@ -c $(CFLAGS) $(INCLUDES) <

%.cu: %.cu
	$(NVCC) $(GPU_CARD) $(NVCC_FLAGS) -o $@ -c < $(CUDA_INC)

clean:
	rm -f $(OBJS) $(EXEC) *.o aout

install:
```

# Integrating CUDA Files into a C Project

CUDA provides two sets of runtime++ API interfaces:

+   - An interface with C++ conventions
- An interface with C conventions

When porting C to CUDA, you might need to prepare device memory and data from C functions by calling CUDA runtime functions. For example, it might be necessary to call cudaMalloc from a .c file. To call CUDA runtime functions from C code, you need to include the CUDA runtime header file in your host code, as:

```
#include <cuda_runtime_api.h>
```

You can organize your CUDA kernel functions using separate files like you would with C-based projects. You must then create kernel wrapper functions in the device source files that can be called like a normal C function, but perform a CUDA kernel launch. because the host functions that are declared in device source files default to C++ conventions, you will also need to use the following declaration to resolve mangled references:

```
extern "C" void wrapper_kernel_launch(...) {

}
```