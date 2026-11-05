
| expression
;

资源是一个实现了 System.IDisposable 接口的类或结构体，该接口包含一个名为 Dispose 的无参数方法。使用资源的代码可以调用 Dispose 来表示资源不再需要。

如果 resource_acquisition 的形式是 local_variable_declaration，则 local_variable_declaration 的类型应为 dynamic 或可隐式转换为 System.IDisposable 的类型。如果 resource_acquisition 的形式是 expression，则该表达式应可隐式转换为 System.IDisposable。

在 resource_acquisition 中声明的局部变量是只读的，并且必须包含初始化器。如果嵌入语句尝试修改这些局部变量（通过赋值或 ++ 和 -- 运算符）、获取它们的地址，或将它们作为 ref 或 out 参数传递，则会发生编译时错误。

using 语句被翻译为三个部分：获取、使用和释放。资源的使用被隐式包含在包含 finally 子句的 try 语句中。该 finally 子句会释放资源。如果获取到空资源，则不会调用 Dispose，也不会抛出异常。如果资源的类型为 dynamic，则在获取期间会通过隐式动态转换（§10.2.10）将其动态转换为 IDisposable，以确保在实际使用和释放之前转换成功。

using 语句的形式

```
using (ResourceType resource = «expression» ) «statement»
```

对应于三种可能的展开之一。当 ResourceType 是不可为空的值类型或具有值类型约束的类型参数（§14.2.5）时，展开在语义上等价于

```
{
  ResourceType resource = «expression»;
  try
  {
    «statement»;
  }
  finally
  {
    ((IDisposable)resource).Dispose();
  }
}
```

除非 resource 到 System.IDisposable 的强制转换不会导致装箱发生。

否则，当 ResourceType 为 dynamic 时，展开为

否则，展开为

```csharp
    {
        ResourceType resource = «expression»;
        try
        {
            «statement»;
        }
        finally
        {
            IDisposable d = (IDisposable)resource;
            if (d != null)
            {
                d.Dispose();
            }
        }
    }
```

在任何展开中，`resource` 变量在嵌入语句中是只读的，而 `d` 变量在嵌入语句中不可访问且对嵌入语句不可见。

实现可以以不同的方式实现给定的 `using_statement`，例如出于性能原因，只要行为与上述展开一致即可。

using 语句的形式：

```csharp
    using («expression») «statement»
```

具有相同的三种可能的展开。在这种情况下，`ResourceType` 隐式为 `expression` 的编译时类型（如果存在）。否则，接口 `IDisposable` 本身用作 `ResourceType`。`resource` 变量在嵌入语句中不可访问且对嵌入语句不可见。

当 `resource_acquisition` 采用 `local_variable_declaration` 的形式时，可以获取给定类型的多个资源。using 语句的形式

```csharp
    using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) «statement»
```

精确等价于一系列嵌套的 using 语句：

```csharp
    using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
    ...
    using (ResourceType rN = eN)
    «statement»
```

示例：下面的示例创建一个名为 `log.txt` 的文件并向其中写入两行文本。然后示例打开同一个文件进行读取并将其中包含的文本行复制到控制台。

```csharp
using System;
using System.IO;

class Test
{
    static void Main()
    {
        using (TextWriter w = File.CreateText("log.txt"))
        {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }
        using (TextReader r = File.OpenText("log.txt"))
        {
            string s;
            while ((s = r.ReadLine()) != null)
            {
                Console.WriteLine(s);
            }
        }
    }
}
```

由于 TextWriter 和 TextReader 类实现了 IDisposable 接口，示例可以使用 using 语句来确保在写入或读取操作后底层文件被正确关闭。

*结束示例*

## 12.15 yield 语句

yield 语句用于在迭代器块（§12.3）中向迭代器的枚举器对象（§14.14.5）或枚举器对象（§14.14.6）产生一个值，或用于发出迭代结束的信号。

```
yield_statement
  : 'yield' 'return' expression ';'
  | 'yield' 'break' ';'
```

yield 是一个上下文关键字（§6.4.4），只有在紧跟 return 或 break 关键字之前使用时才具有特殊含义。

