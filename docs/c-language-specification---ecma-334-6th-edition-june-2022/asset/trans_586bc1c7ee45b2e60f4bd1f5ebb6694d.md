
如下文所述的接口。建议在重载解析产生的结果不是明确的公共实例方法或没有适用方法时发出警告。

-   如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不执行后续步骤。
-   在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果是一个错误，或者结果不是允许读取的公共实例属性，则产生错误，并且不执行后续步骤。
-   在 E 上使用标识符 MoveNext 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果是一个错误，或者结果不是方法组，则产生错误，并且不执行后续步骤。
-   在方法组上使用空实参列表执行重载解析。如果重载解析导致没有适用方法、导致二义性，或者导致单个最佳方法但该方法为静态或非公共，或者其返回类型不是 bool，则产生错误，并且不执行后续步骤。
-   集合类型为 X，枚举器类型为 E，迭代类型为 Current 属性的类型。

否则，检查可枚举接口：

-   如果在所有存在从 X 到 IEnumerable<T_i> 的隐式转换的类型 T_i 中，存在唯一类型 T，使得 T 不是 dynamic，并且对于所有其他 T_i 都存在从 IEnumerable<T> 到 IEnumerable<T_i> 的隐式转换，那么集合类型为接口 IEnumerable<T>，枚举器类型为接口 IEnumerator<T>，迭代类型为 T。
-   否则，如果存在多个这样的类型 T，则产生错误，并且不执行后续步骤。
-   否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，那么集合类型为此接口，枚举器类型为接口 System.Collections.IEnumerator，迭代类型为 object。
-   否则，产生错误，并且不执行后续步骤。

上述步骤如果成功，将明确产生集合类型 C、枚举器类型 E 和迭代类型 T。形式为

```
foreach (V v in x) «embedded_statement»
```

的 foreach 语句随后展开为：
```
{
    E e = ((C)x).GetEnumerator();
    try
    {
        while (e.MoveNext())
        {
            V v = (V)(T)e.Current;
            «embedded_statement»
        }
    }
    finally
    {
        ... // Dispose e
    }
}
```

变量 e 对表达式 x、嵌入语句或程序中的任何其他源代码均不可见也不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（迭代类型）到 V（foreach 语句中的 local_variable_type）的显式转换（§10.3），则产生错误，并且不执行后续步骤。

*注意：如果 x 的值为 null，则在运行时引发 System.NullReferenceException。注意结束*

允许实现以不同方式实现给定的 foreach_statement；例如，出于性能原因，只要行为与上述展开一致即可。

将 v 放在 while 循环内部，对于嵌入语句中出现的任何匿名函数如何捕获它（§11.16.6.2）很重要。

*示例：*

```
int[] values = { 7, 9, 13 };
Action f = null;
foreach (var value in values)
{
    if (f == null)
    {
        f = () => Console.WriteLine("First value: " + value);
    }
}
f();
```

如果展开形式中的 v 声明在 while 循环之外，那么它将在所有迭代之间共享，并且其在 for 循环之后的值将是最终值 13，这也是调用 f 将打印的内容。相反，由于每次迭代都有自己的变量 v，第一次迭代中由 f 捕获的变量将继续保持值 7，这也是将打印的内容。（请注意，早期版本的 C# 在 while 循环之外声明 v。）

*示例结束*

finally 块的主体按以下步骤构造：

-   如果存在从 E 到 System.IDisposable 接口的隐式转换，则
    -   如果 E 是不可为 null 的值类型，则 finally 子句展开为以下语义等价形式：

```
finally
{
    ((System.IDisposable)e).Dispose();
}
```

    -   否则，finally 子句展开为以下语义等价形式：

```
finally
{
    System.IDisposable d = e as System.IDisposable;
    if (d != null)
    {
        d.Dispose();
    }
}
```

但以下情况除外：如果 E 是值类型，或者 E 是实例化为值类型的类型参数，则将 e 转换为 System.IDisposable 不得导致装箱。

-   否则，如果 E 是密封类型，则 finally 子句展开为空块：
    
    `finally {}`

-   否则，finally 子句展开为：

```
finally
{
    System.IDisposable d = e as System.IDisposable;
    if (d != null)
    {
        d.Dispose();
    }
}
```

局部变量 d 对任何用户代码均不可见也不可访问。特别是，它不会与作用域包含该 finally 块的任何其他变量冲突。

foreach 遍历数组元素的顺序如下：对于一维数组，元素按索引递增顺序遍历，从索引 0 开始，到索引 Length - 1 结束。对于多维数组，元素的遍历顺序是使最右侧维度的索引先增加，然后下一个左侧维度，依此类推直至最左侧。

示例：以下示例按元素顺序打印二维数组中的每个值：

```
using System;
class Test
{
    static void Main()
    {
        double[,] values =
        {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
        {
            Console.Write("${elementValue} ");
        }
        Console.WriteLine();
    }
}
```

产生的输出如下：

1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9

示例结束

示例：在以下示例中

```
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers)
{
Console.WriteLine(n);
}
```

n 的类型被推断为 int，即 numbers 的迭代类型。

示例结束

## 12.10 跳转语句

### 12.10.1 概述

跳转语句无条件转移控制。

```
jump_statement
: break_statement
| continue_statement
| goto_statement
| return_statement
| throw_statement
;
```

跳转语句将控制转移到的位置称为该跳转语句的目标。

当跳转语句出现在某个块内，而该跳转语句的目标在该块外时，称该跳转语句退出该块。虽然跳转语句可以将控制转移出块，但它绝不能将控制转移入块。

由于存在中间的 try 语句，跳转语句的执行变得复杂。在不存在此类 try 语句时，跳转语句无条件地将控制从该跳转语句转移到其目标。在存在此类中间 try 语句时，执行更为复杂。如果跳转语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点时（如果会到达），控制将转移到下一个外层 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。

示例：在以下代码中

```
using System;
class Test
{
    static void Main()
    {
        while (true)
        {
            try
            {
                try
                {
                    Console.WriteLine("Before break");
                    break;
                }
                finally
                {
                    Console.WriteLine("Innermost finally block");
                }
            }
        }
    }
}
```

