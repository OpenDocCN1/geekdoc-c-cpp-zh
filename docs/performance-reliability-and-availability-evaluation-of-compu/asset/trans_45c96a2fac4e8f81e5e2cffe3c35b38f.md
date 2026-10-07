
## 性能测量

## 355

![](img/2d1450514bb14a0cdf0eb5048614afab_371_0.png)

### 图 23.5 基于软件的间隔定时器。

开销（Overhead）—— 被测系统决定了如何使用间隔定时器来测量事件的持续时间。例如，程序 1 中描述的名为“被测量的代码”的部分即为事件。我们可以将其视为一个方法、过程、指令块或基本块。通过读取软件定时器 `Start_count = read_timer()` 来捕获当前时间。执行此原语函数 `read_timer()` 会读取软件瞬时并将相应的值存储在 `Start_count` 中。执行该原语函数后，感兴趣的事件（被测量的代码）开始执行。在事件执行完成后，再次读取软件定时器，将其当前瞬时存储在 `Stop_count` 中。该事件的通过时间（$T_e$）通过减去 `Stop_count` 中的值来估算。此差值指定了事件执行期间经过的时钟周期数。将此差值乘以一个时钟周期的持续时间即可得到事件持续时间的估算。值得提到，时钟周期被认为是定时器的计时参考。

在程序 2 中，我们有了一个如何在 Python 程序中测量代码段（事件）执行时间的示例。在这个特定示例中，通过应用 Python time 库的 `time.time()` 函数测量了三个函数（三个事件：tri、factorial 和 matrixops）的执行时间。记录时间戳、时间戳差值以及支持 `time.time()` 函数的库用红色代码编写。

在 C 语言中，库 `<sys/time.h>` 中的函数 `gettimeofday` 返回自 1970 年 1 月 1 日 00:00:00 UTC（UNIX 纪元协调世界）以来经过的时间。

## 356 计算系统的性能、可靠性和可用性评估

```algorithm
Algorithm 1 测量程序中一段代码的持续时间
1:
2: Start_count = read_timer();
3:
4: 被测量的代码
5: ...
6: Stop_count = read_timer();
7: Elapsed_time = (stop_count - start_count) × clock_period;
8:
```

该函数以两个独立的 double 变量返回秒和微秒。为了获得包括微秒在内的总时间，我们需要相应地将两者相加。程序 3 所示的代码段展示了如何计算函数的持续时间。在这个特定示例中，测量了 `func()` 的执行时间。红色命令行描述了估算执行时间所需的特定命令。

如果秒数并不重要，我们可以通过计算 `end.tv_sec - begin.tv_sec` 获取经过时间。`gettimeofday()` 的第二个参数用于指定当前时区。由于我们计算的是经过时间，只要对 begin 和 end 使用相同的值，时区就是无关的。因此，我们对两次调用都使用 0。

使用这种方法估算事件持续时间（$T_e$）时，结果测量的值超过了事件本身的持续（见图 23.6）。需要强调的是，访问定时器需要内存读取操作，并可能需要调用操作系统内核。此外，从定时器读取的值被存储为变量，这需要执行内存写入。该过程执行了两次。首先，它在事件开始时执行，产生开销 $T_1 + T_2$，然后在事件结束时再次执行，产生开销 $T_3$。这些操作可能会为事件本身的持续增加显著的时间（开销）。

> overhead = $T_1 + T_2 + T_3$。

如果开销与事件持续时间（$T_e$）处于同一级，开销可能是显著的。如果开销 $\ll T_e$，可以忽略开销。然而，如果开销 $\approx T_e$ 或开销 $> T_e$，这些操作将给事件持续带来巨大的延迟；因此，不适合测量此类数量级的事件。第 23.7 节提供了 Linux 性能计数器基本工具的快速概述。

## 性能测量 357

### 算法 2 测量 Python 程序中函数的持续时间

```python
1: import time
2: import pstats
3: import math
4: #  NumPy 用于矩阵操作
5: import numpy
6: #
7: def trig(a):
     print("Trigonometric Functions,", end="\n*2")
     print("从弧度到角度的转换值为：", end="\n")
     print(math.degrees(a))
     print("pi/6 的值为：", end="\n")
     print(math.sin(a))
     print("pi/6 的余弦值为：", end="\n")
     print(math.cos(a))
     print("pi/6 的正值为：", end="\n")
     print(math.tan(a),\n*2)

def factorial(x):
    # 计算整数阶乘的递归函数
    if x == 1:
        return 1
    else:
        return (x * factorial(x-1))

def matrixops(x,y):
    print("平方根：")
    print(numpy.sqrt(x))
    print("所有之和：")
    print(numpy.sum(y))
    print("所有列之和：")
    print(numpy.sum(y,axis=0))
    print("所有行之和：")
    print(numpy.sum(y,axis=1))
    print("转置：")
    print(y.T)

def main():
    rad = math.pi/6
    num = 50
    # 初始化
    b = numpy.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
    c = numpy.array([[1, 4, 7], [2, 5, 8], [3, 6, 9]])
    # 测量时间
    start = time.time()
    trig(rad)
    end = time.time()
    print("trig 耗时", end-start, "秒")

    start = time.time()
    factorial(num)
    end = time.time()
    print("factorial 耗时", end-start, "秒")

    start = time.time()
    matrixops(b,c)
    end = time.time()
    print("matrixops 耗时", end-start, "秒")

if __name__ == "__main__":
    main()
```
