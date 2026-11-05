
- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。
- for 语句是可到达的，并且存在 for 条件，且该条件不具有常量值 true。

## 13.9.5 foreach 语句

foreach 语句枚举集合的元素，并对集合中的每个元素执行一个嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

foreach 语句的 local-variable-type 和 identifier 声明该语句的迭代变量。如果将 var 标识符作为 local-variable-type 给出，并且作用域中没有名为 var 的类型，则称该迭代变量为隐式类型迭代变量，其类型按如下所述取为 foreach 语句的元素类型。迭代变量对应于一个只读局部变量，其作用域覆盖嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在对其进行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或者 ++ 和 -- 运算符）或者将迭代变量作为 ref 或 out 参数传递，则发生编译时错误。

为简洁起见，下文中的 IEnumerable、IEnumerator、IEnumerable<T> 和 IEnumerator<T> 指代命名空间 System.Collections 和 System.Collections.Generic 中的对应类型。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和元素类型。该确定过程如下：

- 如果表达式的类型 X 是数组类型，则存在从 X 到 IEnumerable 接口的隐式引用转换（因为 System.Array 实现此接口）。集合类型为 IEnumerable 接口，枚举器类型为 IEnumerator 接口，元素类型为数组类型 X 的元素类型。
- 如果表达式的类型 X 是 dynamic，则存在从表达式到 IEnumerable 接口的隐式转换（§11.2.9）。集合类型为 IEnumerable 接口，枚举器类型为 IEnumerator 接口。如果将 var 标识符作为 local-variable-type 给出，则元素类型为 dynamic；否则为 object。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且不带类型实参执行成员查找。如果成员查找未产生匹配，或产生二义性，或产生的匹配不是方法组，则按下面所述检查可枚举接口。建议在成员查找产生的结果不是方法组或没有匹配时发出警告。
  - 使用得到的方法组和空参数列表执行重载决策。如果重载决策没有找到适用方法、产生二义性，或者只找到一个最佳方法但该方法为静态方法或不是公共方法，则按下面所述检查可枚举接口。建议在重载决策产生的结果不是无二义性的公共实例方法或没有适用方法时发出警告。
  - 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不再执行后续步骤。
  - 在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找没有产生匹配、结果为错误，或者结果不是允许读取的公共实例属性，则产生错误，并且不再执行后续步骤。
- 在 E 上使用标识符 MoveNext 且不带类型实参执行成员查找。如果成员查找没有产生匹配、结果为错误，或者结果不是方法组，则产生错误，并且不再执行后续步骤。
- 使用空参数列表对该方法组执行重载决策。如果重载决策没有找到适用方法、产生二义性，或者只找到一个最佳方法但该方法为静态方法、不是公共方法，或者其返回类型不是 bool，则产生错误，并且不再执行后续步骤。
- **集合类型**为 X，**枚举器类型**为 E，**元素类型**为 Current 属性的类型。
- 否则，检查可枚举接口：
  - 如果在所有存在从 X 到 IEnumerable<T_i> 的隐式转换的类型 T_i 中，存在唯一类型 T，使得 T 不是 dynamic，并且对于所有其他 T_i，都存在从 IEnumerable<T> 到 IEnumerable<T_i> 的隐式转换，则**集合类型**为接口 IEnumerable<T>，**枚举器类型**为接口 IEnumerator<T>，**元素类型**为 T。
  - 否则，如果这样的类型 T 多于一个，则产生错误，并且不再执行后续步骤。
  - 否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，则**集合类型**为该接口，**枚举器类型**为接口 System.Collections.IEnumerator，**元素类型**为 object。
  - 否则，产生错误，并且不再执行后续步骤。

上述步骤如果成功，将明确产生集合类型 C、枚举器类型 E 和元素类型 T。形式如下的 foreach 语句

```
foreach (V v in x) embedded-statement
```

随后展开为：

```
{
    E e = ((C)(x)).GetEnumerator();
    try {
        while (e.MoveNext()) {
            V v = (T)e.Current;
            embedded-statement
        }
    }
    finally {
        ... // Dispose e
    }
}
```

变量 e 对表达式 x、嵌入语句或程序的任何其他源代码不可见也不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V（foreach 语句中的 local-variable-type）的显式转换（§11.2.13），则产生错误，并且不再执行后续步骤。[注意：如果 x 的值为 null，则运行时将引发 System.NullReferenceException。注意结束]

允许实现以不同方式实现给定的 foreach 语句；例如，出于性能原因，只要其行为与上述展开一致即可。

v 放在 while 循环内部的位置很重要，因为它决定了嵌入语句中出现的任何匿名函数如何捕获（§12.16.6.2）它。

[示例：]

```csharp
int[] values = { 7, 9, 13 };
Action f = null;
foreach (var value in values)
{
    if (f == null) f = () => Console.WriteLine("First value: " + value);
    f();
}
```

如果展开形式中的 v 声明在 while 循环之外，那么它将在所有迭代之间共享，并且它在 for 循环之后的值将是最终值 13，这也是调用 f 时会打印的内容。相反，由于每次迭代都有自己的变量 v，第一次迭代中由 f 捕获的变量将继续保持值 7，这也正是会打印的内容。（请注意，早期版本的 C# 将 v 声明在 while 循环之外。）*示例结束*

finally 块的主体按照以下步骤构造：

- 如果存在从 E 到 `System.IDisposable` 接口的隐式转换，则
  - 如果 E 是不可为 null 的值类型，则 finally 子句展开为以下语义等价形式：
    ```csharp
    finally {
        ((System.IDisposable)e).Dispose();
    }
    ```
  - 否则，finally 子句展开为以下语义等价形式：
    ```csharp
    finally {
        System.IDisposable d = e as System.IDisposable;
        if (d != null) d.Dispose();
    }
    ```
    但有一种情况例外：如果 E 是值类型，或者实例化为值类型的类型参数，则将 e 转换为 `System.IDisposable` 不得导致装箱发生。
- 否则，如果 E 是密封类型，则 finally 子句展开为空块：
  ```csharp
  finally {
  }
  ```
- 否则，finally 子句展开为：
  ```csharp
  finally {
      System.IDisposable d = e as System.IDisposable;
      if (d != null) d.Dispose();
  }
  ```

局部变量 d 对任何用户代码不可见也不可访问。特别地，它不会与作用域包含该 finally 块的任何其他变量冲突。

foreach 遍历数组元素的顺序如下：对于一维数组，元素按索引递增顺序遍历，从索引 0 开始，到索引 Length – 1 结束。对于多维数组，遍历元素时，最右侧维度的索引先递增，然后向左下一维度递增，依此类推。

[示例：以下示例按元素顺序打印二维数组中的每个值：

```csharp
using System;
class Test
{
    static void Main() {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);
        Console.WriteLine();
    } }
```
