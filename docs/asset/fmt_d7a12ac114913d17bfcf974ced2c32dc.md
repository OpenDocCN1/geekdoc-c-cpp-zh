
```cpp
void Calculator::Compute(char op) // 执行计算
{
  Boolean result;
  int operand1, operand2;
  result = GetTwoOperands(operand1, operand2); // 弹出 2 个操作数
  if (result == True) // 如果成功，执行计算
    // 并将结果推入栈中

    switch (op) {
      case '+': S.Push(operand2+operand1);
        break;
      case '-': S.Push(operand2-operand1);
        break;
      case '*': S.Push(operand2*operand1);
        break;
      case '/': if (operand1 == 0) // 检查除数是否为 0
        {
          cerr << "Divide by 0!" << endl;
          S.ClearStack();
          // 如果除数为 0，则清空栈
        } else
          S.Push(operand2/operand1);
          break;
      case '^': S.Push(pow(operand2,operand1));
        break;
    }
    cout << S.Peek() << ' '; // 输出计算结果
  } else
    S.ClearStack();
}

Calculator::Calculator(void) // 构造函数
{}

void Calculator::Run(void) // 读取并处理后缀符号表达式
{
  char c[20];
  while(cin >> c, *c != 'q') // 读取以 'q' 结尾的表达式
switch(*c)
{
    case 'c':
        S.ClearStack();
        // 当出现 'c' 时，清空操作数栈
        break;
    case '-':
        // 判断 '-' 是负号还是减法运算符
        if (strlen(c)>1)
            // 如果字符串长度大于 1
            // 1, '-' 是负号
            Enter(atoi(c));
            // 将字符串转换为整数
            // 并推入栈中
        else
            Compute(*c);// 如果 '-' 是减法
            // 符号，执行计算
        break;
    case '+':
    case '*':
    case '/':
    case '^':
        Compute(*c); // 执行计算
        break;
    default:
        // 如果字符串是操作数，
         将其转换为整数并将其
        // 推入栈
        Enter(atoi(c));
        break;
}

void Calculator::Clear(void) // 清空操作数栈
{
    S.ClearStack();
}

// 9_9.cpp
#include "9_9.h"
int main()
{
    Calculator CALC;
    CALC.Run();
}
```

# 9.2 线性集合 — 385

运行结果：

```
10 20 + =30
15 / =5
8 * =16

 + ^ =256
Missing operand!
10 q
```

# 9.2.5 队列 (Queues)

与栈不同，队列也是具有受限访问模式的线性集合。我们只能在一侧（头部）添加元素，只能在另一侧（尾部）移除元素。队列既可以用数组实现，也可以用链列表实现。队列状态定义与栈相似。队列应该提供头指针和尾指针作为数据成员，并且还需要提供这些操作的接口：

- 初始化
- 入队 (Enqueue)
- 清空 (Clear)
- 访问头部

图17 显示了静态数组中的简单实现。我们可以看到在删除元素时，所有元素都会向头部移动，这非常低效。设计队列的一种方法是将其设计为环形。该思路如图18 所示。队列维护两个分别指向头部和尾部的指针。队列在入队和出队元素时更改这些指针。关键部分是使用模运算来环绕队列，确保指针在跨越边界时重置为零。队列还需要统计元素数量。这种方法是队列的实现。

#endif //QUEUE_CLASS

通过链表实现队列也留作了一个练习题。

## 9.3 在线性集合中组织数据

在本节中，我们将讨论如何在线性集合中组织数据，介绍如何对集合进行排序以及在集合中查找特定元素。

### 9.3.1 插入排序

插入排序的基本思想是将未排序元素逐个插入到正确的位置（已排序的子集合中），直到集合完全排序。例如，如果我们需要对一个包含 `n` 个元素的数组 `a` 进行进行排序，我们可以将 `a[0]` 视为已排序的子集合，将 `a[1..n-1]` 视为待排序的子集合。该过程如图 9.19 所示。该算法有若干变体，使用不同的方法寻找插入元素的位置。这里只介绍最简单的一种：直接插入排序。

示例 9.11：直接插入排序的实现。

