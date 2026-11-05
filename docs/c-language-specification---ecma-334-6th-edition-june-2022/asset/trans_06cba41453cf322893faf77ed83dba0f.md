
```csharp
{
    sum += selector(item);
}
return sum;
}
}
```

`ItemList<T>` 类有两个 `Sum` 方法。每个方法都接受一个选择器参数，该参数从列表项中提取要求和的値。提取的值可以是 `int` 或 `double`，所得和同样是 `int` 或 `double`。

例如，`Sum` 方法可用于计算订单中明细行列表的总和。

```csharp
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}
```

```csharp
void ComputeSums()
{
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
    ...
}
```

在第一次调用 `orderDetails.Sum` 时，两个 `Sum` 方法都适用，因为匿名函数 `d => d.UnitCount` 与 `Func<Detail,int>` 和 `Func<Detail,double>` 都兼容。但是，重载决策选择第一个 `Sum` 方法，因为到 `Func<Detail,int>` 的转换优于到 `Func<Detail,double>` 的转换。

在第二次调用 `orderDetails.Sum` 时，只有第二个 `Sum` 方法适用，因为匿名函数 `d => d.UnitPrice * d.UnitCount` 生成 `double` 类型的值。因此，重载决策为该调用选择第二个 `Sum` 方法。

*示例结束*

## 11.16.5 匿名函数与动态绑定

匿名函数不能作为动态绑定操作的接收方、参数或操作数。

## 11.16.6 外部变量

### 11.16.6.1 概述

任何局部变量、值参数或参数数组，只要其作用域包含 *lambda_expression* 或 *anonymous_method_expression*，就称为该匿名函数的**外部变量**。在类的实例函数成员中，this 值被视为值参数，并且是该函数成员内包含的任何匿名函数的*外部变量*。

### 11.16.6.2 捕获的外部变量

当匿名函数引用某个外部变量时，称该外部变量已被该匿名函数**捕获**。通常，局部变量的生存期仅限于与其关联的块或语句的执行期间（§9.2.8）。但是，捕获的外部变量的生存期至少会延长到由该匿名函数创建的委托或表达式树可供垃圾回收为止。

示例：在以下示例中

```
using System;

delegate int D();

class Test
{
    static D F()
    {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main()
    {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```

局部变量 x 被该匿名函数捕获，并且 x 的生存期至少会延长到从 F 返回的委托可供垃圾回收为止。由于每次调用该匿名函数都操作同一个 x 实例，因此该示例的输出为：

1
2
3

示例结束

当局部变量或值参数被匿名函数捕获时，该局部变量或参数不再被视为固定变量（§22.4），而是被视为可移动变量。但是，捕获的外部变量不能在 fixed 语句（§22.7）中使用，因此不能获取捕获的外部变量的地址。

> 注意：与未捕获的变量不同，捕获的局部变量可以同时暴露给多个执行线程。 注释结束

### 11.16.6.3 局部变量的实例化

当执行进入变量的作用域时，局部变量被视为已实例化。

示例：例如，当调用以下方法时，局部变量 x 会被实例化并初始化三次——循环的每次迭代一次。

```
static void F()
{
    for (int i = 0; i < 3; i++)
    {
        int x = i * 2 + 1;
        ...
    }
}
```

```
int x;
for (int i = 0; i < 3; i++)
{
    x = i * 2 + 1;
    result[i] = () => Console.WriteLine(x);
}
return result;
}
```

输出为：

5
5
5

请注意，允许（但不要求）编译器将三次实例化优化为单个委托实例（§10.7.2）。

*示例结束*

如果 for 循环声明了迭代变量，则该变量本身被视为在循环外部声明。

*示例：* 因此，如果将示例改为捕获迭代变量本身：

```
static D[] F()
{
    D[] result = new D[3];
    for (int i = 0; i < 3; i++)
    {
        result[i] = () => Console.WriteLine(i);
    }
    return result;
}
```

只会捕获迭代变量的一个实例，从而产生输出：

3
3
3

*示例结束*

匿名函数委托可以共享某些捕获的变量，而其他捕获变量则具有单独的实例。

*示例：* 例如，如果将 F 改为

```
static D[] F()
{
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++)
    {
        int y = 0;
        result[i] = () => Console.WriteLine($"{+x} {+y}");
    }
    return result;
}
```

这三个委托捕获同一个 *x* 实例，但捕获不同的 *y* 实例，输出为：

```
1 1
2 1
3 1
```

*示例结束*

不同的匿名函数可以捕获同一个外部变量实例。

*示例：* 在以下示例中：

```csharp
using System;

delegate void Setter(int value);
delegate int Getter();

class Test
{
    static void Main()
    {
        int x = 0;
        Setter s = (int value) => x = value;
        Getter g = () => x;
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```

这两个匿名函数捕获同一个局部变量 x 的实例，因此它们可以通过该变量“通信”。该示例的输出为：

```
5
10
```

*示例结束*

## 11.16.7 匿名函数表达式的求值

匿名函数 *F* 应始终转换为委托类型 *D* 或表达式树类型 *E*，可以直接转换，也可以通过执行委托创建表达式 `new D(F)` 进行转换。此转换决定匿名函数的结果，如 §10.7 所述。

## 11.16.8 实现示例

**本子条款为资料性内容。**

本子条款描述匿名函数转换基于其他 C# 构造的一种可能实现。此处描述的实现基于商业 C# 编译器所使用的相同原则，但它绝不是强制实现，也不是唯一可能的实现。它仅简要提及到表达式树的转换，因为其确切语义不在本规范范围内。

本子条款的其余部分给出几个包含具有不同特征的匿名函数的代码示例。对于每个示例，都会提供仅使用其他 C# 构造的对应代码转换。在这些示例中，假定标识符 D 表示以下委托类型：

```
public delegate void D();
```

匿名函数的最简单形式是不捕获任何外部变量的形式：

```
class Test
{
    static void F()
    {
        D d = () => Console.WriteLine("test");
    }
}
```

这可以转换为一个委托实例化，该实例化引用一个编译器生成的静态方法，匿名函数的代码置于该方法中：

```
class Test
{
    static void F()
    {
        D d = new D(__Method1);
    }

    static void __Method1()
    {
        Console.WriteLine("test");
    }
}
```

在以下示例中，匿名函数引用 this 的实例成员：

```
class Test
{
    int x;

    void F()
    {
        D d = () => Console.WriteLine(x);
    }
}
```

这可以转换为一个编译器生成的实例方法，该方法包含匿名函数的代码：

```
class Test
{
    int x;

    void F()
    {
        D d = new D(__Method1);
    }

    void __Method1()
    {
        Console.WriteLine(x);
    }
}
```

