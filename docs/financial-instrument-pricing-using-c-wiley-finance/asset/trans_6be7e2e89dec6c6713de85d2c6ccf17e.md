
我们分别在大小为 500、1000 和 2000 的方阵上测试了这些选项（数值单位为秒）：

```
Elapsed time, Raw creation: 0.0110011
Elapsed time, Raw sequential multiply: 0.629063
Elapsed time, Raw parallel multiply PPL: 0.487049
Elapsed time, Raw parallel multiply OpenMP: 0.79708
Elapsed time, Nested creation: 0.0030003
Elapsed time, Nested sequential multiplication: 0.390039
Elapsed time, Nested parallel multiplication PPL: 0.876088
Elapsed time, Nested parallel multiplication OpenMP: 0.648065
Elapsed time, Boost creation: 0.0010001
Elapsed time, Boost sequential multiplication: 0.20302
Elapsed time, Boost parallel multiplication PPL: 1.43914
Elapsed time, Boost parallel multiplication OMP: 0.546055
Elapsed time, Duffy creation: 0.0040004
Elapsed time, Duffy sequential multiplication: 2.11721
Elapsed time, Duffy parallel multiplication OMP: 1.89219
Elapsed time, Raw creation: 0.0360036
Elapsed time, Raw sequential multiply: 15.4175
Elapsed time, Raw parallel multiply PPL: 4.64546
Elapsed time, Raw parallel multiply OpenMP: 4.88649
Elapsed time, Nested creation: 0.0070007
Elapsed time, Nested sequential multiplication: 18.1538
Elapsed time, Nested parallel multiplication PPL: 5.58186
Elapsed time, Nested parallel multiplication OpenMP: 5.45755
Elapsed time, Boost creation: 0
Elapsed time, Boost sequential multiplication: 13.0693
Elapsed time, Boost parallel multiplication PPL: 12.5833
Elapsed time, Boost parallel multiplication OMP: 5.09251
Elapsed time, Duffy creation: 0.0210021
Elapsed time, Duffy sequential multiplication: 34.8985
Elapsed time, Duffy parallel multiplication PPL: 0
Elapsed time, Duffy parallel multiplication OMP: 21.8812
Elapsed time, Raw creation: 0.169017
Elapsed time, Raw sequential multiply: 96.8327
Elapsed time, Raw parallel multiply PPL: 47.2557
Elapsed time, Raw parallel multiply OpenMP: 43.8634
Elapsed time, Nested creation: 0.0890089
Elapsed time, Nested sequential multiplication: 107.685
Elapsed time, Nested parallel multiplication PPL: 57.9658
Elapsed time, Nested parallel multiplication OpenMP: 44.6464
Elapsed time, Boost creation: 0
Elapsed time, Boost sequential multiplication: 143.671
Elapsed time, Boost parallel multiplication PPL: 106.551
Elapsed time, Boost parallel multiplication OMP: 46.0605
Elapsed time, Duffy creation: 0.0900009
Elapsed time, Duffy sequential multiplication: 221.928
Elapsed time, Duffy parallel multiplication OMP: 156.694
```

我们在具有超线程技术的双核处理器上运行了这段代码。我们可以比较和对比不同的输出结果。我们特别可以看到，图 10.1 中类结构的复杂性与其他解决方案相比会对性能产生负面影响。

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_313_0.png)

图 10.1 最后，Duffy（2004B）中的矩阵类接口与 PPL 的接口不兼容，因此没有包含该案例的结果。我们在此说明，我们不再支持 Duffy（2004B）中的矩阵类。

我们将在后续章节中再次讨论性能测量、多线程和多任务。

## 10.4.6 Boost Chrono 库

该库包含与 `<chrono>` 相同的功能，此外还提供了一些在 C++ 中未出现的时钟。这些时钟是操作系统时间 API 的轻量封装，因此可以提取进程所消耗的墙上时钟时间、用户 CPU 时间和系统 CPU 时间：

- `process_real_cpu_clock`：捕获当前进程消耗的墙上时钟 CPU 时间。
- `process_user_cpu_clock`：捕获当前进程消耗的用户 CPU 时间。
- `process_system_cpu_clock`：捕获当前进程消耗的系统 CPU 时间。
- 一个与元组类似的类 `process_cpu_clock`，可同时捕获真实、用户 CPU 和系统 CPU 的进程时间。
- 一个 `thread_clock` 时钟，给出当前线程消耗的时间（在平台支持的情况下）。