```cpp
//9_11.h
#ifndef ARRAY_BASED_SORTING_FUNCTIONS
#define ARRAY_BASED_SORTING_FUNCTIONS
```

```cpp
//Use direct insertion sort to sort the n elements in array A
template <class T>
```

![](img/5618306d085ac1bac8275d6c4c5bbf2a_406_0.png)

图 9.19：插入排序的步骤。

```cpp
void InsertionSort(T A[], int n)
{
    int i, j;
    T temp;

    // 将索引为 1-n-1 的元素插入到排序序列
    // 中恰当的位置
    for (i = 1; i < n; i++)
    {
        // 从 A[i-1] 到 A[0] 扫描元素，找到插入 A[i]
        // 的合适位置
        j = i;
        temp = A[i];
        while (j > 0 && temp < A[j-1])
            // 逐个比较直到 temp=A[j-1]，j 就是
            // 插入的位置
            // 如果 j==0，0 就是合适的位置
            A[j] = A[j-1]; // 将元素逐个后移，使得
            // 在找到合适位置时可以立即插入
            j--;
        }
        // 找到位置后立即插入
        A[j] = temp;
    }
}
#endif
```

### 9.3.2 选择排序

选择排序的基本思想是从待排序的子集合中选择最小元素，并将其放在已排序子集合的末尾。它有几种基于寻找最小元素不同方法的变体。最简单的一种是遍历集合，即所谓的直接选择排序，如图 9.20 所示。

示例 9.12：直接选择排序的实现。

```cpp
//9_12.h
#ifndef ARRAY_BASED_SORTING_FUNCTIONS
#define ARRAY_BASED_SORTING_FUNCTIONS
```

初始状态：

[5 4 10 20 12 3]

1. 选取 3

[5 4 10 20 12 3]

2. 选取 4

[4 10 20 12 5]

3. 选取 5

3 4 [10 20 12 5]

4. 选取 10

3 4 5 [20 12 10]

5. 选取 12

3 4 5 10 [12 20]

排序后：

3 4 5 10 12 [20]

图 9.20：直接选择排序的步骤。

```cpp
// 工具函数：交换 x 和 y 的值
template <class T>
void Swap (T &x, T &y)
{
  T temp;
  temp = x;
  x = y;
  y = temp;
}
```

```cpp
// 使用选择排序对数组 A 中的 n 个元素排序
template <class T>
void SelectionSort(T A[], int n)
{
  int startIndex;             // 选择最小元素的
  int i, j;                   //每一轮
  for (i = 0; i < n-1; i++)
  {
    startIndex = i;         // 最小元素的初始
    // 索引设置为 i
    for (j = i+1; j < n; j++) {
        // 在 A[i]..A[n-1] 之间比较
        // 获取最小的一个
        if (A[j] < A[startIndex]) { // startIndex 存储
            // 最小元素的索引
            startIndex = j;
        }
    }
    Swap(A[i], A[startIndex]); // 交换元素
  }
```

### 9.3.3 交换排序

交换排序的思想是将集合中的元素成对比较，如果它们无序则进行交换。冒泡排序是一个很好的例子。以下是针对 `n` 个元素的数组的冒泡排序算法：

- 检查前两个元素，如果无序则交换它们。对第二个和第三个执行类似的操作，直到达到最后一个。这整个过程称为冒泡排序的第一阶段。执行后，最大值位于第 `n` 个位置。
- 对 `n-1` 个元素重复第一步。执行后，这 `n-1` 个元素的最大值位于第 `n-1` 位置。
- 重复第二步，直到没有元素发生交换（冒泡排序的一个阶段）。对于 `n` 个元素的集合，冒泡排序需要 `n-1` 个阶段。

图 9.21 显示了冒泡排序的步骤。

示例 9.13：冒泡排序的实现。

```cpp
//13.h
#ifndef ARRAY_BASED_SORTING_FUNCTIONS
#define ARRAY_BASED_SORTING_FUNCTIONS

// 工具函数：交换 x 和 y 的值
template <class T>
void Swap (T &x, T &y) {
    T temp;
    temp = x;
    x = y;
    y = temp;
}
```

