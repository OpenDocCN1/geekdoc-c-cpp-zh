

堆栈溢出情况。如果发生溢出，checked 运算符会通过异常强制执行溢出处理。如果在代码中使用 checked 运算符，CLR 将强制执行溢出检查，并在发生溢出时引发异常。如果发生溢出，unchecked 运算符不会引发异常。

## 说明

## checked 运算符

当由于数据类型（例如 int）的限制而导致数据丢失或接收到不可预测的值时，为了跳过这个垃圾值并生成“StackOverflow 异常”，会使用 checked 运算符。checked 关键字用于控制整型算术运算和转换的溢出检查上下文。根据以下形式，它可以用作运算符或语句。

checked 语句，

- 1. checked 块
- 2. 包含要在 checked 上下文中计算的表达式的语句块。
- 3. checked 运算符。
- 4. checked (expression)。
- 5. 要在 checked 上下文中计算的表达式。注意，表达式必须放在括号 () 中。

以下操作受溢出检查影响：

- 对整型使用以下预定义运算符的表达式：++ -- -（一元） + * /
- 整型之间的显式数值转换。

## unchecked 运算符

它与 checked 运算符相反，在实际场景中会得到垃圾值。它在 C# 中默认使用。如果要抑制溢出检查，可以使用 unchecked 运算符。在这种情况下，不会引发异常，但数据会丢失。

例如，byte 类型不能保存大于 255 的值。因此溢出位将被丢弃，byte 变量将保存零值。

unchecked 语句可以采用以下形式，

- 1. unchecked 块
- 2. 包含要在 unchecked 上下文中计算的表达式的语句块。
- 3. unchecked 运算符。
- 4. unchecked (expression)
- 5. 要在 unchecked 上下文中计算的表达式。注意，表达式必须放在括号 ( ) 中。

## 示例

```csharp
//Illustration of checked and unchecked

try{
checked
{
no1 += 15;
}
unchecked
{
n += 20;
}
}
catch(Exception ex)
{
Console.WriteLine(ex.Message.ToString());
}
```

## 两分题及答案

**Q.1** C# 中波浪号（~）是什么意思？

**答案：** ~ 运算符对其操作数执行按位求补运算，其效果是反转每一位。按位求补运算符已为 int、uint、long 和 ulong 预定义。此外，~ 符号还用于声明析构函数。

- **Q.2** 根据操作数数量，运算符有哪些类型？
  
  **答案：**
  - **一元运算符**：接受一个操作数来执行运算的运算符。
  - **二元运算符**：接受两个操作数来执行运算的运算符。
  - **三元运算符**：接受三个操作数来执行运算的运算符。

- **Q.3** C# 中的逻辑运算符有哪些？
  
  **答案：** 它们用于组合两个或多个条件/约束，或补充对所考虑的原始条件的求值。它们描述如下：
  
  - **逻辑与**：当所考虑的两个条件都满足时，'&&' 运算符返回 true。否则返回 false。例如，当 a 和 b 都为 true（即非零）时，a && b 返回 true。
  - **逻辑或**：当所考虑的条件中有一个（或两个）满足时，'||' 运算符返回 true。否则返回 false。例如，如果 a 或 b 中有一个为 true（即非零），a || b 返回 true。当然，当 a 和 b 都为 true 时，它也返回 true。
  - **逻辑非：** 如果所考虑的条件不满足，'!' 运算符返回 true。否则返回 false。例如，如果 a 为 false，即 a=0，则 !a 返回 true。

## Q.4 C# 中的按位“与”和“或”运算符是什么？

答案：

- 1. &（按位与）接受两个数作为操作数，并对两个数的每一位执行与运算。只有当两个位都为 1 时，与运算的结果才为 1。
- 2. |（按位或）接受两个数作为操作数，并对两个数的每一位执行或运算。只要两个位中任意一个为 1，或运算的结果就为 1。

## Q.5 C# 中的 sizeof 和 typeof 运算符是什么？

答案：

| sizeof() | 运算符返回数据类型的大小。 | 例如，sizeof(int) 返回 4。 |
| typeof() | 运算符返回类的类型。 | 例如，typeof(StreamReader); |

## Q.6 列出可重载的运算符。AU：2019 年 5 月

答案：C# 中可重载的运算符

