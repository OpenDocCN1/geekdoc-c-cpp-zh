
## 访问修饰符

另一种修饰符是访问修饰符。它指定类型及其成员的可访问性级别。C# 包含以下可访问性修饰符：

- `public`
- `protected`
- `internal`
- `protected internal`
- `private`

公共访问提供的访问限制最少；访问 `public` 成员或类基本上没有限制。请注意，在示例 3-1 中，`class` 定义和 `Main( )` 方法标头都包含 `public` 访问修饰符。通过指定 `public` 访问权限，其他类可以在不同应用程序中重用你的类。

私有是最具限制性的访问修饰符。私有成员只能在其声明所在的 `class` 主体内访问。在面向对象设计中，数据通常使用 `private` 修饰符定义，而访问这些数据的方法则声明为具有 `public` 访问权限。通过将数据成员定义为 `private`，你可以限制通过成员的方法或属性访问数据，这些内容你将在本章中学习。

表 3-1 显示了访问修饰符的不同可访问性级别。

表 3-1 C# 访问修饰符

| 修饰符 | 可访问性说明 |
| --- | --- |
| `public` | 无限制 |
| `protected` | 限于包含它的*类*或从包含它的*类*派生的类 |
| `internal` | 限于当前项目 |
| `protected internal` | 限于当前项目或从*类*派生的类 |
| `private` | 限于包含它的*类* |

当 `class` 或 `class` 成员未指定修饰符时，将假定默认可访问性级别为 `private`。本章后面，你将了解另一种修饰符：`override`。此关键字添加到方法标头中，用于为先前定义的方法声明新定义。先前定义的方法和新方法都由同一个标识符引用。

## 返回类型

返回类型标识方法完成时返回的值的类型。可以返回任何预定义类型或有效的用户定义类型。方法可以在其所有语句执行完毕时返回一个值，也可以只是将控制权返回给调用它的方法，而不带回值。

返回类型总是紧挨着方法名之前列出，如图 3-1 所示。方法不必返回任何内容；不过，通过方法名最多只能返回一种数据类型。

> 你将在第 7 章学习数组和集合（如 ArrayList）。C# 允许方法返回集合；不过，返回必须通过单个标识符进行。该标识符可以是数组的名称。

如果方法不返回值，则将 void 关键字放在方法标头中的返回类型位置，如下行代码所示：

```
public void DisplayInstructions( )
```

如果方法标头中指定的返回类型不是 void，则方法体中必须包含 return 语句。返回的值必须是兼容的值——要么与标头中的类型匹配，要么可以存储在该类型中。

return 语句的形式如下：

```
return [value];
```

注意，value 放在方括号中表示它是可选的。如果方法标头使用 void 作为返回类型，则可以省略或包含 return 语句，如下所示：

```
return;
```

只要返回类型不是 void，就必须在 return 关键字后面有一个返回值。该值可以是字面量、算术表达式或保存值的变量。示例 3-3 演示了返回计算值。

### 示例 3-3

```
public static double CalculateMilesPerGallon
    (int milesTraveled, double gallonsUsed)
{
    return milesTraveled / gallonsUsed;
}
```

示例 3-3 中的方法标头表明返回一个 **double** 值。这就是 **public** 关键字后面的 **double**。在方法体内部，除法结果会生成一个兼容的 **double** 值。

返回的值会发送回程序中调用该方法的位置。例如，`CalculateMilesPerGallon( )` 方法返回的值会发送回 `WriteLine( )` 方法，以便在下面的调用中显示：

```
Console.WriteLine("Miles per gallon = {0:N2}",
                  CalculateMilesPerGallon(289, 12.2));
```

`WriteLine( )` 方法产生的输出将是：

```
Miles per gallon = 23.69
```

![](img/e33ae760e23d89eac66541252ad65de8_165_0.png)

如果你的方法只有一个入口和一个出口，程序会更容易修改和调试。这是一种你应该尝试纳入设计的问题解决技巧。其含义是，你应该尽量在一个方法中只使用一个 **return** 语句。

## 方法名

命名方法时，遵循创建标识符的规则，这些规则在第 2 章中描述。标识符应是有意义的名称，用来标识代码段的总体用途。许多程序员使用标准约定，用动作动词短语命名方法。这个动词短语应描述方法打算完成的任务。**类**和方法标识符使用 **Pascal 命名法**。这种 C# 约定规定，当标识符至少包含三个字符时，首字符大写。作为标识符一部分的后续单词也以大写字符开头。遵循这些风格约定的方法标识符示例包括：`CalculateSalesTax( )`、`AssignSectionNumber( )`、`DisplayResults( )`、`InputAge( )` 和 `ConvertInputValue( )`。

![](img/e33ae760e23d89eac66541252ad65de8_165_1.png)

C# 程序对数据成员标识符使用 **Camel 命名法**约定。这种风格规定标识符的首字母小写，后续每个连接单词的首字母大写。示例包括 `studentName`、`major` 和 `yearInSchool`。

## 参数

方法标头圆括号内的项称为参数（parameters），或实参（arguments）。有时方法需要提供独特的数据。例如，如果编写一个方法计算三个值的平均值，该方法需要将这三个值发送给它。示例 3-3 中的 `CalculateMilesPerGallon( )` 方法需要两个实参：一个用于 `milesTraveled` 的 **int** 值和一个用于 `gallonsUsed` 的 **double** 值。正是通过参数和实参，数据才能传入方法中。

编写方法时，你决定该方法需要什么类型的独特数据。然后，将数据类型和该数据类型的标识符放在圆括号内。你必须在圆括号内包含匹配的类型和标识符对。`CalculateMilesPerGallon( )` 方法的两个匹配参数对如下：

```
(int milesTraveled, double gallonsUsed)
```

在方法体中，标识符用于引用应在何处以及何时使用该独特数据项。对于 `CalculateMilesPerGallon( )` 方法，`milesTraveled` 和 `gallonsUsed` 用在算术表达式中。表达式的结果返回给调用方法。

有些程序员区分参数和实参，使用术语 **参数** 来指代出现在方法标头中的项，而使用 **实参** 来指代出现在方法调用中的项。另一些人则通过在术语前加上 actual 和 formal 来区分实参和参数。**形式参数**，或称实参，出现在方法标头中。**实际实参**，或称参数，出现在调用中。把实际实参看作发送给方法的实际数据。形式参数就像占位符；它们形式化地指明期望发送什么类型的数据供方法使用。本书使用术语“parameters”指代方法标头中的项，并使用术语“arguments”指代通过方法调用发送到方法中的项。对于示例 3-3，`CalculateMilesPerGallon( )` 方法的实参是 289 和 12.2。这是实际数据或数字；不过，实际实参也可以是变量的标识符。它还可以是涉及算术语句的表达式或对另一个方法的调用。

与 `return` 类型一样，参数是可选的。如果不包含参数，则使用一对空圆括号。如果包含多个参数，则用逗号分隔。

> 有些语言将 void 关键字放在圆括号内代替参数列表，以表示不需要参数。C# 不允许这样做，并会生成语法错误。

参数有几种不同类型，本章后面将进行探讨。

## 方法体

如你在示例 3-1 中所见，构成方法体的语句括在花括号中。下面的 `DisplayMessage( )` 方法体包含两次对 `Console` 类中 `Write( )` 方法的调用、一次对 `Console` 类中 `WriteLine( )` 方法的调用，以及一个不返回值的 `return` 语句。

```csharp
public void DisplayMessage( )
{
    Console.Write("This is ");
    Console.Write("an example of a method ");
    Console.WriteLine("body. ");
    return;    // no value is returned
}
```
