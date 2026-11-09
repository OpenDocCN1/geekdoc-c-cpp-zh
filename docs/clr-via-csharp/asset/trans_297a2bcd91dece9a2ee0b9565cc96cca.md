
确保类型安全，并且在给数组元素赋值时，CLR 必须确保该赋值是合法的。因此，CLR 必须在运行时检查数组是否包含 `Int32` 元素。在这个例子中，数组不包含 `Int32` 元素，因此不能允许该赋值；CLR 将抛出 `ArrayTypeMismatchException`。

> **注意**
>
> 如果你只需要将某些数组元素复制到另一个数组，`System.Buffer` 的 **BlockCopy** 方法比 `Array` 的 **Copy** 方法执行得更快。但是，**Buffer** 的 **BlockCopy** 仅支持基元类型；它不提供 **Array** 的 **Copy** 方法那样的类型转换能力。**Int32** 参数表示为数组内的字节偏移量，而不是元素索引。**BlockCopy** 实际上是为将按位兼容的数据从一种数组类型复制到另一种按位兼容的数组类型而设计的，例如将包含 Unicode 字符的 `Byte[]`（按正确字节顺序）复制到 `Char[]`。此方法使程序员能够部分弥补无法将数组视为任意类型内存块的不足。
>
> 如果你需要可靠地将一组数组元素从一个数组复制到另一个数组，则应使用 `System.Array` 的 **ConstrainedCopy** 方法。此方法保证复制操作要么完成，要么抛出异常，而不会破坏目标数组中的任何数据。这使得 **ConstrainedCopy** 可用于受约束执行区域（CER）。为了提供此保证，**ConstrainedCopy** 要求源数组的元素类型与目标数组的元素类型相同或是其派生类型。此外，它不会执行任何装箱、拆箱或向下转换。

### 所有数组都隐式派生自 System.Array

当你像这样声明一个数组变量时，

```csharp
FileStream[] fsArray;
```

CLR 会自动为 AppDomain 创建一个 `FileStream[]` 类型。此类型将隐式派生自 `System.Array` 类型，因此，在 `System.Array` 类型上定义的所有实例方法和属性都将由 `FileStream[]` 类型继承，从而允许使用 `fsArray` 变量调用这些方法和属性。这使得数组的使用极其方便，因为 `System.Array` 定义了许多有用的实例方法和属性，例如 `Clone`、`CopyTo`、`GetLength`、`GetLongLength`、`GetLowerBound`、`GetUpperBound`、`Length`、`Rank` 等。

`System.Array` 类型还公开了大量极其有用的、用于操作数组的静态方法。这些方法都以数组的引用作为参数。一些有用的静态方法包括 `AsReadOnly`、`BinarySearch`、`Clear`、`ConstrainedCopy`、`ConvertAll`、`Copy`、`Exists`、`Find`、`FindAll`、`FindIndex`、`FindLast`、`FindLastIndex`、`ForEach`、`IndexOf`、`LastIndexOf`、`Resize`、`Reverse`、`Sort` 和 `TrueForAll`。这些方法中的每一个都有许多重载。事实上，许多方法都提供了泛型重载，以实现编译时类型安全以及良好的性能。我鼓励你查阅 SDK 文档，以了解这些方法有多么有用和强大。

### 所有数组都隐式实现 IEnumerable、ICollection 和 IList

有许多方法可操作各种集合对象，因为这些方法声明的参数类型为 `IEnumerable`、`ICollection` 和 `IList`。可以将数组传递给这些方法，因为 `System.Array` 也实现了这三个接口。`System.Array` 实现这些非泛型接口，是因为它们将所有元素都视为 `System.Object`。然而，如果 `System.Array` 能实现这些接口的泛型等效接口，从而提供更好的编译时类型安全和更好的性能，那将很不错。

