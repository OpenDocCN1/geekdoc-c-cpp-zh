

## 定义和使用数组

你可以把数组看作是一个装有相同类型事物的大家袋或列表。你在声明数组时定义数组中事物的数据类型。数组中的每个项目都由一个顺序编号（所谓的索引）标识，从 0 开始，因此数组是零基的。在 VB.NET 中声明和访问数组时使用圆括号，而在 C# 中使用方括号。在你定义数组并填充其元素后，可以通过其零基元素索引（0、1、2 等）访问元素。

以下代码片段定义了一个名为 roles 的数组，它可以同时容纳多达两个角色：

```
VB.NET
Dim roles(1) As String

C#
string[] roles = new string[2];
```

你看到了 VB.NET 和 C# 示例之间的区别吗？这不是笔误。在 VB.NET 中，你通过指定上界来定义数组的大小。上界是你可以在数组中访问的最后一个元素。因为数组是零基的（也就是说，你使用索引 0 来寻址数组中的项目），如果你需要容纳两个项目，上界就是 1，给你项目 0 和 1。

在 C# 中，另一方面，你不定义上界，而是定义大小。因此在 C# 中，你只需指定 2 即可获得包含两个元素的数组。

此外，C# 要求你使用关键字 new，它会为你实例化一个新数组。VB.NET 不会自动执行此操作，如果你像 C# 示例中那样使用 New 关键字，它会引发错误。你将在本章后面看到 new（VB.NET 中的 New）关键字。

要将角色输入数组，你使用以下语法：

```
VB.NET
roles(0) = "Administrators"
roles(1) = "ContentManagers"

C#
roles[0] = "Administrators";
roles[1] = "ContentManagers";
```

与数组一样，你在 VB.NET 中使用圆括号，在 C# 中使用方括号来寻址数组中的元素。请注意，(0) 和 [0] 指的是数组中的第一个元素，而 (1) 和 [1] 指的是第二个。

按设计，数组具有固定大小。鉴于前面的示例，一个可容纳两个元素的数组会抛出错误：

```
VB.NET
roles(2) = "Members" // Throws an error

C#
roles[2] = "Members"; // Throws an error
```

此代码试图将第三个角色挤入只能容纳两个角色的数组中。显然，这不合适，你会收到“Index was outside the bounds of the array.”的错误。
但如果在代码的后期运行阶段需要为数组创建更多空间怎么办？VB.NET 非常简单。你可以使用 ReDim 语句：

```
ReDim Preserve roles(2)
roles(2) = "Members" ' Works fine now
```

此行代码将数组重新调整为其新大小：上界为二，为第三个元素腾出空间。Preserve 关键字是必要的，以保持当前项目在数组中完好无损。没有它，重新调整大小的数组将为空。

C# 没有直接重新调整数组大小的方法。然而，你可以利用 .NET Framework 的 Array 类来调整数组大小，如下所示：

```
Array.Resize(ref roles, 3); // Resize the array so it can hold three elements

roles[2] = "Members"; // Works fine now
```

现在不要担心这种语法；你可能很少需要它，因为 .NET Framework 提供了固定大小数组的替代方案。由于 Array.Resize 也可用于 VB.NET，如果你使用该语言，则有两个选择。

当你开始使用数组时，你会发现它们在运行时使用起来很快，但缺乏一些有用的功能。向数组添加新元素或从数组中删除现有项目并不容易。幸运的是，.NET Framework 提供了各种有用的集合，可以提供你需要的功能

## 定义和使用集合

集合与数组类似，因为它们使你能够在一个变量中存储多个对象。袋子类比适用于集合：你可以简单地将一些项目放入袋子中，它会为你保存它们。集合与众不同之处在于它们如何通过 Add 方法使你能够工作，以将元素添加到集合中。同样，它们具有 Remove 和 Clear 方法，可从集合中删除一个或所有项目。就像数组一样，它们使你能够迭代，或循环，以访问集合中的项目。

当集合在 .NET Framework 1.0 中引入时，ArrayList 和 Hashtable 因其易于使用而迅速变得流行。ArrayList 使你能够添加任意对象，这些对象以你添加它们的顺序存储，而 Hashtable 使你能够按自定义键引用对象存储。与前面的示例相比，这些集合的主要好处是，你需要调整数组大小以腾出第三个角色的空间，而 ArrayList 在需要时动态增长。以下示例向你展示了它的工作原理：

```
VB.NET
Dim roles As New ArrayList() // Create a new ArrayList. You don't need to set its size explicitly

roles.Add("Administrators") // Add the first role
```

```
roles.Add("ContentManagers")   ' Add the second role
roles.Add("Members")             ' Keep adding roles and the ArrayList
                                     ' grows as necessary
```

### C#

```
ArrayList roles = new ArrayList(); // Create a new ArrayList. You don't need
                                            // to set its size explicitly

roles.Add("Administrators");      // Add the first role
roles.Add("ContentManagers")   // Add the second role
roles.Add("Members");             // Keep adding roles and the ArrayList
                                     // grows as necessary
```

由于此代码现在调用一个方法（Add）而不是将其分配给数组中的预定义索引，因此在 VB.NET 和 C# 中都需要使用圆括号（()）。方法的使用将在本章后面讨论。

所有集合都解决了数组的一些问题，但也引入了一些自身的问题。它们最大的缺点是它不是强类型的。这意味着你可以使用 Add 方法将任何对象添加到列表中。这意味着 ArrayList 可以同时保存不同类型的对象。这乍一看可能不是什么大问题，但当你开始使用包含多种类型对象的 ArrayList 工作时，你会很快明白这为什么有问题。以 roles 为例。使用数组和 ArrayList 版本，代码只是添加了一些包含名称的字符串。然后你可以使用这些字符串来构建 Web 表单中的下拉列表，以便用户选择角色。到目前为止，一切都很好，但如果列表中的其中一个项目不是字符串怎么办？如果另一位开发人员不小心编写了一些代码，将 Drop 控制添加到 ArrayList 中怎么办？由于 ArrayList 接受所有对象，它不会抱怨。然而，如果你的代码期望一个 String，但得到一个 DropList 控制，则你的代码将会崩溃。

随着 .NET 2.0 的发布，微软引入了一个名为 generics 的概念。泛型在 .NET 的 4.5.1 版本中仍然强劲存在，帮助你克服像 ArrayList 这样的弱类型集合引入的问题。

## 泛型简介

自 .NET 2.0 引入以来，泛型在 .NET Framework 的许多位置出现。虽然它们在集合使用的地方使用，但泛型的使用并不限于集合；你也可以将它们用于更简单的对象类型。

泛型对代码来说就像文字处理中的 Word 模板。它们使你能够编写一个代码模板，该模板可以在不同场景中使用不同类型。与泛型一起，你可以定义一个不指定类型的通用模板。只有在实例化它时才定义类型。这项主要的好处是，你可以一遍又一遍地重用同一个模板用于多种数据类型，而无需重写和维护多个版本的代码。除了在代码定义中使用泛型之外，你还可以在 .NET Framework 中找到大量可供你的代码使用的泛型启用对象和集合。

要了解如何利用泛型，请看下面的示例。它本质上是你之前看到的 ArrayList 使用的相同代码，但这次列表的类型受到限制，因此它只接受字符串：

