

```vb
Private Sub btnCalc_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCalc.Click
    ' prompts the user to enter two sale amounts, then totals both amounts,
    ' then calls a function to calculate the bonus, then displays the bonus

    Dim strInputSale1 As String
    Dim strInputSale2 As String
    Dim decSale1 As Decimal
    Dim decSale2 As Decimal
    Dim decSum As Decimal
    Dim decBonus As Decimal

    strInputSale1 = InputBox("First sale amount", "Bonus Solution")
    strInputSale2 = InputBox("Second sale amount", "Bonus Solution")

    Decimal.TryParse(strInputSale1, decSale1)
    Decimal.TryParse(strInputSale2, decSale2)
    decSum = decSale1 + decSale2
    decBonus = GetBonus(decSum)
    lblBonus.Text = decBonus.ToString("C2")
End Sub
```

**图18-14**

- 图18-15显示了GetSum函数的代码。在btnCalc控件的Click事件过程中，将decSum = decSale1 + decSale2语句更改为decSum = GetSum(decSale1, decSale2)。

```vb
Private Function GetSum(ByVal decS1 As Decimal, _
    ByVal decS2 As Decimal) As Decimal
    ' totals the sales amounts

    Return decS1 + decS2
End Function
```

**图18-15**

## 19 一束阳光

学习完第19章后，你应该能够：

- 解释数组的用途
- 创建一维数组
- 在一维数组中存储数据
- 对一维数组的内容进行排序
- 搜索一维数组

### 让我们分组

自第7章以来，你编写的所有应用程序都使用了简单变量。**简单变量**（也称为**标量变量**）是一种与内存中任何其他变量都无关的变量。然而，有时你会遇到应用程序中某些变量彼此相关的情况。在这些情况下，将相关变量作为一个组来处理会更加容易和高效。你已经熟悉分组的概念。你衣橱里的衣服可能被分成了组，如外套、毛衣、衬衫、连衣裙等。以这种方式对衣服分组，可以让你轻松找到最喜欢的毛衣，因为你只需查看毛衣组，而不是整个衣橱。你可能也将CD（光盘）收藏按音乐类型或艺术家进行分组。如果你的收藏按艺术家分组，那么只需几秒钟就能找到所有的披头士CD，并且根据你拥有的披头士CD数量，之后只需很短时间就能找到特定的一张CD。当你将相关变量组合在一起时，这个组就被称为变量数组，或者更简洁地说，一个**数组**。你可以使用包含12个String变量的数组来存储一年12个月份的名称。或者，你可以使用包含50个Decimal变量的数组来存储每个州（共50个州）的销售额。商业应用程序中最常用的数组是一维数组和二维数组。本章以及下一章将介绍一维数组。二维数组将在第21章中介绍。

数组中的每个变量都具有相同的名称和数据类型。你使用一个唯一的编号（称为**下标**）来区分一维数组中的一个变量与另一个变量。下标表示变量在数组中的位置，由计算机在数组于内部内存中创建时分配。一维数组中的第一个变量分配到的下标为0，第二个为1，依此类推。通过数组名称和变量的下标（紧跟在数组名称后面的一对括号内）来引用数组中的每个变量。要引用名为strFriends的一维String数组中的第一个变量，可以使用strFriends(0)——读作“strFriends 下标零”。同样，要引用strFriends数组中的第三个变量，可以使用strFriends(2)。图19-1使用第7章中的存储箱插图展示了这一命名约定。图中包含的intAge、decRate和strMonth变量是标量变量。

![](img/cf88270932e011575089da06b940a1d9_438_0.png)

**图19-1：** 一维`strFriends`数组命名约定的图示

图19-2展示了在Visual Basic中声明过程级一维数组的两种语法版本。在每种语法中，*arrayName*是数组的名称，*dataType*是数组变量（称为元素）将要存储的数据类型。图中还包含了使用这两种语法版本的示例。

### 声明过程级一维数组

```vb
Syntax—Version 1

Dim arrayName(highestSubscript) As dataType

Syntax—Version 2

Dim arrayName() As dataType = {initialValues}
```

**图19-2：** 声明过程级一维数组的语法版本及示例

```vb
Example 1—Version 1's syntax
Dim intNumbers(5) As Integer
declares and initializes (to 0) a six-element Integer array named intNumbers

Example 2—Version 2's syntax
Dim strFriends() As String = {"Sue", "Bob", "John", "Mary"}
declares and initializes a four-element String array named strFriends
```

在语法版本1中，*highestSubscript*是一个整数，指定数组中的最大下标。创建数组时，它将包含比*highestSubscript*参数中指定的数量多一个元素；这是因为一维数组的第一个元素下标为0。因此，示例1中声明的*intNumbers*数组将包含六个元素，下标分别为0、1、2、3、4和5。使用语法版本1时，计算机会在数组创建时自动初始化数组中的每个元素。数值数组中的元素被初始化为数字0。而String数组中的元素则被初始化为空字符串。

与其让计算机使用默认值来初始化每个数组元素，你可以在声明数组时使用语法版本2来指定每个元素的初始值。为数组指定初始值通常称为**填充数组**。在语法的*initialValues*部分列出初始值，使用逗号分隔这些值，并将值列表放在大括号（{}）中。注意，语法版本2不包含*highestSubscript*参数；而是数组名称后面跟着一对空括号。计算机根据*initialValues*部分列出的值数量自动计算最大下标。因为一维数组的第一个下标是0，所以最大下标总是比*initialValues*部分列出的值数量少1。例如，Dim strFriends() As String = {"Sue", "Bob", "John", "Mary"}语句创建了一个四个元素的数组，下标分别为0、1、2和3。计算机将字符串"Sue"分配给*strFriends(0)*元素，将"Bob"分配给*strFriends(1)*元素，将"John"分配给*strFriends(2)*元素，将"Mary"分配给*strFriends(3)*元素，如图19-1中先前所示。

数组中的变量（元素）可以像任何其他变量一样使用：可以为它们赋值，在计算中使用它们，显示它们的内容等等。图19-3展示了执行这些任务的示例。

### 使用一维数组中的元素

**示例1**

```vb
Dim strCities() As String = {"Paris", "Rome", "Lisbon"}
strCities(0) = "Madrid"
```

将字符串“Madrid”赋值给strCities数组中的第一个元素，替换掉字符串“Paris”。

**示例2**

```vb
Dim intSalaries() As Integer = {25000, 35000, 50000, 23000}
intSalaries(3) = intSalaries(3) + 2000
```

将2000加到intSalaries数组中最后一个元素（23000）的内容上，然后将结果（25000）赋给该元素。

**示例3**

```vb
Dim decSales(10) As Decimal
Decimal.TryParse(txtSales.Text, decSales(2))
lblSales.Text = decSales(2).ToString("C2")
```

将TryParse方法返回的值赋给decSales数组中的第三个元素，然后在lblSales控件中显示该值（格式化为带美元符号和两位小数的形式）。

**图19-3：** 使用一维数组元素的示例

你在本章中编写的过程将演示一维数组在应用程序中的一些使用方式。在大多数应用程序中，数组存储的值来自计算机磁盘上的文件，并在声明数组后赋值给数组。然而，为了让你更容易理解代码及其结果，本章中的应用程序使用Dim语句将适当的值存储到数组中。

