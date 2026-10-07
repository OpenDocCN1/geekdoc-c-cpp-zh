

# 第 12 章：泛型

根据你对协变和逆变性的了解，你可能认为数组既不是安全的逆变性的，也不是安全的协变的。也就是说，你可能认为一个数组只有在从不被写入时才是安全的协变的，且只有在从不被读取时才是安全的逆变性的——尽管这两种限制似乎都不符合实际情况。

遗憾的是，C# 确实支持数组协变，尽管它不是类型安全的。例如，`Fruit[] fruits = new Apple[10];` 在 C# 中是完全合法的。如果你接着包含表达式 `fruits[0] = new Orange();`，那么运行时将以异常的形式抛出类型安全违反。令深困扰的是，将 `Orange` 赋值给 `Fruit` 数组并不总是合法的，因为这可能是一个 `Apple` 数组，但这种情况并非仅存在于 C# 中，而是存在于所有使用运行时实现数组的 CLR 语言中。

你应该尽量避免不安全的数组协变。每个数组都可以转换为只读（因此是安全的协变的）接口 `IEnumerable<T>`；也就是说，`IEnumerable<Fruit> fruits = new Apple[10]` 是既安全又合法的，因为如果你只有一个只读接口，就没有办法将 `Orange` 插入数组中。

| 指南 |
| :--- |
| **避免不安全的数组协变。相反，考虑将数组转换为只读接口 `IEnumerable<T>`，该接口可以通过协变转换进行安全转换。** |

# 泛型内部机制

鉴于前面的章节中讨论了对象在 CLI 类型系统中泛用性，得知泛型也是对象，这似乎并不令人意外。事实上，泛型类上的类型参数带有元数据，运行时在需要时使用这些元数据构建相应的类。因此，泛型支持继承、多态和封装。通过泛型，你可以定义方法、属性、字段、类、接口和委托。

为了实现这一点，泛型需要底层运行时的支持。反之，在 C# 语言中添加泛型是编译器和框架的共同特性。例如，为了避免装箱（boxing），基于值类型参数的泛型实现与基于引用类型参数的泛型是不同的。

# 高级主题

# 泛型的 CIL 表示

当泛型类被编译时，它与非泛型类没有显著区别。编译的结果仅由元数据和 CIL。CIL 是参数化的，以接受代码中某处用户提供的类型。例如，假设你有一个如列表 12.46 所示声明的简单 `Stack` 类。

**列表 12.46：** `Stack<T>` 声明

```csharp
public class Stack<T> where T : IComparable
{
    private T[] _Items;
    // 类的其余部分
    //...
}
```

当你编译该类时，生成的 CIL 是参数化的，看起来类似于列表 12.47。

**列表 12.47：** `Stack<T>` 的 CIL 代码

```csharp
.class private auto ansi beforefieldinit
Stack<1>([mscorlib]System.IComparable)T>
extends [mscorlib]System.Object
  ...
}
```

第一个值得注意的项是第二行中出现在 `Stack` 之后的 '1'。这是泛型类型的元（arity）：它声明了泛型类需要类型参数的类型参数数量。如 `EntityDictionary<TKey, TValue>` 的声明的元数为 2。

生成的 CIL 的第二行显示了施加在该类上的约束。类型参数 `T` 被装饰了 `IComparable` 约束的接口声明。

如果你继续查看 CIL，你会发现该项的类型为 `T` 的数组声明被更改为包含一个使用感叹号表示法的类型参数，这是支持泛型的 CIL 版本的特性。感叹号表示为该类指定的第一个类型参数的存在，如列表 12.48 所示。

# 列表 12.48：支持泛型的、带感叹号表示法的 CIL

```csharp
.class public auto ansi beforefield
'Stack'1<<[msclib]System,IComparable>> T>
extends [msclib]System.Object
{
    .field private !0[ ] _Items
}
```

除了代码中包含了元和用感叹号表示的类型参数外，为泛型类生成的 CIL 与为非泛型类生成的 CIL 之间几乎没有区别。

# 高级主题

# 基于值类型的泛型实例化

当泛型类型第一次使用值类型作为类型参数进行构造时，运行时会创建一个专门的泛型类型，并将提供的类型参数恰当地放置在 CIL 中。因此，运行时会为每个新的参数值类型创建新的泛型类型。

例如，假设某些代码声明了一个由整数构造的 `Stack`，如列表 12.49 所示。

# 列表 12.49：`Stack<int>` 定义

```csharp
Stack<int> stack;
```

第一次使用此类型 `Stack<int>` 时，运行时会生成 `Stack` 类的专门版本，用类型参数 `int` 替换其类型参数。从以后，每当代码使用 `Stack<int>` 类时（在列表 12.50 中你声明了两个 `Stack<int>` 实例），它们都使用运行时已经为 `Stack<int>` 生成的代码。

# 列表 12.50：声明类型 `Stack<T>` 的变量

```csharp
Stack<int> stackOne = new();
Stack<int> stackTwo = new();
```

如果在代码后期创建了具有不同类型参数（例如用户定义的结构体）的另一个 `Stack`，运行时将生成另一个版本的泛型类型。专门化类的用处是性能更好。此外，代码可以避免装箱，因为每个专门的泛型都原生包含该值类型。

# 高级主题

# 基于引用类型的泛型实例化

泛型对引用类型的工作方式有所不同。当泛型第一次使用引用类型进行构造时，运行时会创建一个专门的泛型类型，在 CIL 中用对象引用替换类型参数，而不是创建一个专门的泛型类型。此后每次构造的类型是引用类型时，运行时都会复用之前生成的泛型类型版本，即使引用类型不同。

例如，假设有两个引用类型：`Customer` 类和 `Order` 类。接下来，你创建一个 `Customer` 类型的 `EntityDictionary`：

```csharp
EntityDictionary<Guid, Customer> customers;
```

在访问此类之前，运行时会生成该泛型类的专门版本，它不是将 `Customer` 存储为指定的数据类型，而是存储对象引用。假设下一行代码创建了另一个引用类型 `Order` 的 `EntityDictionary`：

```csharp
EntityDictionary<Guid, Order> orders =
new EntityDictionary<Guid, Order>();
```

与值类型不同，为使用 `Order` 类型的 `EntityDictionary` 没有创建新的泛型类专门版本。相反，将实例化使用对象引用的 `EntityDictionary` 实例，并将 `orders` 变量指向它。

为了仍然获得类型安全的优势，对于每个替换类型参数的对象引用，运行时会为专门分配的 `Order` 类型使用相同的内存区域，并将指针设置为该内存引用。假设你随后遇到一行实例化 `Customer` 类型 `EntityDictionary` 的代码如下：

```csharp
customers = new EntityDictionary<Guid, Customer>();
```

与之前使用 `Order` 类型创建的 `EntityDictionary` 类一样，会实例化另一个专门的 `EntityDictionary` 类实例（基于对象引用的版本），并将其中包含的指针设置为引用 `Customer` 类型。

尽管当泛型引用类型的类型参数发生变化时，运行时使用相同的内部泛型类型定义，但如果类型参数是值类型，这种行为将被取代。例如，`Dictionary<int, Customer>`、`Dictionary<Guid, Order>` 和 `Dictionary<long, Order>` 将新的内部类型定义。