```cpp
// 使用冒泡排序对数组 A 中的 n 个元素排序
template <class T>
void BubbleSort(T A[], int n)
{
    int i, j;
    int lastExchangeIndex; // 记录最后一次交换
                             // 元素的索引
    // i 是下一轮
                             // 将发生的索引
    i = n - 1;
    while (i > 0) { // 继续排序，直到最后一轮
                    // 没有发生交换或已完成 n-1 轮
        lastExchangeIndex = 0; // 在每一轮
                               // 之前将交换索引置 0
        for (j = 0; j < i; j++) { // 在 A[0]..A[i] 之间
                                   // 比较并交换
            if (A[j+1] < A[j]) { // 如果元素 A[j+1] < A[j]，交换它们
                Swap(A[j], A[j+1]);
                lastExchangeIndex = j; // 记录较小的
                                      // 索引
            }
        }
        i = lastExchangeIndex; // 将 i 设置为最后
                               // 交换的索引
    }
}
#endif
```

| 8 | 5 | 2 | 2 | 2 |

|---|---|---|---|---|

| 5 | 2 | 4 | 3 | 3 |

| 2 | 4 | 3 | 4 | 4 |

| 4 | 3 | 5 | 5 | 5 |

| 3 | 8 | 8 | 8 | 8 |

图 9.21：冒泡排序的步骤。

### 9.3.4 顺序查找

顺序查找是一种基础搜索方法。它遍历数组，并将每个元素与目标元素进行比较，直到找到匹配项。如果没有匹配目标元素的元素，则搜索失败。

示例 9.14：顺序查找。

```cpp
//9_14.h
#ifndef SEARCH_METHODS
#define SEARCH_METHODS

// 使用顺序查找在数组列表中查找值为 key 的元素
// 如果找到，则返回元素的索引，否则返回 -1
template <class T>
int SeqSearch(T list[], int n, T key)
{
    for(int i=0; i < n; i++)
        if (list[i] == key)
            return i;
    return -1;
}

#endif //SEARCH_METHODS
```

### 9.3.5 二分查找

如果我们对排序后的集合进行搜索，就可以使用二分查找。二分查找的思想是：通过比较将序列分为两个大小相等的部分，其中只有一个部分可能包含目标元素。图 9.22 显示了二分查找的步骤。

示例 9.15：二分查找。

```cpp
//9_15.h
#ifndef SEARCH_METHODS
#define SEARCH_METHODS
```

| 5 | 13 | 19 | 21 | 37 | 56 | 64 | 75 | 80 | 88 | 92 |

|---|---|---|---|---|---|---|---|---|---|

low=0

high=10

mid=(low+high)/2=5 21<list[mid]

| 5 | 13 | 19 | 21 | 37 |

low=0

high=mid-1=4

mid=(low+high)/2=2 21>list[mid]

| 21 | 37 |

low=mid+1

high

mid=(low+high)/2=3 21=list[mid] 找到了元素 21，索引为 3

图 9.22：二分查找的步骤。

```cpp
// 使用二分查找在升序数组列表中查找值为 key 的元素
template<class T>
int BinSearch(T list[], int n, T key)
{
    int mid, low, high;
    T midvalue;
    low=0;
    high=n-1;
    while (low <= high) { // low <= high 表示数组
                         // 尚未遍历完
        mid=(low+high)/2; // 获取中间
                         // 元素的索引
        midvalue = list[mid]; // 获取元素的值
        if (key == midvalue) { // 如果找到，返回索引
            return mid;
        } else if (key < midvalue) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return -1;
}
```

# 9 集合及其组织

```cpp
else if (key < midvalue)
    high = mid-1;      //如果 key < midvalue，则将搜索范围
                               //设置为前半部分
else
    low = mid+1;       //否则，将搜索范围设置为
                               //后半部分
}
return -1;               //如果没有找到则返回-1

#endif                                 //SEARCH_METHODS
```

# 9.4 应用 – 改进小型的人资源管理程序

我们在第 8 章中演示了如何使用多态。现在我们使用动态数组来实现相同的功能。

**示例 9.16:** 改进人力资源管理程序。

程序中有四个文件：第 8 章中的 `employee.h` 和 `employee.cpp`，本章中的 `9_3.h`，以及一个从 `8.cpp` 派生经过略微修改的 `9_16.cpp`。