| 运算符 | 重载可能性 |
| +, -, !, ~, ++, --, true, false | 这些一元运算符可以重载。 |
| +, -, *, /, %, &, \|, <<, >> | 这些二元运算符可以重载。 |
| ==, !=, >, <, <=, >= | 比较运算符可以重载。 |
| &&, \|\| | 条件逻辑运算符不能重载，但它们通过 & 和 \| 计算，而 & 和 \| 可以重载。 |

## 长答题

- Q.1 讨论 C# 中的各种运算符。（参见 3.1 节）
- Q.2 什么是优先级和结合性？（参见 3.4 节）
- Q.3 什么是 checked 和 unchecked 运算符？（参见 3.6 节）
- Q.4 C# 中的表达式是什么？（参见 3.5 节）
- Q.5 讨论 C# 中使用的各种标点符号。（参见 3.3 节）

## Q.6 详细说明运算符的类型。（参见 3.2 节）

AU：2017 年 12 月，16 分

## Q.7 描述 checked 和 unchecked 运算符的用途。（参见 3.6 节）

AU：2018 年 12 月，13 分

## Q.8 给定一个数组，编写一个 C# 程序将其向右旋转 k 个元素。设元素为 1、2、3、4、5、6、7、8、9、10。如果 k = 3，则向右旋转后变为 8、9、10、1、2、3、4、5、6、7。

AU：2019 年 12 月，13 分

答案：

```csharp
/* C# program to right rotate it by k elements where k is pivot*/
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace CodingAlgorithm
{
    public static class RotateArrayRight
    {
        //Rotate array to the right of a given pivot
        public static int[] Rotate(int[] x, int pivot)
        {
            if (pivot < 0 || x == null)
                throw new Exception("Invalid argument");

            pivot = pivot % x.Length;

            //Rotate first half
            x = RotateSub(x, 0, pivot - 1);

            //Rotate second half
            x = RotateSub(x, pivot, x.Length - 1);

            //Rotate all
            x = RotateSub(x, 0, x.Length - 1);
            return x;
        }

        private static int[] RotateSub(int[] x, int start, int end)
        {
            while (start < end)
            {
                int temp = x[start];
                x[start] = x[end];
                x[end] = temp;
                start++;
                end--;
            }
            return x;
        }
    }
}
```

## Q.9 举例说明 C# 中的各种算术运算符。

（参见 3.2 节）

AU：2019 年 12 月，7 分

## 笔记

## 第一单元

## 第 4 章

## 核心 C# —— 第三部分 —— 流控制与各种控制语句

教学大纲：流控制。

| 节号 | 主题名称 | 页码 |
|---|---|---|
| 4.1 | 流控制 | 4 - 2 |
| 4.2 | 选择语句 | 4 - 2 |
| 4.3 | 迭代语句 | 4 - 15 |
| 4.4 | 跳转语句 | 4 - 24 |
| 4.5 | 其他语句 | 4 - 30 |
|  | 两分题及答案 | 4 - 33 |
|  | 长答题 | 4 - 34 |

## 4.1 流控制

**概念**

控制语句用作控制已开发应用程序内处理过程的附加手段。

**说明**

| 控制语句 | 描述 |
|---|---|
| 选择语句 | 选择语句是一种控制语句，允许基于某种条件在程序中的两条或多条执行路径之间进行选择。这些语句包括 if、else、switch、case。 |
| 迭代语句 | 迭代语句使用户能够重复执行同一组语句，直到满足特定条件。这些语句包括 for、while、do-while 和 for each 循环。 |
| 跳转语句 | 跳转语句使用户能够基于任何条件或无任何条件跳转到代码的另一部分。这些语句包括 break、continue、goto、return 和 throw 语句。 |
| 其他语句 | 其他语句指用于特殊目的的特定语句。这些包括块语句、空语句、using 语句。 |

## 4.2 选择语句

**概念**

- 1. 选择语句是一种控制语句，允许基于某种条件在程序中的两条或多条执行路径之间进行选择。

**说明**

- 2. C# 包括单向、双向和 n 向（多重）选择器。
  - 2.1) 不带 else 的 if 语句是单向选择器。
  - 2.2) if..else 语句是双向选择器。
  - 2.3) if..elseif..else、嵌套 if 和 switch 语句是 n 向选择器。

