
```
Public Structure Product
Dim DescriptionString As String
Dim ProductNumberString As String
Dim QuantityInteger As Integer
Dim PriceDecimal As Decimal
End Structure

Structure SalesDetail
Dim SaleDecimal() As Decimal
End Structure
```

默认情况下，结构是 Public 的。如果在结构内部包含数组，则不能指定元素个数。必须在代码中使用 ReDim 语句来声明元素个数。

在很多方面，结构类似于定义一个新的数据类型。

## 基于结构声明变量

创建结构后，就可以像声明其他数据类型一样声明该结构的变量。

```
Dim OfficeEmployee As Employee
Dim WarehouseEmployee As Employee
Dim WidgetProduct As Product
Dim InventoryProduct(100) As Product
Dim HousewaresSalesDetail As SalesDetail
Dim HomeFurnishingsSalesDetail As SalesDetail
```

## 访问结构变量中的元素

在声明为结构的变量中，每个数据字段称为该结构的一个元素。要访问元素，请使用与对象类似的点表示法：指定 变量.元素。

```
OfficeEmployee.LastNameString
OfficeEmployee.HireDate
WarehouseEmployee.LastNameString
WidgetProduct.DescriptionString
WidgetProduct.QuantityInteger
WidgetProduct.PriceDecimal
InventoryProduct(IndexInteger).DescriptionString
InventoryProduct(IndexInteger).QuantityInteger
InventoryProduct(IndexInteger).PriceDecimal
```

注意前面示例中索引的使用。每个示例都取自前面的 Structure 和 Dim 语句。不是数组的变量（如 WidgetProduct）不需要索引。然而，对于声明为包含 101 个元素的数组的 InventoryProduct，您不仅必须指定 InventoryProduct 项，还必须指定结构内的元素。

## 在结构中包含数组

要在结构中声明数组（请参阅前面显示的 SalesDetail 结构），请在过程内部使用 ReDim 语句来指定数组的大小。

```
' Module-level declarations.
Structure SalesDetail
    Dim SaleDecimal() As Decimal
End Structure

Dim HousewaresSalesDetail As SalesDetail
' Inside a procedure (such as the Form_Load):
' Establish the number of elements in the array.
ReDim HousewaresSalesDetail.SaleDecimal(6)

' In processing:
HousewaresSalesDetail.SaleDecimal(DayIndexInteger) = TodaysSalesDecimal
```

## 异常处理

运行时错误称为异常。当您尝试使用转换方法（如 Single.Parse 或 Decimal.Parse）而用户输入了非数字数据或使文本框留空时，可能会发生异常。当操作失败时，CLR 会引发异常，您可以使用 .NET 的结构化异常处理来捕获和处理该异常。

### Try/Catch 块

要捕获异常，请将可能导致错误的任何语句括在 Try/Catch 块中。如果在执行 Try 块中的语句时发生异常，程序控制将转移到 Catch 块；如果包含 Finally 语句，则无论是否发生异常，该部分中的代码都会最后执行。

```
Try    ' Statements that may cause error.
Catch [VariableName As ExceptionType]
    ' Statements for action when exception occurs.
[Finally
    ' Statements that always execute before exit of Try block]
End Try
```

```
Try
    QuantityInteger = Integer.Parse(QuantityTextBox.Text)
    QuantityLabel.Text = QuantityInteger.ToString()
Catch
    MessageLabel.Text = "Error in input data."
End Try
```

前面示例中出现的 Catch 将捕获任何异常。您还可以指定要捕获的异常类型，甚至可以包含多个 Catch 语句，每个语句捕获不同类型的异常。要指定要捕获的特定异常类型，请使用预定义的异常类之一，这些异常类都基于或派生自 System.Exception 类。选择“调试 / 异常”可查看系统异常类的完整列表。

要捕获无法转换为数字的错误输入数据，请编写以下 Catch 语句：

```
Catch Err As InvalidCastException
    MessageLabel.Text = "Error in input data."
```

