

```cpp
static TCHAR* LockName(void);
private:
    unsigned uID;
    double dBalance;
    TCHAR szLock[16];
};
```

```cpp
TCHAR* CBankAccount::LockName(void)
{
    static int iCount = 0;
    static TCHAR szBuffer[16];
    sprintf(szBuffer, _T("_lock_%d"), ++iCount);
    return szBuffer;
}
```

```cpp
void CBankAccount::Transfer(CBankAccount a, CBankAccount b, double dAmount)
{
    CLOCK* outerLock = new CLOCK(a->szLock);
    if (dAmount < a->dBalance)
    {
        CLOCK* innerLock = new CLOCK(b->szLock);
        a->dBalance = dAmount;
        b->dBalance += dAmount;
        delete innerLock;
    }
}
```

前面的代码看起来是正确的，但实际上并不是。它是错误的！假设有这种情况：线程 A 想要从账户 X 转账某些金额到账户 Y，而同时，线程 B 想要从账户 Y 转账某些金额到账户 X。当线程进入 `Transfer` 方法时，它将获取属于账户 X 的锁。现在，假设用于 X 的互斥锁名称为 `lock_X`。假设下一个调度的线程是 B，它获取了账户 Y 的锁，其互斥锁名称为 `lock_Y`。接下来，线程 A 继续并尝试获取属于账户 Y 的锁。它被阻塞，因为 `lock_Y` 被线程 B 持有并属于账户 Y。现在，线程 B 继续并尝试获取 `lock_X`，而该锁被之前挂起的的线程 A 持有。

# 理解并发代码设计

通过下图所示：

| T | 线程 A (从 X 转到 Y) | 线程 B (从 Y 转到 X) |
|---|---|---|
| 0 | Clock* outerLock = new Clock(a->LockName()); // 线程 A 获取账户 X 的 lock_1 | Clock* outerLock = new Clock(a->LockName()); // 线程 B 获取账户 Y 的 lock_2 |
| 1 | | if (dAmount < a->dBalance) |
| 2 | | |
| 4 | Clock* outerLock = new Clock(b->LockName()); // 线程 A尝试获取账户 Y 的 lock_2 并挂起 | Clock* outerLock = new Clock(b->LockName()); // 线程 B 尝试获取账户 X 的 lock_3 并挂起 |
| 5 | // 等待 等永远 || 挂起 // 等待 等永远 || |
| 7 | | |

再次，第一列（**T**）是执行语句的时间。下一列是**线程 A** 的代码语句。接着是**线程 B** 的代码语句。图中所示的情况可能非常罕见，但当我们设计并行代码时，必须时刻意识到这些情况。

# 理解代码设计中的并行性

我们已经正确提到，对于程序员来说，最困难的工作不是编写代码——而是正确地设计应用程序。当你遵循这些步骤，在创建一个良好且稳定的设计后，你只剩下最后一步：按照创建的设计逐步编写代码。我们接下来的示例将以逐步渐进的方式教你如何从零开始构建应用程序，同时考虑如何添加并行性。

我们将创建一个计算 Schwefel 函数的程序。通常，对于 Schwefel 函数的计算以及概率和统计对结果产生显著影响的简单函数，会遗传算法。这是因为此类算法会生成具有其特征的大量基因组群体，并比较它们的得分（结果）。为了示例的简单性，我们将创建自己的类 `CSchwefel`，它将满足我们的需求。

Schwefel 函数如下：

f(x) = \sum_{i=1}^{n} \left( \sum_{j=1}^{i} x_j \right)^2, -65.536 \leq x_i \leq 65.536

# 准备工作

确保 Visual Studio 已经运行。

# 如何实现

现在，让我们创建程序并解释其结构。执行以下步骤：

1. 创建一个名为 `ConcurrentDesign` 的新 C++ 控制应用程序。
2. 打开解决方案并打开 `stdafx.h` 文件，将以下代码粘贴到其中：
```cpp
#pragma once

#include "targetver.h"

#include <stdio.h>
#include <char.h>
#include <Windows.h>
#include <cfloat.h>
#include <time.h>
#include <omp.h>

#include "Schwefel.h"
```
3. 打开解决方案并右键点击头文件。添加一个名为 `Schwefel` 的新头文件。打开 `Schwefel.h`。将以下代码粘贴到其中：
```cpp
#ifndef __SCHWEFEL__
#define __SCHWEFEL__
#include "stdafx.h"

SYSTEMTIME operator - (const SYSTEMTIME& stFirst, const SYSTEMTIME& stSecond);

class CSchwefel;
```
（注：由于原始文本存在大量重复、乱码和交织的代码，已根据标准的 C++ 模式和提供的片段，在下方重建了类结构。）

