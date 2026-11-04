
创建固定大小的缓冲区时，使用 fixed 的以下形式：

```
fixed type buf-name[size];
```

这里，type 是数组的数据类型；buf-name 是固定大小缓冲区的名称；size 是缓冲区中的元素数量。固定大小的缓冲区只能在 struct 内指定。

为了理解固定大小缓冲区可能有用的原因，请考虑这样一种情况：你想要将银行账户信息传递给用 C++ 编写的账户管理程序。此外，假设每个账户记录使用以下组织方式：

| 名称 | 8 位 ASCII 字符字符串，长 80 字节 |
| 余额 | 一个 double，长 8 字节 |
| ID | 一个 long，长 8 字节 |

在 C++ 中，每个结构本身包含 Name 数组。这与 C# 不同，C# 通常只存储对数组的引用。因此，在 C# struct 中表示此数据需要使用固定大小的缓冲区，如下所示：

// Use a fixed-size buffer.
unsafe struct FixedBankRecord {
    public fixed byte Name[80]; // create a fixed-size buffer
    public double Balance;
    public long ID;
}
```

通过为 Name 使用固定大小的缓冲区，FixedBankRecord 的每个实例都将包含 Name 数组的全部 80 个字节，这就是 C++ struct 的组织方式。因此，FixedBankRecord 的总体大小为 96，这是其成员的总和。以下程序演示了这一事实：

```
// Demonstrate a fixed-size buffer.
using System;
// Create a fixed-size buffer.
unsafe struct FixedBankRecord {
    public fixed byte Name[80]; // create a fixed-size buffer
    public double Balance;
    public long ID;
}
class FixedSizeBuffer {
    // Mark Main as unsafe.
    unsafe static void Main() {
        Console.WriteLine("Size of FixedBankRecord is " +
            sizeof(FixedBankRecord));
    }
}
```

输出如下所示：

```
Size of FixedBankRecord is 96
```

声明可空类型的第二种方式更简短，并且更常用。只需在类型名称后加上 ?。例如，下面显示了声明可空 int 和 bool 类型的更常见方式：

```
int? count;
bool? done;
```

使用可空类型时，你经常会看到像这样创建的可空对象：

```
int? count = null;
```

这显式地将 count 初始化为 null。这满足了变量在使用前必须赋值的约束。在这种情况下，该值 simply 意味着未定义。

你可以以正常方式为可空变量赋值，因为从基础类型到可空类型的转换是预定义的。例如，这将值 100 分配给 count。

```
count = 100;
```

有两种方法可以确定可空类型变量是否为空或包含值。首先，可以将其值与 null 进行比较。例如，使用前述语句声明的 count，下面的代码确定它是否有值：

```
if(count != null) // has a value
```

如果 count 不为 null，则它包含一个值。

确定可空类型是否包含值的第二种方法是使用 Nullable<T> 定义的 HasValue 只读属性。如下所示：

```
bool HasValue
```

HasValue 如果在其上调用的实例包含值，则返回 true。否则返回 false。使用 HasValue 属性，下面是确定可空对象 count 是否具有值的第二种方法：

```
if(count.HasValue) // has a value
```

假设可空对象包含一个值，可以使用 Nullable<T> 定义的 Value 只读属性获取其值，如下所示：

```
T Value
```

它返回在其上调用的可空实例的值。如果尝试从 null 变量获取值，将抛出 System.InvalidOperationException。也可以通过将其强制转换为基础类型来获取可空实例的值。

以下程序将各部分组合在一起并演示处理可空类型的基本机制：

// Demonstrate a nullable type.

using System;

class NullableDemo {
    static void Main() {
        int? count = null;
        if(count.HasValue)
            Console.WriteLine("count has this value: " + count.Value);
        else
            Console.WriteLine("count has no value");

        count = 100;

        if(count.HasValue)
            Console.WriteLine("count has this value: " + count.Value);
        else
            Console.WriteLine("count has no value");
    }
}
```

输出如下所示：

```
count has no value
count has this value: 100
```