### Exception 类

每个异常都是 Exception 类的一个实例。该类的属性允许您确定错误的代码源、错误类型和原因。Message 属性包含有关错误的文本消息，Source 属性包含导致错误的对象的名称。

您可以通过指定 Exception 对象的 Message 属性来包含与该异常类型关联的文本消息，该对象由您在 Catch 语句上命名的变量来声明。

```
Catch AnErr As InvalidCastException
    MessageLabel.Text = "Error in input data. " & AnErr.Message
```

### 处理多个异常

包含多个 Catch 块（处理程序）以捕获不同类型的错误。当发生异常时，Catch 语句将按顺序检查。将使用第一个具有匹配异常类型的 Catch。

```
Catch AnErr As InvalidCastException
    ' Statements for nonnumeric data.
Catch AnErr As ArithmeticException
    ' Statements for calculation problem.
Catch AnErr As Exception
    ' Statements for any other exception.
```

最后一个 Catch 将处理与前两个异常类型不匹配的任何异常。请注意，多个 Catch 语句可以使用相同的变量名；您在 Catch 语句上声明的变量具有块级作用域，因此仅在该单个 Catch 内部可见。

### 使用 TryParse 捕获错误

捕获异常是一项非常耗费资源的操作。更高效的方法是使用 TryParse 方法执行转换。TryParse 会尝试转换，如果成功则返回布尔值 true，如果失败则返回 false。转换后的值可在方法的一个参数中获取。与 Parse 方法一样，TryParse 仅处理字符串数据。

```
' Convert input to integer.
Dim ConvertedInteger As Integer
If Integer.TryParse(NumberTextBox.Text, ConvertedInteger) Then
    ' Successful conversion; perform calculation with ConvertedInteger.
Else
    ' Unsuccessful conversion.
    MessageBox.Show("Invalid input data.")
End If
```

Integer.TryParse 方法返回 true，并将转换后的值放入第二个参数（前面示例中的 ConvertedInteger）。如果转换不成功，该方法返回 false，并且 ConvertedInteger 参数中保存的值为零。

| 方法 | 返回类型 | 示例 |
|---|---|---|
| Short.TryParse(String, VariableShort) | Short | If Short.TryParse(NumTextBox.Text, VarShort) Then |
| Integer.TryParse(String, VariableInteger) | Integer | If Integer.TryParse(NumTextBox.Text, VarInteger) Then |
| Long.TryParse(String, VariableLong) | Long | If Long.TryParse(NumTextBox.Text, VarLong) Then |
| Decimal.TryParse(String, VariableDecimal) | Decimal | If Decimal.TryParse(NumTextBox.Text, VarDecimal) Then |
| Single.TryParse(String, VariableSingle) | Single | If Single.TryParse(NumTextBox.Text, VarSingle) Then |
| Double.TryParse(String, VariableDouble) | Double | If Double.TryParse(NumTextBox.Text, VarDouble) Then |
| DateTime.TryParse(String, VariableDateTime) 或 Date.TryParse(String, VariableDate) | Date | If DateTime.TryParse(DateTextBox.Text, VarDate) Then<br>If Date.TryParse(DateTextBox.Text, VarDate) Then |
| Boolean.TryParse(String, VariableBoolean) | Boolean | If Boolean.TryParse(TrueFalseTextBox.Text, VarBoolean) Then |

## 控制结构

使用控制结构可以修改程序中逻辑流的顺序。每个控制结构都会测试表达式以确定要采用的路径。

### 布尔表达式

您可以测试布尔表达式的值为真还是假。表达式可以基于布尔变量的值，也可以基于两个或多个值的关系。您可以使用六个关系运算符和逻辑运算符来构成表达式。

| 关系运算符 | 逻辑运算符 |
|---|---|
| >（大于） | And |
| <（小于） | Or |
| =（等于） | Not |
| >=（大于或等于） | AndAlso |
| <=（小于或等于） | OrElse |
| <>（不等于） |  |
