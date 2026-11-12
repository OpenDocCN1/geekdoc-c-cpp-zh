
花费在执行线程指令上的时间。前一个数值大于后一个数值，因为线程是时间片轮转的。

## B.12. 原子函数

原子函数对全局内存或共享内存中驻留的一个32位或64位字执行读-修改-写原子操作。例如，`atomicAdd()`读取全局内存或共享内存中某个地址处的一个字，向其添加一个数字，并将结果写回同一地址。该操作是原子的，意味着它保证在不受其他线程干扰的情况下执行。换句话说，在操作完成之前，没有其他线程可以访问此地址。原子函数不充当内存栅栏，也不对内存操作隐含同步或顺序约束（有关内存栅栏的更多详细信息，请参阅内存栅栏函数）。原子函数只能在设备函数中使用。

在计算能力低于6.x的GPU架构上，从GPU执行的原子操作仅相对于该GPU是原子的。如果GPU尝试对对等GPU的内存执行原子操作，该操作表现为对对等GPU的常规读取后跟写入，并且这两个操作不会作为单个原子操作完成。同样，从GPU到CPU内存的原子操作相对于CPU发起的原子操作也不是原子的。

计算能力6.x引入了一种新的原子类型，允许开发人员扩大或缩小原子操作的范围。例如，`atomicAdd_system`保证该指令相对于系统中的其他CPU和GPU是原子的。`atomicAdd_block`意味着该指令仅相对于同一线程块中其他线程的原子操作是原子的。在以下示例中，CPU和GPU都可以原子地更新地址 `addr` 处的整数值：

```
__global__ void mykernel(int *addr) {
    atomicAdd_system(addr, 10); // only available on devices with compute capability 6.x
}

void foo() {
    int *addr;
    cudaMallocManaged(&addr, 4);
    *addr = 0;

    mykernel<<<..., >>>(addr);
    __sync_fetch_and_add(addr, 10); // CPU atomic operation
}
```

> 系统范围的原子操作不受计算能力低于7.2的Tegra设备支持。

新的作用域版本的原子操作仅适用于计算能力6.x及更高版本下列出的所有原子操作。

请注意，任何原子操作都可以基于 **atomicCAS()**（比较并交换）实现。例如，双精度浮点数的 **atomicAdd()** 在计算能力低于6.0的设备上不可用，但可以按如下方式实现：

```
#if __CUDA_ARCH__ < 600
__device__ double atomicAdd(double* address, double val)
{
    unsigned long long int* address_as_ull =
                              (unsigned long long int*)address;
    unsigned long long int old = *address_as_ull, assumed;
    do {
        assumed = old;
        old = atomicCAS(address_as_ull, assumed,
                        __double_as_longlong(val +
                        __longlong_as_double(assumed)));
    } // Note: uses integer comparison to avoid hang in case of NaN (since NaN != NaN)
    while (assumed != old);
    return __longlong_as_double(old);
}
#endif
```

### B.12.1. 算术函数

### B.12.1.1. atomicAdd()

```
int atomicAdd(int* address, int val);
unsigned int atomicAdd(unsigned int* address,
                       unsigned int val);
unsigned long long int atomicAdd(unsigned long long int* address,
                                 unsigned long long int val);
float atomicAdd(float* address, float val);
double atomicAdd(double* address, double val);
__half2 atomicAdd(__half2* address, __half2 val);
__half atomicAdd(__half* address, __half val);
```

读取全局内存或共享内存中地址 **address** 处的16位、32位或64位字 old，计算（*old* + *val*），并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 old。

**atomicAdd()** 的32位浮点版本仅受计算能力2.x及更高版本设备支持。

**atomicAdd()** 的64位浮点版本仅受计算能力6.x及更高版本设备支持。

**atomicAdd()** 的32位 __half2 浮点版本仅受计算能力6.x及更高版本设备支持。__half2 加法操作的原子性分别针对两个 __half 元素保证；整个 __half2 不保证作为单个32位访问是原子的。

**atomicAdd()** 的16位 __half 浮点版本仅受计算能力7.x及更高版本设备支持。

### B.12.1.2. atomicSub()

```
int atomicSub(int* address, int val);
unsigned int atomicSub(unsigned int* address,
                       unsigned int val);
```

读取全局内存或共享内存中地址 **address** 处的32位字 **old**，计算（**old** - **val**），并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。

### B.12.1.3. atomicExch()

```
int atomicExch(int* address, int val);
unsigned int atomicExch(unsigned int* address,
                        unsigned int val);
unsigned long long int atomicExch(unsigned long long int* address,
                                  unsigned long long int val);
float atomicExch(float* address, float val);
```

读取全局内存或共享内存中地址 **address** 处的32位或64位字 **old**，并将 **val** 存回同一地址的内存中。这两个操作在一个原子事务中执行。该函数返回 **old**。

### B.12.1.4. atomicMin()

```
int atomicMin(int* address, int val);
unsigned int atomicMin(unsigned int* address,
                       unsigned int val);
unsigned long long int atomicMin(unsigned long long int* address,
                                 unsigned long long int val);
```

读取全局内存或共享内存中地址 **address** 处的32位或64位字 **old**，计算 **old** 和 **val** 的最小值，并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。

**atomicMin()** 的64位版本仅受计算能力3.5及更高版本设备支持。

### B.12.1.5. atomicMax()

```
int atomicMax(int* address, int val);
unsigned int atomicMax(unsigned int* address,
                       unsigned int val);
unsigned long long int atomicMax(unsigned long long int* address,
                                 unsigned long long int val);
```

读取全局内存或共享内存中地址 **address** 处的32位或64位字 **old**，计算 **old** 和 **val** 的最大值，并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。

**atomicMax()** 的64位版本仅受计算能力3.5及更高版本设备支持。

### B.12.1.6. atomicInc()

```
unsigned int atomicInc(unsigned int* address,
                               unsigned int val);
```

读取全局内存或共享内存中地址 **address** 处的32位字 **old**，计算 ((**old** >= **val**) ? 0 : (**old**+1))，并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。

### B.12.1.7. atomicDec()

```
unsigned int atomicDec(unsigned int* address,
                               unsigned int val);
```

读取全局内存或共享内存中地址 **address** 处的32位字 **old**，计算 (((**old** == 0) || (**old** > **val**)) ? **val** : (**old**-1) )，并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。

### B.12.1.8. atomicCAS()

```
int atomicCAS(int* address, int compare, int val);
unsigned int atomicCAS(unsigned int* address,
                       unsigned int compare,
                       unsigned int val);
unsigned long long int atomicCAS(unsigned long long int* address,
                                 unsigned long long int compare,
                                 unsigned long long int val);
unsigned short int atomicCAS(unsigned short int* address,
                             unsigned short int compare,
                             unsigned short int val);
```

读取全局内存或共享内存中地址 **address** 处的16位、32位或64位字 **old**，计算（**old** == **compare** ? **val** : **old**），并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**（比较并交换）。

### B.12.2. 位运算函数

### B.12.2.1. atomicAnd()

```
int atomicAnd(int* address, int val);
unsigned int atomicAnd(unsigned int* address,
                       unsigned int val);
unsigned long long int atomicAnd(unsigned long long int* address,
                                 unsigned long long int val);
```

读取全局内存或共享内存中地址 **address** 处的32位或64位字 **old**，计算（**old & val**），并将结果存回同一地址的内存中。这三个操作在一个原子事务中执行。该函数返回 **old**。
