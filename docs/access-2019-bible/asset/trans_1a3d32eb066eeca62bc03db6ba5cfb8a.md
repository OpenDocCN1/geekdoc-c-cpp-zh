

# 动态数组

动态数组在声明时不带任何索引，可以在过程执行期间稍后调整大小。除了没有索引号之外，它们的声明方式与固定数组相同：

```
Dim aProductIDs() As Long
```

使用动态数组声明时，在数组通过提供维度进行初始化之前，不会分配内存。在初始化之前，你不能向此数组赋值。要初始化动态数组，请使用 ReDim 关键字：

```
ReDim aProductIDs(1 to 100)
```

请注意，数据类型的 ReDim 语句中不包含。数据类型在数组声明时设置，并且不能更改。当你在运行时才知道需要的数组大小时，使用动态数组。在此示例中，数据库中所有打开窗体的名称都放入一个数组中。由于你无法知道哪些窗体将被打开，因此声明一个动态数组，并在过程执行时调整其大小：

```
Sub FormArray()

    Dim aForms() As String
    Dim frm As Form
    Dim lFrmCnt As Long
    Dim i As Long

    If Application.Forms.Count > 0 Then
        ReDim aForms(1 To Application.Forms.Count)

        For Each frm In Application.Forms
            lFrmCnt = lFrmCnt + 1
            aForms(lFrmCnt) = frm.Name
        Next frm

        For i = LBound(aForms) To UBound(aForms)
            Debug.Print aForms(i) & " is open."
        Next i
    End If

End Sub
```

Forms.Count 属性用于确定动态数组的大小。然后 For...Each 循环将每个打开窗体的名称放入数组的不同索引中。最后，过程遍历数组并将每个窗体的名称打印到立即窗口。

如果你在设计时就知道数组的大小，最好创建固定数组。如果你必须使用动态数组，通过确定需要的数组大小并发出 ReDim 语句来调整数组大小，你将获得最佳性能。然而，有时在开始填充数组之前你并不知道需要多少个元素。VBA 提供了 Preserve 关键字，可以在不丢失数组中已有的任何数据的情况下调整动态数组的大小。使用 ReDim 而不使用 Preserve 会调整数组大小，正如你所见，但数组会被重新初始化，任何现有数据都会丢失：

```
ReDim Preserve aCustomerIDs(1 to x) As Long
```

Preserve 关键字会创建一个新的、大小为新大小的数组，然后将所有数据从旧数组复制到新数组中。即使对于中等大小的数组，这也可能成为性能杀手。只有在没有其他选择时才使用 Preserve。

## 数组函数

VBA 提供了几个可与数组一起使用的有用函数。我们没有空间涵盖所有内容，但我们将介绍最常用和最有趣的函数。

### 边界函数

VBA 提供了两个函数 LBound 和 UBound 来确定数组的大小。LBound 返回下界，UBound 返回上界。这些函数在使用时循环遍历数组的所有元素时最有用：

```
For i = LBound(aContacts) To UBound(aContacts)
    Debug.Print aContacts(i)
Next i
```

如果 aContacts 声明为 Dim aContacts(1 to 5) As String，LBound 将返回 1，UBound 将返回 5。真正的益处在于当你将代码修订为 Dim aContacts(1 to 6) As String 时。如果你已在 For...Next 循环中硬编码边界，你将需要在两个地方更改上界。通过使用 LBound 和 UBound，你只需在 Dim 语句中进行更改。

对于二维数组，LBound 和 UBound 需要第二个参数指定维度。以下示例是遍历二维数组所有元素的典型方法：

```
For i = LBound(aBounds, 1) To UBound(aBounds, 1)
    For j = LBound(aBounds, 2) To UBound(aBounds, 2)
        Debug.Print aBounds(i, j)
    Next j
Next i
```

### Array 函数

Array 函数允许你通过在一行语句中提供数组的所有值来创建数组。Array 函数返回的数组称为变体数组——一个保存数组的 Variant 数据类型。要将 Array 函数的结果返回给变量，该变量必须声明为 Variant。Array 函数的语法为：

ParamArray 关键字表示可以有一个或多个参数，但数量在事先未知。Array 函数的参数由逗号分隔，每个参数成为数组的一个元素：

```
Sub ArrayFunction()

    Dim vaRates As Variant
    Dim i As Long

    vaRates = Array(0.05, 0.055, 0.06, 0.065, 0.07)

    For i = LBound(vaRates) To UBound(vaRates)
        Debug.Print vaRates(i)
    Next i

End Sub
```

