

## 类型推断

在此时，你可能会疑惑，为什么在编写列表 1-13 所示的 F# 代码时不需要指定类型信息。你可能会对 F# 是一种脚本语言或动态语言产生错误的印象，这些语言通常不强调类型。实际上，事实并非如此；F# 是一种强类型语言。F# 通过一种名为“类型推断”（type inference）的功能提供了省略定义的能力，该功能根据代码的使用方式来识别类型信息。列表 1-77 显示了函数 f 及其在 F# 中的定义方式。s 的类型可以通过调用 `System.String.IsNullOrEmpty` 来确定，该方法接收一个字符串并返回一个布尔值。这就是 F# 识别类型信息的方式。

列表 1-77 一个类型推断示例

```
> let f s = System.String.IsNullOrEmpty s;

val f : string -> bool
```

类型推断效果非常好，但有时需要帮助，例如在处理重载方法时，因为重载方法通过参数类型来区分彼此。例如，在列表 1-78 中，`LastIndexOf` 方法可以接受 `char` 和 `string` 作为输入。你可能没有预期编译器能读懂你的心思，对吧？因为变量 `ch` 可以是 `string` 类型或 `char` 类型，你必须为变量 `ch` 指定类型。如果你不告诉参数类型，F# 就无法确定应该使用哪一个重载方法。正确的代码在列表 1-79 中。

列表 1-78 使用重载方法时的类型推断

```
> let f ch = "abc".IndexOf(ch);

let f ch = "abc".IndexOf(ch);
~~~~~~~~~~~~~~~~~~~
```

stdin(10,12): error F50041: 根据此程序点之前的类型信息，无法确定方法 'IndexOf' 的唯一重载。。可能需要类型注解。候选者：System.String.IndexOf(value: char) : int, System.String.IndexOf(value: string) : int

列表 1-79 指定类型后的类型推断

```
> let f (ch:string) = "abc".IndexOf(ch);

val f : string -> int
```

了解类型推断过程是如何运作很有帮助。它是从上到下、从左到右执行的。它不是从程序的 `main` 函数开始的。因此，列表 1-80 中的代码无法编译。无法从 `str.Length` 推断出字符串类型，因为 .NET 中有许多具有 `Length` 属性的类型。

## 列表 1-80 从上到下的类型推断

```
let f str = str.Length // 无法确定 str 的类型

[EntryPoint]
let main argv =
    let result = f "abc"
    0 // 返回一个整数退出代码
```

![](img/63aaf94e2830ab8ce5946beef77_0.png)

注意：最佳实践是边写代码边让 F# 编译器为你推断出类型。如果出现错误，可以通过提供类型信息来轻松解决。这些错误在下方的代码中所示。类型推断是从上到下处理的，这与代码执行的顺序不同。程序入口点通常位于文件末尾，在入口点装饰变量是没有帮助的。

IntelliSense 使用不同的方式为用户提供类型信息。有时 IntelliSense 会显示类型信息，但代码将无法编译。下面是一个简单的代码示例。尽管 IntelliSense 显示了 `str` 的 `System.String` 类型，但第二行的类型是未知的。

```
let f str =
    let len = str.Length // str 类型未知
    str + "aa"
```

类型推断趋势使代码更加通用。这种简单性不仅节省了你的时间，还通过使代码更加直观友好提升了可读性，正如列表 1-81 所示。

## 列表 81 F# 与 C# 并列

```
F# 代码
let printAll aSeq =
    for n in aSeq do
        <function call>
```

```C# 等效代码
public static void printAll<a>(IEnumerable<a> aSeq)
{
    foreach (a in aSeq)
}
```

将元组传递给 C# 函数看起来很良好，直到你有一个需要 `out` 参数的函数。元组没有提供说明某个值是 `ref` 还是 `out` 的方法，但元组有助于解决这个问题。

```cs
public int SharpFunction(int k, out int n)
```

函数实际上向调用者返回了两个值。因此解决方案是声明一个元组来持有返回的值：

```
let returnValue, n = SharpFunction(1)
```

这种方法适用于外部声明的方法。对外部声明方法的调用需要 `&` 运算符。列表 1-84 显示了如何在外部函数中处理 `out` 参数。

## 列表 84 使用 F# 暴露一个带有 out 参数的 C# 外部函数

```cs
C# 函数定义
[DllImport("MyDLL.dll")]
public static extern int SharpFunction(IntPtr inRef, out IntPtrPtr);
```

在 F# FSI 中定义并调用函数：

```
[System.Runtime.InteropServices.DllImport("something.dll")]
extern int SharpFunction(IntPtr inRef, out IntPtrPtr);
let mutable myOutPtr
let n = SharpFunction(0, myOutPtr)
```

如果你想向 C# 项目暴露一个 `out` 参数，你需要一个名为 `System.Runtime.InteropServices.Out` 的特殊属性。在 F# 中为参数装饰此属性，C# 调用者就可以看到该参数旨在作为 `out` 参数。参见列表 1-85 中的示例。`byref` 关键字用于将变量声明为引用类型传递。

## 列表 1-85 使用 F# 向 C# 暴露一个 out 参数

```
let f ([System.Runtime.InteropServices.Out]a: byref) = a <- 9
```

我已经涵盖了 `out` 参数，现在让我们关注注意力到 `ref`。处理 C# 的 `ref` 定义是很容易的。列表 1-86 显示了如何在 F# 中处理 `ref` 参数。示例代码中有一个 `byref` 关键字，我将在第 6 章“其他独特特性”中介绍它。现在，把它 true为一个引用变量。

## 列表 1-86 使用 F# 调用一个带有 ref 参数的 C# 函数

```cs
C 函数定义
namespace CSharp
{
    public class Chapter1Class
    {
        public static int ParameterFunction(int inValue, ref int refValue)
        {
            refValue += 3;
            return inValue + 7;
        }

        public static void ReturnSample(out int x)
        {
            x = 8;
        }
    }
}
```

```fs
F# 调用 C# 函数的代码
// 声明可变变量
let mutableValue = 2

// 声明引用单元
let refValue = ref 2

// 将可变变量传入函数
let refFunction = CSharp.Chapter1Class.ParameterFunction(1, &mutableValue)

// 将引用单元传入函数
let refFunction2 = CSharp.Chapter1Class.ParameterFunction(1, refValue)
```

## 互操作与函数参数

一些 F# 用户开始使用 F# 作为库编写工具。由于 F# 是一种 .NET 语言，与其他语言的互操作是无缝的。向 F# 项目添加引用与向 C# 项目添加引用的完全相同。唯一需要解释的是：

1. 使用 `#r` 引用 DLL。
2. 打开命名空间。

列表 1-83 显示了如何引用 `System.Core`、打开 `Collections.Generic` 命名空间并使用 `HashSet<>`。

## 列表 83 在 F# 脚本文件或 FSI 中创建 HashSet

```fs
#r "System.Core"
open System.Collections.Generic
let a = HashSet<int>()
```

注意：F# 不需要 `new` 来实例化对象。然而，当类实现 `IDisposable` 接口时，建议使用 `new` 关键字。与 C# 相比，在 F# 中调用 .NET 方法的方法区别不大。以下是使用 .NET 方法将字符串转换为整数：

```
System.Convert.ToInt32("2")
```

