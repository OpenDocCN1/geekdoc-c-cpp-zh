

`SimpleArray/Program.cs`：

```
Person[] beatles = {
    new Person { FirstName="John", LastName="Lennon" },
    new Person { FirstName="Paul", LastName="McCartney" }
};
Person[] beatlesClone = (Person[])beatles.Clone();
```

![](img/3d365b72b289213a91ade7eb366b8f35_279_0.png)

图 7.6

除了使用 `Clone` 方法，你也可以使用 `Array.Copy` 方法，它同样会创建浅拷贝。不过，`Clone` 和 `Copy` 有一个重要区别：`Clone` 会创建一个新数组；而使用 `Copy` 时，你必须传入一个秩相同且元素数量足够的现有数组。

> **注意** *如果你需要包含引用类型的数组的深拷贝，你必须遍历数组并创建新对象。*

## 排序

`Array` 类使用快速排序算法对数组中的元素进行排序。`Sort` 方法要求数组中的元素实现 `IComparable` 接口。诸如 `System.String` 和 `System.Int32` 之类的简单类型实现了 `IComparable`，因此你可以对包含这些类型的元素进行排序。

在示例程序中，`names` 数组包含 `string` 类型的元素，可以对该数组排序（代码文件 `SortingSample/Program.cs`）：

```
string[] names = {
    "Christina Aguilera",
    "Shakira",
    "Beyonce",
    "Lady Gaga"
};

Array.Sort(names);

foreach (var name in names)
{
    WriteLine(name);
}
```

应用程序的输出显示了数组排序后的结果：

```
Beyonce
Christina Aguilera
Lady Gaga
Shakira
```

如果你将自定义类用于数组，你必须实现 `IComparable` 接口。该接口只定义了一个方法 `CompareTo`，如果要比较的对象相等，该方法返回 0；如果实例应排在参数对象之前，则返回小于 0 的值；如果实例应排在参数对象之后，则返回大于 0 的值。

修改 `Person` 类以实现 `IComparable<Person>` 接口。比较时首先使用 `String` 类的 `Compare` 方法对 `LastName` 的值进行比较。如果 `LastName` 值相同，再比较 `FirstName`（代码文件 `SortingSample/Person.cs`）：

```
public class Person: IComparable<Person>
{
    public int CompareTo(Person other)
    {
        if (other == null) return 1;

        int result = string.Compare(this.LastName, other.LastName);
        if (result == 0)
        {
            result = string.Compare(this.FirstName, other.FirstName);
        }
        return result;
    }
    //...
```

现在可以按姓氏对 `Person` 对象数组进行排序（代码文件 `SortingSample/Program.cs`）：

```
Person[] persons = {
        new Person { FirstName="Damon", LastName="Hill" },
        new Person { FirstName="Niki", LastName="Lauda" },
        new Person { FirstName="Ayrton", LastName="Senna" },
        new Person { FirstName="Graham", LastName="Hill" }
    };

    Array.Sort(persons);
    foreach (var p in persons)
    {
        WriteLine(p);
    }
```

使用 `Person` 类的排序，输出返回按姓氏排序的名字：

```
Damon Hill
Graham Hill
Niki Lauda
Ayrton Senna
```

如果 `Person` 对象需要以不同方式排序，或者你无法更改用作数组元素的类，你可以实现 `IComparer` 或 `IComparer<T>` 接口。这些接口定义了 `Compare` 方法。这两个接口都不需要由被比较的类实现。`IComparer` 接口独立于要比较的类。这就是为什么 `Compare` 方法定义了两个需要比较的参数。返回值与 `IComparable` 接口的 `CompareTo` 方法类似。

`PersonComparer` 类实现了 `IComparer<Person>` 接口，以便按 `FirstName` 或 `LastName` 对 `Person` 对象进行排序。枚举 `PersonCompareType` 定义了 `PersonComparer` 可用的不同排序选项：`FirstName` 和 `LastName`。比较方式通过 `PersonComparer` 类的构造函数定义，该构造函数设置了一个 `PersonCompareType` 值。`Compare` 方法使用 `switch` 语句实现，以按 `LastName` 或 `FirstName` 进行比较（代码文件 `SortingSample/PersonComparer.cs`）：