不过，CLR 团队不希望 `System.Array` 实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`，因为存在与多维数组和非零基数组相关的问题。在 `System.Array` 上定义这些接口会使所有数组类型都启用这些接口。相反，CLR 采用了一个小技巧：当创建单维、零下限的数组类型时，CLR 会自动使该数组类型实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`（其中 T 是该数组的元素类型），并且只要数组类型的所有基类型是引用类型，就也会为这些基类型实现这三个接口。下面的层次结构图有助于说明这一点：

```text
Object
    Array (non-generic IEnumerable, ICollection, IList)
        Object[]        (IEnumerable, ICollection, IList of Object)
            String[]    (IEnumerable, ICollection, IList of String)
                Stream[]    (IEnumerable, ICollection, IList of Stream)
                    FileStream[] (IEnumerable, ICollection, IList of FileStream)
        .
        .
        .        (other arrays of reference types)
        .
```

因此，例如，如果你有以下代码行，

```csharp
FileStream[] fsArray;
```

那么当 CLR 创建 `FileStream[]` 类型时，它将使该类型自动实现 `IEnumerable<FileStream>`、`ICollection<FileStream>` 和 `IList<FileStream>` 接口。此外，`FileStream[]` 类型还将为其基类型实现这些接口：`IEnumerable<Stream>`、`IEnumerable<Object>`、`ICollection<Stream>`、`ICollection<Object>`、`IList<Stream>` 和 `IList<Object>`。由于所有这些接口都由 CLR 自动实现，因此凡是需要这些接口的地方都可以使用 `fsArray` 变量。例如，可以将 `fsArray` 变量传递给具有以下任一原型的方法：

```csharp
void M1(IList<FileStream> fsList) { ... }
void M2(ICollection<Stream> sCollection) { ... }
void M3(IEnumerable<Object> oEnumerable) { ... }
```

请注意，如果数组包含值类型元素，则该数组类型不会为元素的基类型实现这些接口。例如，如果你有以下代码行，

```
DateTime[] dtArr; // An array of value types
```

那么 `DateTime[]` 类型将仅实现 `IEnumerable<DateTime>`、`ICollection<DateTime>` 和 `IList<DateTime>`；它不会实现针对 `System.ValueType` 或 `System.Object` 泛型化的这些接口版本。这意味着不能将 `dtArr` 变量作为参数传递给前面展示的 `M3` 方法。原因在于值类型数组在内存中的布局与引用类型数组不同。本章前面已讨论过数组的内存布局。

### 传递和返回数组

当将数组作为参数传递给方法时，你实际上传递的是对该数组的引用。因此，被调用的方法能够修改数组中的元素。如果你不想允许这样做，就必须创建该数组的副本，并将副本传入方法。请注意，`Array.Copy` 方法执行的是浅复制，因此，如果数组的元素是引用类型，则新数组引用的是已经存在的对象。

类似地，有些方法会返回对数组的引用。如果该方法构造并初始化了数组，那么返回对该数组的引用没有问题。但是，如果该方法想要返回对由字段维护的内部数组的引用，则必须决定是否希望方法的调用者可以直接访问此数组及其元素。如果希望如此，只需返回该数组的引用。但大多数情况下，你不会希望方法的调用者拥有这种访问权限，因此该方法应构造一个新数组并调用 `Array.Copy`，返回对新数组的引用。再次提醒，`Array.Copy` 对原始数组进行的是浅复制。

如果你定义的方法返回对数组的引用，并且该数组中没有元素，那么你的方法可以返回 `null`，也可以返回对包含零个元素的数组的引用。在实现这类方法时，Microsoft 强烈建议让方法返回零长度数组，因为这样做可以简化调用该方法的开发者必须编写的代码。例如，即使没有要遍历的预约，下面这段易于理解的代码也能正确运行：

```
// This code is easier to write and understand.
Appointment[] appointments = GetAppointmentsForToday();
for (Int32 a = 0; a < appointments.Length; a++) {
    ...
}
```

如果没有要遍历的预约，下面的代码也能正确运行。但是，这段代码编写和理解起来稍微困难一些：
