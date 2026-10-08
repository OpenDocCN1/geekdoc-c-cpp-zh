
CAS 接受三个输入：一个内存位置、该内存位置的预期值，以及你想要存储在该内存位置的值。它执行以下步骤：

- 1. 读取目标位置，并将其中存储的值与预期值进行比较。
    - a. 如果存储的值等于预期值，则将目标内存位置填充所需的值。
    - b. 如果存储的值不等于预期值，则目标位置不发生变化。
- 2. 无论何种情况下，CAS 操作总是返回它在目标位置找到的存储值。注意，你可以使用返回的值来检查交换是否成功。如果返回的值是预期值，则 CAS 操作可能已经成功。原子性（Atomic）意味着整个 CAS 过程在没有任何其他线程干扰的情况下完成。由于这是一次原子操作，如果 CAS 操作的返回值表示写入成功，那么该更改必须对所有其他线程可见。

现在，这就是 CAS 操作。为了了解更多关于原子操作知识，使用 CUDA 的 `atomicCAS` 设备函数从组中实现一个原子函数对你非常有帮助。例如，你将实现一个 32 位整数加法。相关 `atomicCAS` 变体的签名如下：

```
int atomicCAS(int *address, int compare, int val);
```

这里 `address` 是内存位置，`compare` 是该位置的预期值，`val` 是你希望写入该位置的值。

那么，你如何使用 `atomicCAS` 实现原子加法呢？你需要将加法分解为它的组成部分，并将其定义为 CAS 操作。在实现自定义原子操作时，一种很有用的技术是定义目标的起始状态和结束状态。对于加法，起始状态是将被增加的基值。结束状态是起始状态与增量之和。这个定义直接翻译为 `atomicCAS`：预期值是起始状态，所需的值是结束状态。

要实现自定义原子加法，你将从一个函数签名开始，该函数接收一个要加的位置和一个要加的数值：

```
__device__ myAtomicAdd(int *address, int incr) {
}
```

你可以通过简单读取目标内存位置来计算目标的预期值。所需的值由加上传递给 `myAtomicAdd` 的 `incr` 值定义。使用这些预期值和所需值，可以调用 `atomicCAS` 来实现加法：

```
__device__ myAtomicAdd(int *address, int incr) {
// 为 *address 存储的值创建一个初始假设值。
int expected = *address;
int oldValue = atomicCAS(address, expected, expected + incr);
...
}
```

`myAtomicAdd` 函数已经可以执行原子加法了！但只有当读取到 `expected` 的值在执行 `atomicCAS` 时也是 `address` 处存储的值，该操作才会成功。目标位置被多个线程共享（否则不需要原子操作），另一个线程可能在被读取之后、被 `atomicCAS` 修改之前修改 `address` 处的值。如果发生这种情况，`atomicCAS` 将失败，因为 `address` 的当前值与 `expected` 的值将不一致。

记住，失败是通过与预期值不同的 `atomicCAS` 返回值信号的。利用该信息，`myAtomicAdd` 可以检查失败并在循环中重试比较并交换，直到 `atomicCAS` 成功：

```cpp
int myAtomicAdd(int *address, int incr) {
    // 为 *address 存储的值创建一个初始值。
    int expected = *address;
    int oldValue = atomicCAS(address, expected, expected + incr);

    // 当 expected 不正确时，进行循环。
    while (oldValue != expected) {
        expected = oldValue;
        oldValue = atomicCAS(address, expected, expected + incr);
    }
    return oldValue;
}
```

该函数的前三行与之前相同。如果第一次 `atomicCAS` 失败，`myAtomicAdd` 现在只要 `atomicCAS` 返回的最后一个值与预期值不同，就会继续循环。一旦该操作失败，说明交换已经成功，`myAtomicAdd` 退出循环。否则，预期值被重置为最近读取的值，并进行重试。为了匹配其他 CUDA 原子函数的语义，`myAtomicAdd` 还会通过返回 `atomicCAS` 读取的最新值，来返回在目标位置被替换掉的值。

你可以从 wrox.com 下载、编译并运行 `my-atomic-add.cu` 中的这些代码。编译命令为：

```
$ nvcc -arch=sm_11 my-atomic-add.cu
```

虽然下一节涵盖了 CUDA 原生支持的原子函数，但理解你并不限于这些函数是非常重要的。通过 `atomicCAS`，你可以根据特定应用程序的需求实现范围广得的操作。

## 内置 CUDA 原子函数

CUDA 支持一组原子函数。你可访问的子集取决于你设备的计算能力（compute capability）。

在共享内存中操作 32 位值以及在全局内存中操作 64 位值的支持从计算能力 1.1 开始。在这一级别，你将可以访问管理全局内存中 32 位值的函数。

在共享内存中操作 32 位值以及在全局内存中操作 64 位值的支持从计算能力 1.2 开始。在共享内存中进行 64 位操作的支持从计算能力 2.0 开始。

表 7-6 列出了 CUDA 支持的原子函数对应的操作、相关的 CUDA 设备函数以及支持的类型。

## 表 7-6：内置 CUDA 原子操作

| 操作 | 函数 | 支持的类型 |
| --- | --- | --- |
| 加法 | atomicAdd | int, unsigned, unsigned long int, float |
| 减法 | atomicSub | int, unsigned |
| 无条件交换 | atomicExch | int, unsigned, unsigned long int, float |
| 最小值 | atomicMin | int, unsigned, unsigned long int, unsigned int |
| 最大值 | atomicMax | int, unsigned, unsigned long int, unsigned int |
| 增一 | atomicInc | unsigned int |
| 减一 | atomicDec | unsigned int |
| 比较交换 | atomicCAS | int, unsigned, unsigned long int |
| 与 | atomicAnd | int, unsigned, unsigned long int |
| 或 | atomicOr | int, unsigned, unsigned long int |
| 异或 | atomicXor | int, unsigned, unsigned long int |

## 原子操作的代价

虽然原子函数在某些应用程序中非常有用且必要，但它们可能会带来高昂的性能代价。有几个影响因素：

- 1. 在全局内存或共享内存中执行原子操作时，原子性提供的保证之一是更改将对所有线程立可见。因此，至少原子指令必须直接访问全局或共享内存来读取当前值，而不使用缓存。如果原子指令执行成功，它还必须将所需的值写入全局或共享内存。

- 2. 对共享位置的冲突访问可能需要冲突线程进行一次或多次重试，类似于运行多次 `myAtomicAdd` 的循环。虽然内置原子函数的构建方式是有限的，但对于你实现的任何原子操作，情况确实如此。如果你的应用程序在反复循环的同时增加了 I/O 开销，性能将会下降。

- 3. 当 warp 中的线程必须执行不同的指令时，warp 的执行是串行化的。如果 warp 中的多个线程对内存中的同一位置发出原子操作，由于它们相互冲突，会发生类似的情况。因为只有一个线程的原子操作可以成功，所有其他线程必须重试。如果单个原子指令需要 $\tau$ 个周期，而 warp 中的 $\tau$ 个线程在同一内存位置执行该指令，那么所花费的时间将 $\tau^2$，因为每次连续重试都会成功一次。

