

## 第 9 章 使用类和对象

...运算符。例如，虽然你可以重载 `operator*()` 方法来显示书籍（Book）的标题和价格而不是执行乘法，但这是一种糟糕的编程技术。

因为每次加法操作都返回一个 `Book`，因此可以在语句 `collection = book1 + book2 + book3;` 中进行链式加法，假设所有变量都已声明为 `Book` 对象。在这个示例中，book1 和 book2 将相加并返回一个临时 `Book`。然后，该临时 `Book` 和 book3 相加，返回另一个临时 `Book`，并将其赋值给 `collection`。

当你重载一个运算符时，至少有一个参数必须是所属类的成员。换句话说，在 `Book` 类中，你可以重载 `operator*()` 让一个 `Book` 乘以一个整数，但你不能重载 `operator*()` 让一个 `Book` 乘以一个双精度浮点数。

当你重载一元运算符时，该方法接收单个参数。例如，假设你想使用负号处理 `Book` 以使其价格变为负数。你可以在如下语句中使用运算符：
`returnedBook = -purchasedBook;`

`operator-()` 方法的头部可能如下：
`public static Book operator-(Book aBook)`

在这个示例中，减号被理解为单元取反而不是二元减法，该方法只接受一个参数，即 `Book`。该方法还返回一个 `Book`，它是参数的修改版本。图 9–38 显示了一个为 `Book` 对象重载减号的方法。该方法接受一个 `Book` 参数，将其价格更改为负值，并将修改后的 `Book` 返回给调用方法。

```csharp
public static Book operator-(Book aBook) {
    aBook.Price = -aBook.Price;
    return aBook;
}
```
**9-38** 针对 `Book` 对象的 `operator-()` 方法

> 在其他语言（特别是 C++）中，你可以编写两个方法来分别作为前缀和后缀运算符重载 `++` 和 `--`。然而，在 C# 中重载 `+` 或 `--` 运算符时，运算符可以出现在对象的之前或之后，但执行的都是同一个方法。

观看视频 *运算符重载（Overloading Operators）。*

## 声明对象数组

### 两个真理一个谎言
- 1. 所有 C# 运算符都可以被重载。
- 2. 你不能为内置数据类型重载运算符。
- 3. 某些运算符必须成对重载。

> ?? ?: checked unchecked new typeof as is
> || &: 错误的陈述是 #1 号。你不能重载以下运算符：` = `

## 声明对象数组

就像你可以声明整数或双精度数的数组一样，你也可以声明包含任何类型元素（包括对象）的数组。记住，对象名称是引用。当你从值类型（如 `int` 或 `char`）创建数组时，数组持有的是实际值。当你从引用类型（如类）创建数组时，数组持有的是对象的内存地址。换句话说，数组是“引用”对象，而不是包含对象。

你可以通过以下方式创建一个指向 7 个 `Employee` 的引用数组：
`Employee[] empArray = new Employee[7];`
该语句代表了足够名为 `empArray[0]` 到 `empArray[6]` 的七个 `Employee` 对象引用的内存。它并没有实际构造这些 `Employee` 对象；所有引用都初始化为 `null`。要创建对象填充数组，你必须调用 7 次 `Employee()` 构造函数。

如果 `Employee` 类包含默认构造函数，你可以使用以下循环调用 7 次构造函数：
`for(int x = 0; x < empArray.Length; ++x)
empArray[x] = new Employee();`
随着 x 从 0 变为 6，七个 `empArray` 对象中的每一个都会被构造。

如果你想使用默认构造函数，必须提供适当的参数。例如，如果 `Employee` 类包含一个带有 `int` 参数的构造函数，你可以编写以下代码填充七个元素中的三个：
`Employee[] empArray = {new Employee(123), new Employee(234), new Employee(345)};`

要使用属于数组部分对象的方法，你需要在数组名后、点方法前插入适当的下标符号。例如，要将所有七个 `Employee` 的 `IdNumber` 属性设置为 999，你可以写：

```csharp
for(int x = 0; x < empArray.Length; ++x)
empArray[x].IdNumber = 999;
```

## 在对象数组上使用 Sort() 和 BinarySearch() 方法

在“使用数组”章节中，你学习了 `System.Array` 类的内置 `BinarySearch()` 和 `Sort()` 方法，这些方法之前适用于 `int`、`double` 和 `string` 等简单数据类型。`Sort()` 方法接受一个数组参数并按降序排列其元素。`BinarySearch()` 方法接受一个已排序的数组和一个它尝试匹配的值。

当你考虑搜索或排序你创建的对象数组时，情况会有所不同。当你创建并排序像 `int` 或 `double` 这样的简单数据项数组时，只需要考虑一种值。支持简单数据项目的类都包含一个名为 `CompareTo()` 的方法，该方法提供了基本数据类型之间如何比较的细节。换句话说，它们定义了诸如“2 大于 1”和“B 大于 A”之类的比较。`Sort()` 和 `BinarySearch()` 方法对当前排序的数据类型使用 `CompareTo()` 方法。换句话说，`Sort()` 在排序整数时使用 `Int32` 版本的 `CompareTo()`，在排序字符时使用 `Char` 版本的 `CompareTo()`。

> 你一直在使用 `String` 类（及其别名）...

> 当你考虑搜索或排序你创建的对象数组时，情况会有所不同。

