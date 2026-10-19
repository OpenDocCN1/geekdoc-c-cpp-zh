

## Visual Basic 示例：笨拙地复制一组数据项

```
newName = oldName
newAddress = oldAddress
newPhone = oldPhone
newSsn = oldSsn
newGender = oldGender
newSalary = oldSalary
```

每次你想要传输员工的信息时，你都必须使用这一整组语句。如果你以后添加一个新的员工信息项——例如，numWithholdings——你必须找到所有包含赋值块的地方并添加一个 newNumWithholdings = oldNumWithholdings 的赋值。

想象一下在两个员工之间交换数据会有多糟糕。你不需要想象——这里就是：

![](img/649c8eee28c38ca1e062691e45dc9883_357_0.png)

## Visual Basic 示例：以困难的方式交换两组数据

```
* swap new and old employee data
previousOldName = oldName
previousOldAddress = oldAddress
previousOldPhone = oldPhone
previousOldSsn = oldSsn
previousOldGender = oldGender
previousOldSalary = oldSalary

oldName = newName
oldAddress = newAddress
oldPhone = newPhone
oldSsn = newSsn
oldGender = newGender
oldSalary = newSalary

newName = previousOldName
newAddress = previousOldAddress
newPhone = previousOldPhone
newSsn = previousOldSsn
newGender = previousOldGender
newSalary = previousOldSalary
```

更简单的方法是声明一个结构化变量：

## Visual Basic 示例：声明结构

```
Structure Employee
    name As String
    address As String
    phone As String
    ssn As String
    gender As String
    salary As Long
```

```
End Structure
Dim newEmployee As Employee
Dim oldEmployee As Employee
Dim previousOldEmployee As Employee
```

现在你可以用三条语句交换旧员工和新员工结构中的所有元素：

```
Visual Basic Example of an Easier Way to Swap Two Groups of Data
previousOldEmployee = oldEmployee
oldEmployee = newEmployee
newEmployee = previousOldEmployee
```

如果你想添加一个 numWithholdings 这样的字段，你只需将其添加到 Structure 声明中。上述三条语句以及程序中任何类似的语句都不需要修改。C++ 和其他语言也有类似的功能。

> Cross-Reference For details on how much data to share between routines, see "Keep Coupling Loose" in Section 5.3.

## 使用结构简化参数列表

你可以通过使用结构化变量来简化例程参数列表。该技术与刚才展示的类似。与其单独传递每个所需元素，你可以将相关元素分组到一个结构中，并将整个 enchilada 作为一个组结构传递。以下是没有结构笨拙地传递一组相关参数的示例：

```
Visual Basic Example of a Clumsy Routine Call Without a Structure
HardWayRoutine( name, address, phone, ssn, gender, salary )
```

而这是一个使用包含第一个参数列表元素的结构化变量优雅地调用例程的示例：

```
Visual Basic Example of an Elegant Routine Call with a Structure
EasyWayRoutine( employee )
```

如果你想在第一种调用中添加 numWithholdings，你必须在代码中查找并更改对 HardWayRoutine() 的每次调用。如果你向 Employee 添加一个 numWithholdings 元素，你完全不需要更改 EasyWayRoutine() 的参数。

> Cross-Reference For details on the hazards of passing too much data, see "Keep Coupling Loose" in Section 5.3.

你可以将这种技术推向极端，将程序中的所有变量放入一个大而多汁的变量中，然后到处传递它。谨慎的程序员避免将数据捆绑超过逻辑上必要的程度。此外，谨慎的程序员避免在只需要结构中的一两个字段时将结构作为参数传递——他们只传递所需的特定字段。这就是信息隐藏的一个方面：某些信息隐藏在例程中，某些信息对例程隐藏。信息是按需传递的。

## 使用结构减少维护

由于你在使用结构时将相关数据分组，因此更改结构需要在整个程序中进行更少的更改。这在与结构更改在逻辑上无关的代码段中尤其如此。由于更改往往会产生错误，更少的更改意味着更少的错误。如果你的 *Employee* 结构有一个 *title* 字段并且你决定删除它，你不需要更改任何使用整个结构的参数列表或赋值语句。当然，你必须更改任何专门处理员工职称的代码，但这在概念上与删除 *title* 字段相关，很难被忽略。

结构化数据的最大优势在于与 *title* 字段在逻辑上没有任何关系的代码段。有时程序中的语句在概念上引用的是一个数据集合而不是单个组件。在这种情况下，单个组件，例如 *title* 字段，只是被引用因为它们是集合的一部分。此类代码段在逻辑上没有理由专门处理 *title* 字段，并且在你更改 *title* 时很容易被忽略。如果你使用结构，忽略此类代码段是可以的，因为代码引用的是相关数据的集合而不是每个组件。

## 13.2 指针

![](img/649c8eee28c38ca1e062691e45dc9883_359_0.png)

指针的使用是现代编程中最容易出错的领域之一，以至于像 Java、C# 和 Visual Basic 这样的现代语言都不提供指针数据类型。使用指针本质上很复杂，并且正确使用它们需要你对编译器的内存管理方案有极好的理解。许多常见的安全问题，尤其是缓冲区溢出，都可以追溯到指针的错误使用（Howard and LeBlanc 2003）。

即使你的语言不需要你使用指针，对指针的良好理解也会帮助你理解编程语言的工作原理。适量的防御性编程实践会更有帮助。

## 理解指针的范式

从概念上讲，每个指针都由两部分组成：内存中的一个位置以及如何解释该位置内容的知识。

## 内存中的位置

内存中的位置是一个地址，通常以十六进制表示。在 32 位处理器上，地址将是一个 32 位值，例如 0x0001EA40。指针本身仅包含此地址。要使用指针指向的数据，你必须转到该地址并解释该位置内存的内容。如果你查看该位置的内存，它只是一组位。它必须被解释才有意义。

## 如何解释内容的知识

如何解释内存中某个位置内容的知识由指针的基础类型提供。如果一个指针指向一个整数，这实际上意味着编译器将指针给出的内存位置解释为一个整数。当然，你可以有一个整数指针、一个字符串指针和一个浮点指针都指向同一个内存位置。但只有其中一个指针正确地解释了该位置的内容。

在思考指针时，有助于记住内存本身没有固有的解释。只有通过使用特定类型的指针，特定位置的位才被解释为有意义的数据。

图 13-1 显示了同一内存位置的几种视图，以几种不同的方式解释。

![](img/649c8eee28c38ca1e062691e45dc9883_360_0.png)

**Figure 13-1**  The amount of memory used by each data type is shown by double lines.

在图 13-1 的每种情况下，指针都指向包含十六进制值 0x0A 的位置。使用的字节数超出 0A 取决于内存如何被解释。内存内容的使用方式也取决于内存如何

