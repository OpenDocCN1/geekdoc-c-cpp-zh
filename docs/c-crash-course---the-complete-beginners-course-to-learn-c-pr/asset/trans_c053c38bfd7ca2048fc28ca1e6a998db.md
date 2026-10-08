
[content]
了解如何创建自己的泛型类。当你无法使用通用列表，并想要使用预制 .NET 库中找不到的自定义方法创建自己的类时，创建类是非常重要的。

当你创建一个自己的泛型类型时，你实际上创建了一个自定义类。让我们来看一个接受泛型类型的简单类。

```csharp
public class MyGeneric<T>
{
    private T[] array;
    public MyGeneric(int size)
    {
        array = new T[size + 1];
    }
}
```

在上面的代码中，我们创建了一个名为 `MyGeneric` 的泛型自定义类。注意 `>` 和 `<` 之间的 `T` 数据类型。这告诉编译器你想传递一个泛型类型。你可以传递自定义类，也可以传递像 `string` 这样的原始数据类型。这就是 `T` 符号在任何类中的意义。它允许你处理任何数据类型，而不会受到定义数组对类所加的限制。

注意该类的其他部分与我们之前创建的其他类相似。构造函数接收我们正在创建的泛型数组的大小，以便代码可以分配正确的内存空间。由于数据类型是泛型的，我们在 `MyGeneric` 数据类型内部创建了一个私有数组。通过 `T[]` 标记，我们可以在数组中存储任何数据类型。

泛型类创建完成后，我们现在需要一种在类内获取和设置项目的方法。由于我们在创建自己的泛型自定义类，我们需要创建这些方法。首先，让我们创建一个向泛型数组添加值的方法。

```csharp
public class MyGeneric<T>
{
    private T[] array;
    public MyGeneric(int size)
    {
        array = new T[size + 1];
    }

    public void setItem(int index, T value)
    {
        array[index] = value;
    }
}
```

注意我们向 `MyGeneric` 类添加了一个方法。我们保留了相同的属性和构造函数。我们添加了 `setItem` 方法。记住，方法是类的“动词”，所以这个方法向数组添加一个值。它接收数组的索引以标识你想放置值的位置，并使用 `T` 标记告诉编译器可以使用任何泛型数据类型。然后 `setItem` 方法将泛型数据类型分配给数组中的位置。

设置好 `setItem` 方法后，你现在需要从数组中检索值。让我们来看 `MyGeneric` 类中的新方法，它可以允许你从泛型数组中检索值。

```csharp
public class MyGeneric<T>
{
    private T[] array;
    public MyGeneric(int size)
    {
        array = new T[size + 1];
    }

    public T getItem(int index)
    {
        return array[index];
    }

    public void setItem(int index, T value)
    {
        array[index] = value;
    }
}
```

这是一个可以使用泛型工作的完整类。我们添加了从数组中检索信息的 `getItem` 方法。这就是你可以在程序中创建的泛型类的完成。

# 使用 List 泛型类

你可以创建自己的泛型类，也可以使用 .NET 框架提供的预制泛型类。使用预制类比创建自己的类简单得多。除非你对类有预制泛型无法提供的特定需求，否则你不需要创建自己的类。

有几个泛型类可用，但最常用的是 `List` 泛型类。`List` 类包含了你对列表所需要执行的所有操作。让我们先看看如何创建一个列表变量。

```csharp
List<int> myInts = new List<int>();
```

在代码中，原始数据类型设置在 `>` 和 `<` 之间。记住，泛型类型告诉你可以发送任何数据类型，但在此例中，我们使用了整数原始数据类型。

`int` 被传递给泛型 `List` 类，让它知道你想在数组中存储整数列表。

由于泛型 `List` 数据类型仍然是一个类，所以你需要使用 `new` 关键字并调用基构造函数。列表构造函数不需要参数，所以我们只需要使用括号且不向构造函数传递任何数据。

在定义变量并实例化 `List` 后，我们现在可以使用它的方法和属性了。让我们来看向变量中添加值的代码。

```csharp
List<int> myInts = new List<int>();
myInts.Add(1);
myInts.Add(2);
myInts.Add(3);
```

注意，向 `myInts` 变量添加值要容易得多。我们有 `Add` 方法，可以使用它来向泛型列表添加值。我们将数字 1、2、3 添加到 `myInts` 泛型列表变量中。这就足够了而不需要使用繁琐的代码。你也可以像我们在数组章节中使用那样使用 `for` 循环，但这向你的代码中添加值变得简单得多。

最后，你需要一种从泛型列表中检索值的方法。让我们来看可以用于循环遍历每个值并将结果打印到屏幕的代码。

```csharp
List<int> myInts = new List<int>();
myInts.Add(1);
myInts.Add(2);
myInts.Add(3);

for (int i = 0; i < myInts.Count; i++)
{
    Console.WriteLine("MyInts: {0}", myInts[i]);
}
```

在上面的代码中，我们使用了之前使用的相同方法，只是这次我们添加了一个额外的 `for` 循环来遍历每个 `myInts` 值并将其显示在屏幕上。注意，你可以使用 `for` 列表结构来遍历泛型列表中的每个值，就像处理数组一样。在大多数方面，泛型列表和数组的工作方式是类似的。

# 使用 List 类用于自定义类结构

在上面的代码中我们使用了原始整数，但你也可以在泛型列表中存储类结构。也就是说，你对自定义类的存储方式与你对列表中存储原始数字的方式是相同的。例如，如果你有一个包含客户信息的 `Customer` 类，你可能想要存储十个客户，每个客户都存储在自己的类中。然后你将自定义类添加到泛型列表中，这样你就在数组中存储了十个客户。然后你可以遍历这些 `Customer` 值并将它们存储在数据库中。这使得向你的代码中添加值变得更容易。

让我们看看如何创建一个列表变量。

```csharp
List<Customer> myInts = new List<Customer>();
```

在代码中，原始数据类型设置在 `>` 和 `<` 之间。记住，泛型类型告诉你可以发送任何数据类型，但在此例中，我们使用了 `Customer` 数据类型。

`Customer` 被传递给泛型 `List` 类，让它知道你想在数组中存储客户列表。

由于泛型 `List` 数据类型仍然是一个类，所以你需要使用 `new` 关键字并调用基构造函数。列表构造函数不需要参数，所以我们只需要使用括号且不向构造函数传递任何数据。

在定义变量并实例化 `List` 后，我们现在可以使用它的方法和属性了。让我们来看向变量中添加值的代码。

```csharp
List<Customer> myInts = new List<Customer>();
Customer cust = new Customer();
cust.first_name = "John";
cust.last_name = "Smith";
myInts.Add(cust);
```

注意，向 `myInts` 变量添加值要容易得多。我们有 `Add` 方法，可以使用它来向泛型列表添加值。我们将数字 1、2、3 添加到 `myInts` 泛型列表变量中。这就足够了而不需要使用繁琐的代码。你也可以使用 `for` 循环，但这使得向你的代码中添加值变得简单得多。

最后，你需要一种从泛型列表中检索值的方法。让我们来看可以用于循环遍历每个值并将结果打印到屏幕的代码。

```csharp
List<Customer> myInts = new List<Customer>();
Customer cust = new Customer();
cust.first_name = "John";
cust.last_name = "Smith";
myInts.Add(cust);

for (int i = 0; i < myInts.Count; i++)
{
    Console.WriteLine("MyInts: {0}", myInts[i].first_name);
}
```