我们在本书中不讨论这些主题，但你在某些情况下可能会用到它们。我们建议你查阅 Boost 在线文档。

## 10.5 Boost 日期和时间

现在我们介绍支持日期和时间实体的 Boost 库。可以毫不夸张地说，在多种调度、管理信息和日历驱动的应用中，能够访问对*时间实体*进行建模的数据结构和 C++ 类是非常重要的。为此，*Boost 日期时间*库为许多用例提供了广泛支持，例如：

- 基于格里高利历、POSIX 和本地时间体系创建日期和时间。
- 日期迭代器；例如，遍历一周中的天数。
- 日期生成器和算法。
- 本地时间和 UTC（*协调世界时*）支持。
- 日期和时间的输入/输出及序列化。

本书所采用的方法是讨论该库的主要特性，并给出一些“101”示例。然后，我们继续研究几个使用日期和时间的扩展示例及应用。例如，其中一个项目是将用于计算金融应用的遗留代码迁移并扩展到当前库（参见 Duffy, 2004B）。

本章采用实践方法，我们讨论大量示例来展示 *Boost 日期时间*库的实用性。这是一个庞大的库。

### 10.5.1 概念与功能概述

日期和时间抽象在许多类型的应用中具有根本性的重要性。特别是，包含*时间逻辑*的系统数量众多。我们现在不再自行定义处理日期和时间的库与函数，而是使用 *Boost 日期时间*库，并对其进行扩展以满足特定应用领域的需求。为此，我们讨论该库中最重要的类和功能。我们可以将时间视为一维直线或连续体。

有三种基本的*时间类型*：

- *时间点*：这是时间连续体中某个位置的说明符。
- *时间长度*：这是不依附于时间连续体中任何点的一段时间。它是一个具有大小的“浮动”量。
- *时间间隔（时间段）*：这是依附于时间连续体中特定点的一段时间。

与这些概念中的每一个相对应的是一种所谓的*分辨率*，它被定义为可表示的最小持续时间。我们将*时间系统*定义为一组时间类型，以及用于标记和计算这些时间类型的规则与操作。*日历系统*是一种分辨率为一天的时间系统。在本章中，我们重点讨论*格里高利历系统*，因为它是最广泛使用的系统。我们还讨论用于民用时间应用的 UTC 日历系统。*本地时间系统*基于 UTC，并根据地球自转进行调整，使各地的白昼时间大致相似。最后，*时钟设备*是一种与硬件绑定、在时间系统中提供当前日期或时间的软件组件。

### 10.5.2 格里高利时间

Boost 对格里高利历系统的实现包含以下类型：

- `date`：这是处理日期时的主要接口。
- `date_duration`：这是一个天数计数类，我们在使用格里高利历日期进行计算时使用它。
- `date_period`：这是一个表示两个日期之间范围或间隔的类。

此外，该库支持以不同方式对日期周期进行迭代。它还有许多用于生成日期和日期日程的函数。

为了使用该库，我们建议你在代码中使用以下命名空间并包含以下文件：

```
using namespace boost::gregorian;

#include <boost/date_time/gregorian/gregorian.hpp>      // Types and I/O.
#include <boost/date_time/gregorian/gregorian_types.hpp> // Types only.
```

我们现在详细讨论一下格里高利历类型。

### 10.5.3 日期

date 类具有以下功能：

- 从日期组成部分（日、月和年）、字符串以及系统时钟创建日期。
- 日期访问器，例如检索日期组成部分；对日期的查询。
- 将日期转换为字符串。
- 运算符，例如将持续时间添加到日期以生成另一个日期。

我们首先考虑 date 构造函数。我们注意到，默认构造函数会生成一个无效日期。如果我们希望基于当前日期创建日期，应调用使用硬件时钟的构造函数。我们还可以基于格里高利历的年、月、日创建日期。最后，在某些情况下，创建具有“特殊”值的日期可能会很有用，例如：

- 负无穷大和正无穷大。
- 最大和最小日期。

我们现在给出一些示例，展示如何创建 date 的实例：

```
// Some basic constructors.
try
{
    date d1; Print(d1);      // Produces not_a_date_time.
}
catch (bad_year& e)
{
    cout << e.what() << endl;   // Year not valid range [1400, 10000].
}
```
