

## 对常量使用命名约定

对常量使用与变量相同的命名约定是一种良好的实践。为公共常量添加前缀 `g`，为私有常量添加前缀 `m`，这样可以在使用点了解常量的作用域。此外，添加一个标识常量数据类型的后缀有助于保持常量名称的唯一性，并防止错误，例如在数学运算中使用字符串常量。

在图 25.5 中，常量名称除前缀外全部大写。没有要求常量必须使用大写。常量可以使用大写和小写字母的任意组合进行声明。有关命名变量和过程的规则同样适用于常量。然而，许多开发人员使用全大写约定：

```
dFinalPrice = dFullPrice * (1 - dDISCOUNT)
```

在前一行中，通过为变量使用适当的大小写命名方案和为常量使用大写命名方案，很容易看出什么是变量，什么是常量。

与变量不同，使用全局常量不会对代码的可维护性构成风险。常量值永远不会改变，因此无需追踪哪些过程使用了它们。与变量一样，将所有的全局作用域常量放在一个仅用于全局变量和常量的模块中是一种良好的实践。如果你在项目中看到一个名为 `modGlobals` 的模块，很可能开发人员正在使用该约定。

## 消除硬编码值

过程中使用的数字有时被称为魔法数字。这个术语并不意味着这些数字具有任何特殊能力，而是指阅读你代码的其他开发人员可能无法确定这些数字的来源。对于其他开发人员——或者对于几个月或几年后阅读你自己代码的你——这些数字似乎神奇地出现，没有解释。许多开发人员努力从代码中移除任何魔法数字，除了 0 和 1 以及分配给变量的数字。这使代码保持良好组织且易于维护。

在以下代码中，对图 25.5 中的过程进行了重写，魔法数字已被移除并替换为常量：

```
Sub DiscountedAmount2()

    Dim dFullPrice As Double
    Dim dFinalPrice As Double

    Const dDISCOUNT As Double = 0.15
    Const dDISCTHRESHOLD As Double = 5000
    Const sPROMPT As String = "The price is "

    dFullPrice = 8000

    If dFullPrice > dDISCTHRESHOLD Then
        dFinalPrice = dFullPrice * (1 - dDISCOUNT)
Else
    dFinalPrice = dFullPrice
End If

MsgBox sPROMPT & dFinalPrice

End Sub
```

如果你想更改显示的消息、折扣率或折扣阈值，你不必在代码中查找这些值的使用位置。过程中使用的所有重要值都可以在声明部分的 `Const` 语句中找到。更改 `Const` 语句中的值会在过程中任何使用它们的地方进行更改。`If dFullPrice > DISCTHRESHOLD Then` 这一行很容易被理解为全价与折扣阈值的比较。你可能会过度移除代码中的魔法数字。最佳实践是为任何使用多次的数字使用常量，并以第一次阅读代码的方式阅读你的代码，判断描述性注释名称是否比魔法数字更好。

## 使用数组

数组是一种特殊类型的变量。一个数组变量实际上保存了多份数据。与变量保留一块内存不同，数组保留了几块内存。数组的大小可以是固定的或动态的。使用动态数组，你可以在过程中增加或减少大小。本节中的代码可以在 Chapter25.accdb 的 modArrays 模块中找到。

### 固定数组

当你声明一个固定数组时，你在 `Dim` 语句中指定大小，并且该大小以后不能更改。声明固定数组的最简单方法是将上限索引放在变量名后的括号中：

```
Dim aCustomers(10) as Long
```

在此示例中，`aCustomers` 是一个可以容纳 11 个长整数的数组，可能来自 CustomerID 字段。为什么是 11？默认情况下，以这种方式声明的数组的下限为零。这意味着值可以存储在 `aCustomers(0)`、`aCustomers(1)`，一直到 `aCustomers(10)`。

声明固定数组的另一种方法是同时指定下限和上限索引。即使你打算使用默认值，在声明语句中包含下限也是一种良好的实践。使用 `To` 关键字指定数组的下限和上限索引：

```
Dim aCustomers(1 to 10) as Long
```

与前面的示例不同，此数组只有足够的空间容纳十个长整数。长整数使用 8 字节的内存，声明此数组会保留 80 字节来保存所有十个值。内存是在声明数组时使用的，因此即使你从未向数组分配任何值，其他任何内容也无法访问该内存。如果你遇到性能问题或应用程序使用大量内存，你可以查看数组，确保它们不会大于所需。然而，对于现代计算机，这里或那里的 80 字节可能不是问题。

向数组分配值就像向任何其他变量分配值一样，只是你必须指定要分配变量的索引。以下过程在循环中将浮点数（双精度）分配给数组：

```
Sub ArrayAssignment()

Dim aCustomers(1 To 5) As Double

aCustomers(1) = 0.2
aCustomers(2) = 24.6
aCustomers(3) = 7.1
aCustomers(4) = 99.9
aCustomers(5) = 14.7

End Sub
```

就像向变量分配值一样，数组名称位于等号左侧，值位于右侧。然而，与变量不同，每次分配都包括正在分配值的数组索引。

提示
VBA 包含一个指令，用于设置未指定下限的数组的默认下限。`Option Base` 指令确定默认下限。在模块顶部包含 `Option Base 1` 将强制下限为 1。同时声明了下限和上限的数组会忽略 `Option Base` 指令。`Option Base` 指令仅适用于声明它的模块。

从数组读取值看起来会很熟悉。就像从变量读取值一样，你只需使用变量名称。对于数组，你始终必须包含要读取的索引。以下过程在数组中存储五个随机数，将这些数字乘以 10，最后将数字打印到立即窗口：

```
Sub ArrayRandom()

Dim aRandom(1 To 5) As Double
Dim i As Long

For i = 1 To 5
    aRandom(i) = Rnd
Next i

For i = 1 To 5
    aRandom(i) = aRandom(i) * 10
Next i

For i = 1 To 5
    Debug.Print aRandom(i)
Next i

End Sub
```

因为数组索引每次增加一，`For...Next` 循环是访问数组中所有元素的常见方式。

我们目前看到的数组被称为*一维数组*。一维数组就像列表——它们有很多行，但只有一列。你也可以有二维数组。二维数组就像表格——它们有很多行和列。使用逗号分隔第一维的边界与第二维的边界来声明二维数组：

```
Dim aContact(1 To 10, 1 To 3) As String
```

`aContact` 数组有 30 个存储数据的位置。此数组可能用于存储十个联系人的三份数据。读写二维数组需要你指定两个维度的索引：

```
Sub TwoDArray()

    Dim aPotus(1 To 2, 1 To 3)
    Dim i As Long

    aPotus(1, 1) = "George"
    aPotus(1, 2) = "Washington"
    aPotus(1, 3) = "1789-1797"
    aPotus(2, 1) = "John"
    aPotus(2, 2) = "Adams"
    aPotus(2, 3) = "1797-1801"

    For i = 1 To 2
        Debug.Print aPotus(i, 1) & Space(1) & aPotus(i, 2) & Space(1) & _
            "was President in the years" & Space(1) & aPotus(i, 3)
    Next i

End Sub
```

> **注意**
>
> 你可以指定超过二维的维度，但这些数组可能变得非常难以管理。如果你需要存储那么多数据，请考虑使用用户定义类型或自定义类模块。

## 第六部分：Microsoft Access 编程基础