## 可空对象在表达式中

可空对象可用于对其基础类型有效的表达式中。此外，可以在同一表达式中混合使用可空对象和不可空对象。这是因为存在从基础类型到可空类型的预定义转换。当在操作中混合使用不可空类型和可空类型时，结果是一个可空值。

以下程序说明了在表达式中使用可空类型的用法：

// Use nullable objects in expressions.

using System;

class NullableDemo {
    static void Main() {
        int? count = null;
        int? result = null;

        int incr = 10; // notice that incr is a non-nullable type

        // result contains null, because count is null.
        result = count + incr;

        if(result.HasValue)
            Console.WriteLine("result has this value: " + result.Value);
        else
            Console.WriteLine("result has no value");

        // Now, count is given a value and result will contain a value.
        count = 100;
        result = count + incr;
        if(result.HasValue)
            Console.WriteLine("result has this value: " + result.Value);
        else
            Console.WriteLine("result has no value");
    }
}
```

输出如下所示：

```
result has no value
result has this value: 110
```

## ?? 运算符

如果尝试使用强制转换将可空对象转换为其基础类型，当可空对象包含 null 值时，将抛出 System.InvalidOperationException。例如，当你使用强制转换将可空对象的值分配给其基础类型的变量时，就会发生这种情况。你可以通过使用 ?? 运算符来避免抛出此异常的可能性，该运算符称为空合并运算符。它允许你指定一个默认值，当可空对象包含 null 时将使用该默认值。它还消除了对强制转换的需求。

?? 运算符的一般形式如下：

```
nullable-object ?? default-value
```

如果 nullable-object 包含一个值，则 ?? 的值就是该值。否则，?? 操作的值为 default-value。

例如，在下面的代码中 balance 为 null。这导致 currentBalance 被赋值为 0.0，并且不会抛出异常。

```
double? balance = null;
double currentBalance;

currentBalance = balance ?? 0.0;
```

在下一个序列中，balance 被赋值为 123.75：

```
double? balance = 123.75;
double currentBalance;

currentBalance = balance ?? 0.0;
```

现在，currentBalance 将包含 balance 的值，即 123.75。

还有一点：?? 的右手表达式仅在左手表达式不包含值时才会被求值。以下程序演示了这一事实：

// Using ??
using System;
class NullableDemo2 {
    // Return a zero balance.
    static double GetZeroBal() {
        Console.WriteLine("In GetZeroBal().");
        return 0.0;
    }

    static void Main() {
        double? balance = 123.75;
        double currentBalance;

        // Here, GetZeroBal() is not called because balance
        // contains a value.
        currentBalance = balance ?? GetZeroBal();
        Console.WriteLine(currentBalance);
    }
}
```

在此程序中，由于 balance 包含一个值，因此不会调用方法 GetZeroBal()。如上所述，当 ?? 的左手表达式包含值时，右手表达式不会被求值。

## 可空对象与关系运算符和逻辑运算符

可空对象可以在关系表达式中使用，就像其对应的不可空类型一样。然而，还有一条额外的规则适用。当使用 <、>、<= 或 >= 运算符比较两个可空对象时，如果任一对象为 null，则结果为 false。例如，考虑以下序列：

```
byte? lower = 16;
byte? upper = null;

// Here, lower is defined, but upper isn't.
if(lower < upper) // false
```

这里，小于测试的结果为 false。然而，有点违反直觉，逆向比较也是如此：

```
if(lower > upper) // .. also false!
```

因此，当用于比较的可空对象之一（或两者）为 null 时，该比较的结果始终为 false。因此，null 不参与排序关系。

然而，你可以使用 == 或 != 运算符测试可空对象是否包含 null。例如，这是一个有效的测试，将导致 true 结果：

```
if(upper == null) // ...
```

当逻辑表达式涉及两个 bool? 对象时，该表达式的结果将是三个值之一：true、false 或 null（未定义）。以下是添加到适用于 bool? 的 & 和 | 运算符的真值表中的条目。