```
public enum PersonCompareType
{
    FirstName,
    LastName
}

public class PersonComparer: IComparer<Person>
{
    private PersonCompareType _compareType;

    public PersonComparer(PersonCompareType compareType)
    {
        _compareType = compareType;
    }

    public int Compare(Person x, Person y)
    {
        if (x == null && y == null) return 0;
        if (x == null) return 1;
        if (y == null) return -1;

        switch (_compareType)
        {
            case PersonCompareType.FirstName:
                return string.Compare(x.FirstName, y.FirstName);
            case PersonCompareType.LastName:
                return string.Compare(x.LastName, y.LastName);
            default:
                throw new ArgumentException("unexpected compare type");
        }
    }
}
```

现在你可以将一个 `PersonComparer` 对象传递给 `Array.Sort` 方法的第二个参数。这里，人员按名字排序（代码文件 `SortingSample/Program.cs`）：

```
Array.Sort(persons, new PersonComparer(PersonCompareType.FirstName));

foreach (var p in persons)
{
    WriteLine(p);
}
```

persons 数组现在按名字排序：

```
Ayrton Senna
Damon Hill
Graham Hill
Niki Lauda
```

> **注意** `Array` 类还提供了需要委托作为参数的 `Sort` 方法。使用该参数，你可以传递一个方法来比较两个对象，而不必依赖 `IComparable` 或 `IComparer` 接口。第 9 章“委托、Lambda 表达式和事件”讨论了如何使用委托。

## 数组作为参数

数组可以作为参数传递给方法，也可以从方法返回。返回数组时，你只需将数组声明为返回类型，如下面的 `GetPersons` 方法所示：

```
static Person[] GetPersons()
{
    return new Person[] {
        new Person { FirstName="Damon", LastName="Hill" },
        new Person { FirstName="Niki", LastName="Lauda" },
        new Person { FirstName="Ayrton", LastName="Senna" },
        new Person { FirstName="Graham", LastName="Hill" }
    };
}
```

将数组传递给方法时，数组通过参数声明，如下面的 `DisplayPersons` 方法所示：

```
static void DisplayPersons(Person[] persons)
{
    //...
}
```

## 数组协变

数组支持协变。这意味着数组可以声明为基类型，而派生类型的元素可以被赋值给元素。

例如，你可以声明一个 `object[]` 类型的参数，如下所示，并将一个 `Person[]` 传递给它：

```
static void DisplayArray(object[] data)
{
    // ...
}
```

> **注意** *数组协变仅适用于引用类型，不适用于值类型。此外，数组协变有一个只能通过运行时异常解决的问题。如果你将 `Person` 数组赋给对象数组，那么该对象数组随后可用于任何派生自 `object` 的类型。编译器会接受例如将字符串传递给数组元素的操作。然而，由于对象数组引用的是一个 `Person` 数组，运行时就会抛出 `ArrayTypeMismatchException` 异常。*

## ArraySegment\<T\>

结构 `ArraySegment<T>` 表示数组的一个片段。如果你处理的是一个大数组，并且不同的方法处理数组的不同部分，你可以将数组部分复制给这些方法。与其创建多个数组，更高效的做法是使用一个数组并将整个数组传递给这些方法。这些方法应该只使用数组的一部分。为此，你可以传递数组中的偏移量以及方法应使用的元素数量，再加上数组本身。这样，至少需要三个参数。使用数组片段时，只需要一个参数。`ArraySegment<T>` 结构包含有关片段的信息（偏移量和计数）。

`SumOfSegments` 方法接受一个 `ArraySegment<int>` 元素数组，用于计算这些片段所定义的所有整数的总和，并返回该总和（代码文件 `ArraySegmentSample/Program.cs`）：

```
static int SumOfSegments(ArraySegment<int>[] segments)
{
    int sum = 0;
    foreach (var segment in segments)
    {
        for (int i = segment.Offset; i < segment.Offset + segment.Count; i++)
        {
            sum += segment.Array[i];
        }
    }
    return sum;
}
```

该方法通过传递一个片段数组来使用。第一个数组元素引用 `ar1` 中从第一个元素开始的三个元素；第二个数组元素引用 `ar2` 中从第四个元素开始的三个元素：

```
int[] ar1 = { 1, 4, 5, 11, 13, 18 };
int[] ar2 = { 3, 4, 5, 18, 21, 27, 33 };

var segments = new ArraySegment<int>[2]
{
    new ArraySegment<int>(ar1, 0, 3),
    new ArraySegment<int>(ar2, 3, 3)
};
```