yield 语句可以出现的位置有若干限制，如下所述。

- yield 语句（任一形式）出现在 method_body、operator_body 或 accessor_body 之外是编译时错误。
- yield 语句（任一形式）出现在匿名函数内部是编译时错误。
- yield 语句（任一形式）出现在 try 语句的 finally 子句中是编译时错误。
- yield return 语句出现在包含任何 catch_clauses 的 try 语句中的任何位置是编译时错误。

示例：以下示例显示了 yield 语句的一些有效和无效用法。

```
delegate IEnumerable<int> D();
IEnumerator<int> GetEnumerator()
{
    try
    {
        yield return 1; // Ok
        yield break;    // Ok
    }
    finally
    {
        yield return 2; // Error, yield in finally
        yield break;   // Error, yield in finally
    }
    try
    {
        yield return 3; // Error, yield return in try/catch
        yield break;   // Ok
    }
    catch
    {
        yield return 4; // Error, yield return in try/catch
        yield break;   // Ok
    }
    D d = delegate
    {
        yield return 5; // Error, yield in an anonymous function
    };

    int MyMethod()
    {
        yield return 1;   // Error, wrong return type for an iterator block
    }
}
```

*结束示例*

yield return 语句中表达式的类型到迭代器的 yield 类型（§14.14.4）必须存在隐式转换（§10.2）。

yield return 语句的执行如下：

- 语句中给出的表达式被求值，隐式转换为 yield 类型，并赋给枚举器对象的 Current 属性。
- 迭代器块的执行被挂起。如果 yield return 语句位于一个或多个 try 块内，则相关的 finally 块此时不会执行。
- 枚举器对象的 MoveNext 方法向其调用者返回 true，表示枚举器对象成功推进到下一项。

对枚举器对象的 MoveNext 方法的下一次调用将从上次挂起的位置恢复迭代器块的执行。

yield break 语句的执行如下：

- 如果 yield break 语句被一个或多个带有相关 finally 块的 try 块包围，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制将转移到下一个外层 try 语句的 finally 块。此过程重复进行，直到所有外层 try 语句的 finally 块都已执行。
- 控制返回到迭代器块的调用者。这或者是枚举器对象的 MoveNext 方法或者是 Dispose 方法。

由于 `yield` break 语句无条件地将控制转移到其他地方，因此 `yield` break 语句的终点永远不可达。

## 13. 命名空间

### 13.1 通用

C# 程序使用命名空间进行组织。命名空间既用作程序的“内部”组织系统，也用作“外部”组织系统——一种展示暴露给其他程序的程序元素的方式。

提供了 using 指令（§13.5）以便于使用命名空间。

### 13.2 编译单元

compilation_unit 由零个或多个 extern_alias_directives 组成，其后跟零个或多个 using_directives，其后跟零个或多个 global_attributes，其后跟零个或多个 namespace_member_declarations。compilation_unit 定义了输入的整体结构。

```
compilation_unit
  : extern_alias_directive* using_directive* global_attributes?
    namespace_member_declaration*
  ;
```

C# 程序由一个或多个编译单元组成。当编译 C# 程序时，所有编译单元一起处理。因此，编译单元可以相互依赖，甚至可能以循环方式依赖。

编译单元的 extern_alias_directives 影响该编译单元的 using_directives、global_attributes 和 namespace_member_declarations，但对其他编译单元没有影响。

编译单元的 using_directives 影响该编译单元的 global_attributes 和 namespace_member_declarations，但对其他编译单元没有影响。

编译单元的 global_attributes（§21.3）允许为目标程序集和模块指定属性。程序集和模块充当类型的物理容器。程序集可能由几个物理上分离的模块组成。

程序的每个编译单元的 namespace_member_declarations 向称为全局命名空间的单个声明空间贡献成员。

*示例：*

```
File A.cs:
  class A {}
File B.cs:
  class B {}
```

这两个编译单元贡献给单个全局命名空间，在本例中声明了两个类，其完全限定名为 A 和 B。由于这两个编译单元贡献给相同的声明空间，如果每个编译单元都包含同名成员的声明，则会出错。

*结束示例*
