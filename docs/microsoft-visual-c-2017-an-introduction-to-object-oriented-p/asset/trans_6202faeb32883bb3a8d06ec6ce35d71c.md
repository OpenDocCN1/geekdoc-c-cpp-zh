
# 将数组值传递给方法

将数组元素传递给方法与将整个数组传递给方法需要不同的方法。

## 向方法传递单个数组元素

在“使用数组”章节中，你学习了可以声明一个数组来创建元素列表，并且可以像使用任何相同类型的单个变量一样，使用数组中的任何单个元素。假设你如下所示声明了一个整数型数组：

```
int[] someNums = new int[12];
```

随后，你可以输出 `someNums[0]` 或为 `someNums[1]` 加 1，就像处理任何整数一样。同样地，你可以完全以传递变量的方式，将单个数组元素传递给方法。

考虑图 7-17 所示的程序。该程序创建并使用了一个包含四个整数的数组。图 7-18 显示了程序的执行情况。

```c
using static System.Console;
class PassArrayElement {
    static void Main() {
        int[] someNums = {10, 12, 22, 35};
        int x;
        Write("\nBeginning of Main() method... ");
        for(x = 0; x < someNums.Length; ++x)
            Write("{0,}", someNums[x]);
        WriteLine();
        for(x = 0; x < someNums.Length; ++x)
            MethodGetsOneInt(someNums[x]);
        Write("At end of Main() method....... ");
        Write("{0,}", someNums[x]);
    }
    private static void MethodGetsOneInt(int oneVal) {
        Write("In MethodGetsOneInt() {0}", oneVal);
        oneVal = 999;
        WriteLine("After change {0}", oneVal);
    }
}
```

**图 7-17** PassArrayElement 程序

# 第 7 章 使用方法

| 在 Main() 方法开始时... | 10 | 12 | 22 | 35 |
|---|---|---|---|---|
| 在 MethodGetsOneInt(1) 中 | 10 | After change 999 | | |
| 在 MethodGetsOneInt(1) 中 | 12 | After change 999 | | |
| 在 MethodGetsOneInt(2) 中 | 22 | After change 999 | | |
| 在 MethodGetsOneInt(2) 中 | 35 | After change 999 | | |
| 在 Main() 方法结束时....... | 10 | 12 | 22 | 35 |

**图 7-18** PassArrayElement 程序的输出

如你在图 7-18 所示，程序显示了四个原始值，并将每个值传递给 `MethodGetsOneInt(1)` 方法，在该方法中值被显示并更改为 999。在方法执行四次后，`Main()` 方法验证这些值没有因为 `MethodGetsOneInt(1)` 内部赋值而改变。`oneVal` 变量是 `MethodGetsOneInt(1)` 方法的局部变量；因此，传入方法的更改不是永久的，也不会反映在 `Main()` 方法声明的数组中。每次执行 `MethodGetsOneInt(1)` 方法，其参数 `oneVal` 只持有传入方法的数组元素的副本，且 `oneVal` 变量只在 `MethodGetsOneInt(1)` 执行期间存在。

## 向方法传递数组

与其向方法传递单个元素，不如你可以传递整个数组。你通过在方法参数列表的数据类型周围加上方括号来指明该参数必须是一个数组。当你将数组传递给方法时，你在方法内部对元素所做的更改将反映在发送给方法的原始数组中。内存地址也被称为**引用**。数组像对象一样，但与 `double` 和 `int` 等内置类型不同，它是**按引用传递**的。当一个简单的 `int` 传递给方法时，它是**按值传递**的。然而，方法接收的是新内存地址处的值副本。相反，当数组传递给方法时，方法接收的是数组的实际内存地址，并可以访问数组元素中的实际值。你已经看到方法可以修改传递给它们的数组。当你在第 6 章中使用 `Sort()` 和 `Reverse()` 方法时，你看到它们改变了其数组参数的内容。

图 7-19 所示的程序创建了一个包含四个整数的数组。对于显示的整数，数组在阴影语句中被传递给方法 `MethodGetsArray()`。在方法头中，通过在数据类型后使用方括号，将参数声明为数组。通过该方法，输出了数字，显示它们在进入方法时从 `Main()` 返回了它们的值，但随后每个数字都被赋值为 888。尽管 `GetsArray()` 是一个 `void` 方法（意味着没有向 `Main()` 方法返回任何内容），当程序在图 7-20 中第二次显示数组时，由于数组是按引用传递的，`MethodGetsArray()` 方法“知道”在 `Main()` 中声明的数组，并直接对 `Main()` 方法声明的原始数组进行更改。

```csharp
using static System.Console;
class PassEntireArray
{
    static void Main()
    {
        int[] someNums = {10, 12, 22, 35};
        int x;
        Write("\nBeginning of Main() method... ");
        for(x = 0; x < someNums.Length; ++x)
            Write("{0,}", someNums[x]);
        WriteLine();
        MethodGetsArray(someNums);
        Write("At end of Main() method....... ");
        Write("{0,}", someNums[x]);
    }

    private static void MethodGetsArray(int[] vals)
    {
        Write("\nBeginning of Main() method... ");
        for(int i = 0; i < vals.Length; ++i)
        {
            Write("In MethodGetsArray() {0}", vals[i]);
            vals[i] = 888;
            WriteLine("After change {0}", vals[i]);
        }
    }
}
```

**图 7-19** PassEntireArray 程序

| 在 Main() 方法开始时... | 10 | 12 | 22 | 35 |
|---|---|---|---|---|
| 在 MethodGetsArray() 中 | 10 | After change 888 | | |
| 在 MethodGetsArray() 中 | 12 | After change 888 | | |
| 在 MethodGetsArray() 中 | 22 | After change 888 | | |
| 在 MethodGetsArray() 中 | 35 | After change 888 | | |
| 在 Main() 方法结束时....... | 10 | 12 | 22 | 35 |

**图 7-20** PassEntireArray 程序的输出

