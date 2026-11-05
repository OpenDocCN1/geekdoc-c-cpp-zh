
```
}
```

将得到：

```
9
10
```

注意：Continue 在 while 或 do-while 循环中通常最有用。对于具有明确退出条件的 for 循环，可能受益不大。

### 第 28.7 节：While 循环

```
int n = 0;
while (n < 5)
{
    Console.WriteLine(n);
    n++;
}
```

输出：

- 0
- 1
- 2
- 3
- 4

IEnumerator 可以使用 while 循环进行迭代：

// Call a custom method that takes a count, and returns an IEnumerator for a list
// of strings with the names of the largest city metro areas.
IEnumerator<string> largestMetroAreas = GetLargestMetroAreas(4);

while (largestMetroAreas.MoveNext())
{
    Console.WriteLine(largestMetroAreas.Current);
}
```

示例输出：

- Tokyo/Yokohama
- New York Metro
- Sao Paulo
- Seoul/Incheon

### 第 28.8 节：break

有时需要在循环中间检查循环条件。前者可以说比后者更优雅：

```
for (;;)
{
    // precondition code that can change the value of should_end_loop expression
    if (should_end_loop)
        break;
    // do something
}
```

替代方案：

```
bool endLoop = false;
for ( ; !endLoop; )
{
    // precondition code that can set endLoop flag
    if (!endLoop)
    {
        // do something
    }
}
```

注意：在嵌套循环和/或 switch 中必须使用不仅仅是简单的 break。

## 第 29 章：迭代器

### 第 29.1 节：使用 Yield 创建迭代器

迭代器产生枚举器。在 C# 中，枚举器是通过定义包含 `yield` 语句的方法、属性或索引器来产生的。

大多数方法会通过普通的 `return` 语句将控制权返回给调用者，这会释放该方法本地的所有状态。相比之下，使用 `yield` 语句的方法允许它们在保留返回这些值之间本地状态的同时，根据请求向调用者返回多个值。这些返回值构成一个序列。迭代器中使用了两种类型的 `yield` 语句：

- `yield return`，它将控制权返回给调用者但保留状态。当控制权传回时，被调用方将从该行继续执行。
- `yield break`，其功能类似于普通的 `return` 语句——这表示序列的结束。普通的 `return` 语句本身在迭代器块中是非法的。

以下示例演示了一个可用于生成斐波那契数列的迭代器方法：

```
~~~csharp
IEnumerable<int> Fibonacci(int count)
{
    int prev = 1;
    int curr = 1;

    for (int i = 0; i < count; i++)
    {
        yield return prev;
        int temp = prev + curr;
        prev = curr;
        curr = temp;
    }
}
~~~
```

然后此迭代器可用于生成斐波那契数列的枚举器，供调用方法使用。下面的代码演示了如何枚举斐波那契数列中的前十项：

```
~~~csharp
void Main()
{
    foreach (int term in Fibonacci(10))
    {
        Console.WriteLine(term);
    }
}
~~~
```

**输出**

```
~~~text
1
1
2
3
5
8
13
21
~~~
```

### 第 29.2 节：简单数值迭代器示例

迭代器的常见用例是对一组数字执行某些操作。下面的示例演示了如何将数字数组中的每个元素单独打印到控制台。

这是因为数组实现了 IEnumerable 接口，允许客户端使用 GetEnumerator() 方法为数组获取迭代器。此方法返回一个枚举器，它是数组中每个数字上的只读、仅向前游标。

```
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

IEnumerator iterator = numbers.GetEnumerator();

while (iterator.MoveNext())
{
    Console.WriteLine(iterator.Current);
}
```
```

输出

```
```
1
2
3
4
5
```
```

也可以使用 foreach 语句实现相同的结果：

```
```csharp
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```
```

## 第 30 章：IEnumerable

IEnumerable 是所有可枚举的非泛型集合（如 ArrayList）的基接口。

IEnumerable<T> 是所有泛型枚举器（如 List<>）的基接口。

IEnumerable 是一个接口，实现 GetEnumerator 方法。GetEnumerator 方法返回一个 IEnumerable，它提供像 foreach 一样的遍历集合的选项。

### 第 30.1 节：带自定义枚举器的 IEnumerable

实现 IEnumerable 接口允许类像 BCL 集合一样被枚举。这需要扩展跟踪枚举状态的 Enumerator 类。

除迭代标准集合外，示例包括：

- 基于函数而非对象集合使用数字范围
- 在集合上实现不同的迭代算法，如在图集合上的 DFS 或 BFS

```
public static void Main(string[] args) {
    foreach (var coffee in new CoffeeCollection()) {
        Console.WriteLine(coffee);
    }
}

public class CoffeeCollection : IEnumerable {
    private CoffeeEnumerator enumerator;

    public CoffeeCollection() {
        enumerator = new CoffeeEnumerator();
    }

    public IEnumerator GetEnumerator() {
        return enumerator;
    }
}

public class CoffeeEnumerator : IEnumerator {
    string[] beverages = new string[3] { "espresso", "macchiato", "latte" };
    int currentIndex = -1;

    public object Current {
        get {
            return beverages[currentIndex];
        }
    }

    public bool MoveNext() {
        currentIndex++;
        if (currentIndex < beverages.Length) {
            return true;
        }
        return false;
    }

    public void Reset() {
        currentIndex = 0;
    }
}
```

```
}
}
```

### 第 30.2 节：IEnumerable<int>

在最基本的形式中，实现 IEnumerable 的对象表示一系列对象。相关对象可以使用 C# 的 foreach 关键字进行迭代。

在下面的示例中，对象 sequenceOfNumbers 实现了 IEnumerable。它表示一系列整数。

foreach 循环依次遍历每个元素。

```
int AddNumbers(IEnumerable<int> sequenceOfNumbers) {
    int returnValue = 0;
    foreach(int i in sequenceOfNumbers) {
        returnValue += i;
    }
    return returnValue;
}
```

## 第 31 章：值类型与引用类型

### 第 31.1 节：使用 ref 关键字按引用传递

来自文档：

> 在 C# 中，参数可以按值或按引用传递给参数。按引用传递使函数成员、方法、属性、索引器、运算符和构造函数能够更改参数的值，并使该更改在调用环境中保持不变。要按引用传递参数，请使用 ref 或 out 关键字。

ref 与 out 的区别在于 out 意味着传递的参数必须在函数结束前被赋值。相比之下，使用 ref 传递的参数可以被更改或保持不变。

```
using System;

class Program
{
    static void Main(string[] args)
    {
        int a = 20;
        Console.WriteLine("Inside Main - Before Callee: a = {0}", a);
        Callee(a);
        Console.WriteLine("Inside Main - After Callee: a = {0}", a);

        Console.WriteLine("Inside Main - Before CalleeRef: a = {0}", a);
        CalleeRef(ref a);
        Console.WriteLine("Inside Main - After CalleeRef: a = {0}", a);

        Console.WriteLine("Inside Main - Before CalleeOut: a = {0}", a);
        CalleeOut(out a);
        Console.WriteLine("Inside Main - After CalleeOut: a = {0}", a);

        Console.ReadLine();
    }

    static void Callee(int a)
    {
        a = 5;
        Console.WriteLine("Inside Callee a : {0}", a);
    }

    static void CalleeRef(ref int a)
    {
        a = 6;
        Console.WriteLine("Inside CalleeRef a : {0}", a);
    }

    static void CalleeOut(out int a)
    {
        a = 7;
        Console.WriteLine("Inside CalleeOut a : {0}", a);
    }
}
```

输出：
