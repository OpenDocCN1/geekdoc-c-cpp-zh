# 8.1. Graphics coprocessor architecture

100. The first task is to find out exactly which graphics processor is available and what its capability is.

On a single computer system, several CUDA-enabled graphics processors may be available via the PCIe bus. With the following two lines, we can find out the number of CUDA-enabled graphics processors available:

```
int count;
cudaGetDeviceCount(&count);
```

CUDA programs look much like C programs. However, certain parts of the program run on the host, which is typically an x86 processor running either Linux or Windows, and other parts run on the device, which is the graphics processor. cudaGetDeviceCount() function on some other means, it finds out the number of devices of capability 10 or higher. A program using this function can be compiled using nvcc, which is NVIDIA's compiler driver. The compiler driver nvcc is a sophisticated wrapper around gcc, and in this case all that nvcc has to do is link the library in cudaGetDeviceCount() is defined. No special option to nvcc is necessary. This and other similar functions are declared in cuda_runtime.h.

Once we know the device, we can find out each device.

```
cudaDeviceProp prop(&prop, i);
```

HereDeviceProp is a structure type with fields corresponding to various properties of the device. The structure is defined in the cuda_runtime.h header file. We do not have to include the header file explicitly in our C++ program because nvcc will include the right header automatically. The cudaDeviceProperties() function may map to the operating system to find out the properties of device i, where it is the second argument in the function call. Alternatively, the information about device properties may be left in some location during the installation of the nvcc driver. In either case, no code is generated that must run on the graphics device.

The prop variable, which is set up in this way, has information about the graphics device. The line

> ¹(CUDA C Programming Guide, (CUDA Compiler Driver NVCC, August, 2014), and (CUDA Runtime API, August, 2014). Functions like cudaGetDeviceCount() are documented in the last of these sources.