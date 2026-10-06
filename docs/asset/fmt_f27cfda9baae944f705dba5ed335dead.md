
class List {

    // 成员声明

```
如何定义 int 的特化版本？将其重写为接受任何类型的模板。假设该类有一个默认构造函数。

## 复习题与练习

### 答

1. 什么是异常点？
2. 什么是异常处理器？
3. 解释 try 块和 catch 块的区别。
4. 如果抛出异常但未被捕获会发生什么？
5. 什么是“栈回溯”？
6. 如果类成员函数抛出异常会发生什么？
7. 如何防止在 new 运算符无法分配内存时程序停止？
8. 为什么为重载函数编写函数模板不方便？
9. 为什么编写使用运算符的函数模板时必须小心？

### 填空

10. 包含 throw 语句的行被称为 ________。
11. ________ 可能直接或间接地导致异常抛出。
12. ________ 处理异常。
13. 在编写函数或类模板时，使用 ________ 来指定通用数据类型。
14. 模板的开头由 ________ 标记。
15. 定义类模板对象时，必须指定要传递的 ________。
16. ________ 用于特定类型。

### 算法工作

17. 编写一个函数在数值数组中搜索指定的值。如果该值在数组中，函数应返回包含该元素的下标。如果没有找到，函数应抛出异常。
18. 编写一个动态分配内存块并返回该块指针的函数。该函数接受一个整数参数作为要分配的内存量。如果 new 运算符无法分配内存，函数应返回空指针。
19. 将你在第 17 题中编写的函数变为模板。
20. 编写一个模板，显示任意类型数组的内容。

### 判断对错

21. F 程序中只能有一个 catch 块。
22. T 如果抛出异常但未被捕获，程序将忽略该错误。

## 复习题与练习

- 23. T 可以通过将其存储在异常类的成员中随异常传递数据。
- 24. T 一旦抛出异常，程序就不可能跳回抛出点。
- 25. T 在函数模板中定义的所有类型参数必须在函数参数列表中至少出现一次。
- 26. T 编译器一遇到模板，就会在内存中为该函数模板创建一个一个实例。
- 27. F 传递给函数模板的类对象必须重载模板中对类对象所使用的运算符。
- 28. T 一个模板中只能使用一种泛型类型。
- 29. T 在函数模板定义中，没有必要使用模板前缀中声明的每个类型参数。
- 30. F 可以重载两个函数模板。
- 31. F 可以重载一个函数模板和一个普通（非模板）函数。
- 32. T 类模板不能派生自另一个类模板。
- 33. F 类模板不能作为基类使用。
- 34. F 特化模板与特定的数据类型工作。

# 找错

以下每个声明或代码段均有错误。尽可能多地找出。

- 35. catch

```cpp
{
  quotient = divide(num1, num2);
  cout << "The quotient is " << quotient << endl;
}
try (string exceptionString)
{
  cout << exceptionString;
}
```

- 36. try

```cpp
{
  quotient = divide(num1, num2);
}
cout << "The quotient is " << quotient << endl;
catch (string exceptionString)
{
  cout << exceptionString;
}
```

- 37. template <class T>

```cpp
T square(T number)
{
  return T * T;
}
```

# 编程挑战

38. template <class T>
int square(int number)
{
  return number * number;
}

39. template <class T1, class T2>
T1 sum(T1 x, T1 y)
{
  return x + y;
}

40. 假设以下定义出现在使用本章介绍的 SimpleVector 类模板的程序中。假设以下语句出现在已定义 `valueSet` 为本章介绍的 SimpleVector 类对象的程序中。假设 `valueSet` 是一个 `int` 向量，且有 20 个元素。
`SimpleVector<int> array(25);`
`cout << valueSet[2] << endl;`

### 1. 日期异常
修改你在第 13 章编程挑战 1（Date）中编写的日期类。该类应实现以下异常类：

- `InvalidDay`：当向类传递无效的天数（< 1 或 > 31）时抛出异常。
- `InvalidMonth`：当向类传递无效的月份（< 1 或 > 12）时抛出异常。
在驱动程序中演示该类的用法。

### 2. 时间格式异常
修改你在第 15 章编程挑战 4（Time Format）中创建的 MiTime 类。该类应实现以下异常：

- `BadHour`：当向类传递无效的小时（< 0 或 > 2359）时抛出异常。
- `BadSeconds`：当向类传递无效的秒数（< 0 或 > 59）时抛出异常。
在驱动程序中演示该类的用法。

### 3. 最大/最小模板
为 `minimum` 和 `maximum` 两个函数编写模板。`minimum` 函数接受两个参数并返回两个中较小的值。`maximum` 函数接受两个参数并返回两个中较大的值。设计一个简单的驱动程序，用各种数据类型演示这些函数。

### 4. 绝对值模板
编写一个函数模板，接受一个参数并返回其绝对值。数的绝对值是其去掉符号的值。例如，-5 的绝对值是 5，2 的绝对值是 2。在简单的驱动程序中测试该模板。

### 5. 总和模板
为名为 `total` 的函数编写模板。该函数应该记录用户输入值的运行总和。函数应返回总和。参数应该是要输入的值的数量。在驱动程序中测试该模板。

### 6. IntArray 异常
实现一个 `IntArray` 类，动态创建一个数组并对数组进行边界检查。如果使用了无效下标，它应该抛出异常并显示消息。

### 7. TestScores
编写一个名为 `TestScores` 的类。构造函数应接受一个分数数组。该类应该有一个返回分数平均值的成员函数。如果任何测试分为负或大于 100，它应该抛出异常。在驱动程序中演示该类的用法。

### 8. SimpleVector 修改
修改本章介绍的 `SimpleVector` 类，添加 `push_back` 和 `pop_back` 成员函数。`push_back` 函数接受一个参数并插入数组末尾。`pop_back` 函数应从数组中删除最后一个元素。

### 9. SearchableVector 修改
修改本章介绍的 `SearchableVector` 类，使其使用二分查找代替线性查找。测试该模板。

### 10. SortableVector 
编写一个名为 `SortableVector` 的类模板，它应派生自 `SimpleVector` 类。它应该有一个按升序排序数组的成员函数。在驱动程序中测试该模板。

### 11. 继承修改
假设你完成了编程挑战 9 和 10，修改 `SearchableVector` 的继承关系，使其派生自 `SortableVector` 类。

### 12. 特化模板
在本章第 16.4 节中描述了如何设计为特定数据类型设计的模板。实现 `SimpleVector` 的特化版本，使其能够处理字符串。在驱动程序中演示它们。

### 13. 异常项目
此作业假设你已完成第 15 章编程挑战 1（Employee 和 ProductionWorker）。修改 `Employee` 和 `ProductionWorker` 类，在发生以下错误时抛出异常：

- `Employee` 类在接收小于 0 或大于 9999 的员工编号时，抛出名为 `InvalidEmployeeNumber` 的异常。
- `ProductionWorker` 类在接收无效班次时，抛出名为 `InvalidShift` 的异常。
- `ProductionWorker` 类在接收负的小时薪率时，抛出名为 `InvalidPayRate` 的异常。

编写一个驱动程序，演示这些异常条件的工作原理。

## 容器

STL 中有两种类型的容器类：序列容器（sequence）和关联容器（associative）。序列容器在内存中按顺序存储其数据，其方式类似于数组。关联容器则以非顺序的方式存储其数据，这使得定位元素速度更快。

STL 目前提供的序列容器列如表 17-1 所示。（注意，`deque` 容器将在第 19 章讨论，`list` 和 `forward_list` 容器将在第 18 章讨论。）

## 表 17-1 序列容器

| 容器类 | 描述 |
| --- | --- |
| array | 一种固定大小的容器，类似于数组。 |
| deque | 双端队列。像 `vector` 一样，它可以快速地从前端和末尾添加或删除元素。（该容器将在第 19 章讨论）。 |
| forward_list | 数据元素的单向链表。可以在任何位置插入或删除值。（该容器将在第 18 章讨论）。 |
| list | 数据元素的双向链表。可以在任何位置插入或删除值。（该容器将在第 18 章讨论）。 |
| vector | 一种像可扩展数组一样工作的容器。可以在 `vector` 中添加或删除值。`vector` 会自动调整其大小以适应包含的元素数量。 |

STL 目前提供的关联容器列如表 17-2 所示。

## 表 17-2 关联容器

| 容器类 | 描述 |
| --- | --- |
| set | 存储一组排序的唯一值。不允许重复。 |
| multiset | 存储一组排序的唯一值。允许重复。 |
| map | 将一组键映射到数据元素。每个数据元素只允许一个键。不允许重复。元素按键的顺序排序。 |
| multimap | 将一组键映射到数据元素。每个数据元素允许多个键。允许重复。元素按键的顺序排序。 |
| unordered_set | 与 `set` 相似，不同之处元素没有排序。 |
| unordered_multiset | 与 `multiset` 相似，不同之处元素没有排序。 |
| unordered_map | 与 `map` 相似，不同之处元素没有排序。 |
| unordered_multimap | 与 `multimap` 相似，不同之处元素没有排序。 |

除了表 17-1 和 17-2 中列出的类外，STL 还提供了表 17-3 所示的三个容器适配器类。容器适配器类本身不是容器，而是将其他容器适配到特定用处的类。注意，我们将在第 19 章讨论这些类。

## 表 17-3 容器适配器类

| 容器适配器类 | 描述 |
| --- | --- |
| stack | 一种在 `deque`（默认）中存储元素的适配器类。栈是一个后进先出（LIFO）容器。当你从栈中检索元素时，栈总是给你最后一个插入的元素。（该类将在第 19 章讨论）。 |
| queue | 一种在 `deque`（默认）中存储元素的适配器类。队列是一个先入后出（FIFO）容器。当你从栈中检索元素时，栈总是给你第一个（或最早）插入的元素。（该类将在第 19 章讨论）。 |
| priority_queue | 一种在 `vector`（默认）中存储元素的适配器类。在这种数据结构中，你检索的元素始终是值最大的元素。（该类将在第 19 章讨论）。 |

容器和容器适配器类在各种 STL 头文件中声明。表 17-4 列出了根据你意图使用的容器需要包含的必要头文件。

## 表 17-4 头文件

| 头文件 | 类 |
| --- | --- |
| `<array>` | array |
| `<deque>` | deque |
| `<forward_list>` | forward_list |
| `<list>` | list |
| `<map>` | map, multimap |
| `<queue>` | queue, priority_queue |
| `<set>` | set, multiset |
| `<stack>` | stack |
| `<unordered_map>` | unordered_map, unordered_multimap |
| `<unordered_set>` | unordered_set, unordered_multiset |
| `<vector>` | vector |

## array 类介绍

也许 STL 中最简单的容器可能是 `array` 类，它是在 C++ 11 中引入的。`array` 对象的工作非常类似于普通数组。它是一个持有相同数据类型元素的固定大小容器。事实上，`array` 对象在内部使用传统数组来存储其元素。`array` 对象相对于普通数组的优势是它有一个 `size()` 成员函数，可以返回对象中包含的元素数量。

![](img/191adf3284699566e6a7b1008ce9bdb5_1064_0.png)

当你定义 `array` 对象时，必须指定元素的数据类型以及对象将存储的元素数量。这是一个示例：

```cpp
array<int, 5> numbers;
```

该语句定义了一个名为 `numbers` 的 `array` 对象。在括号 `<>` 中，数据类型是每个元素的类型，值 `5` 是对象将存储的元素数量。

当你定义 `array` 对象时，必须指定元素的数据类型以及对象将存储的元素数量。这是一个示例：

```cpp
array<int, 5> numbers;
```

该语句定义了一个名为 `numbers` 的 `array` 对象。在括号 `<>` 中，数据类型是每个元素的类型，值 `5` 是对象将存储的元素数量。

`array` 类重载了 `[]` 运算符，让你像使用普通数组一样访问元素。这是一个创建并初始化 `array` 的示例：

```cpp
#include <iostream>
#include <string>
#include <array>

using namespace std;

int main() {
    const int SIZE = 4;
    array<string, SIZE> names = {"Jamie", "Ashley", "Doug", "Claire"};
    cout << "Here are the names:\n";
    for (int i = 0; i < names.size(); i++) {
        cout << names[i] << endl;
    }
    return 0;
}
```

## 输出

```
Here are the names:
Jamie
Ashley
Doug
Claire
```