在前面的示例中，vaRates 变量是一个包含五个元素的 Variant 数组（Array 函数中的五个数字）。由于变量是 Variant，因此你不需要事先指定数组的大小。Array 函数中的参数数量决定了大小。因此，下界和上界由 VBA 确定。默认下界为零，默认上界为 Array 函数中参数数量减一。对于前面的示例中的 vaRates，边界将为 0 到 4。Array 函数返回的数组的下界由模块顶部存在的 Option Base 指令确定，如果存在的话。

### NOTE

Array 函数返回一个变体数组——一个包含数组的 Variant。你也可以声明一个 Variant 数组。Variant 数组是一个数据类型为 Variant 的固定或动态数组。变体数组和 Variant 数组是两种不同的数组类型。

### Split 函数

Split 函数将文本转换为 Variant 数组。VBA 无法知道 Split 函数将返回的数组的大小，因此保存数组的变量必须声明为 Variant。Split 语法如下：

```
Split(string_expression, [delimiter], [limit], [compare])
```

第一个参数是你想要拆分为数组的字符串。delimiter 参数告诉 Split 函数在哪些字符上拆分字符串。limit 参数决定结果数组的大小。一旦数组达到定义的限制，Split 就会停止拆分字符串，即使存在更多分隔符：

```
Sub TheSplitFunction()

    Dim vaWords As Variant
    Dim i As Long

    vaWords = Split("Now is the title.", Space(1))

    For i = LBound(vaWords) To UBound(vaWords)
        Debug.Print vaWords(i)
    Next i

End Sub
```

vaWords 变量将是一个包含四个元素的变体数组：Now、is、the 和 time。分隔符——在本例中为单个空格——不包含在元素中。末尾的句号被包含在内，使最后一个元素为 time。（带句号）而不是 time（不带句号）。

### NOTE

几个 VBA 函数，包括 Split，具有一个 compare 参数，规定文本比较是否区分大小写。这始终是一个可选参数，在本节的示例中被省略。compare 参数的有效选择为 vbBinaryCompare（区分大小写）、vbDatabaseCompare（使用数据库的默认比较）和 vbTextCompare（不区分大小写）。

### Join 函数

Join 函数是 Split 的相反操作。Join 接受一个数组并返回一个字符串。Join 的语法为：

```
Join(source_array, [delimiter])
```

第一个参数是要转换为 String 的一维数组。source_array 可以是 VBA 可以转换为 String 的任何数据类型，甚至是数字和日期。delimiter 是要在数组元素之间插入的字符或字符：

```
Sub TheJoinFunction()

    Dim sResult As String
    Dim aWords(1 To 5) As String

    aWords(1) = "The"
    aWords(2) = "quick"
    aWords(3) = "brown"
    aWords(4) = "fox"
    aWords(5) = "jumped"

    sResult = Join(aWords, Space(1))

    Debug.Print sResult

End Sub
```

sResult 变量将包含字符串 The quick brown fox jumped。数组的每个元素都连接在一起，并在它们之间插入分隔符，在本例中为单个空格。

## 理解 Sub 和 Function

VBA 应用程序中的代码位于称为模块的容器中。正如你在第 24 章中学到的，模块存在于 Access 应用程序中的窗体和报表后面，以及独立模块中。模块本身包含许多过程、变量和常量声明，以及对 VBA 引擎的其他指令。

模块内的代码由过程组成。VBA 中有两种主要类型的过程：子程序或子过程（通常称为 subs）和函数。

过程的一般规则包括以下内容：

- 你必须在作用域内为过程提供唯一名称（参见本章前面“理解变量作用域和生命周期”）。虽然不是一个好主意——因为可能会混淆 VBA 引擎或与你的代码一起工作的其他人——但只要名称在每个过程的作用域内唯一，就有可能有多个同名过程。
- 你分配给过程的名称不能与 VBA 关键字相同。
- 过程和模块不能同名。这是一个命名约定非常有用的地方。如果你总是为模块名称加上 bas 或 mod 前缀，你就不会因为过程和模块同名而导致错误。
- 过程不能在其内部包含其他过程。但是，过程可以调用另一个过程，并在任何时候执行另一个过程中的代码。

由于过程作用域的规则，你不能有两个名为 MyProcedure 的公共过程，尽管你可以有两个名为 MyProcedure 的私有过程，或者一个名为 MyProcedure 的公共过程和一个名为 MyProcedure 的私有过程，但不能在同一个模块中。即使过程具有不同的作用域，使用相同的过程名称用于多个过程也是一个坏主意的原因应该是显而易见的。

以下各节涵盖了 VBA 过程的一些具体内容。规划和编写模块中的过程是使用 VBA 最耗时的部分，因此了解过程如何融入应用程序开发的整体方案非常重要。

子程序和函数都包含可以运行的代码行。当你运行子程序或函数时，你调用它。调用、运行和调用都是指执行（或运行）过程或函数内的语句（或代码行）。所有

