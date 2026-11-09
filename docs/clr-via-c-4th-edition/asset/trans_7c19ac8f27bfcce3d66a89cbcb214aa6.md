
```csharp
// Using ICloneable, I can call any method declared by the
// ICloneable interface (or any method defined by Object) only.

// The comparable variable refers to the same String object
IComparable comparable = s;
// Using comparable, I can call any method declared by the
// IComparable interface (or any method defined by Object) only.

// The enumerable variable refers to the same String object
// At run time, you can cast a variable from one interface to another as
// long as the object's type implements both interfaces.
IEnumerable enumerable = (IEnumerable) comparable;
// Using enumerable, I can call any method declared by the
// IEnumerable interface (or any method defined by Object) only.
```

在这段代码中，所有变量都引用托管堆中的同一个“Jeffrey”String对象，因此，使用这些变量中的任何一个调用任何方法，都是应用于这一个“Jeffrey”String对象。然而，变量的类型指示了能对该对象执行的操作。`s`变量的类型是`String`，因此，我可以使用`s`调用`String`类型定义的任何成员（如`Length`属性）。我还可以使用变量`s`调用从`Object`继承的任何方法（如`GetType`）。

`cloneable`变量是`ICloneable`接口类型，因此，使用`cloneable`变量，我可以调用该接口定义的`Clone`方法。此外，我可以调用`Object`定义的任何方法（如`GetType`），因为CLR知道所有类型都派生自`Object`。然而，使用`cloneable`变量，我不能调用`String`本身定义的公共方法，也不能调用`String`实现的任何其他接口定义的任何方法。类似地，使用`comparable`变量，我可以调用`CompareTo`或`Object`定义的任何方法，但使用该变量不能调用任何其他方法。

> **重要说明** 与引用类型一样，值类型可以实现零个或多个接口。然而，当将值类型的实例强制转换为接口类型时，值类型的实例必须装箱。这是因为接口变量是一个引用，必须指向堆上的对象，这样CLR才能检查对象的类型对象指针，以确定对象的确切类型。然后，当使用已装箱的值类型调用接口方法时，CLR将遵循对象的类型对象指针，找到类型对象的方法表，以调用正确的方法。

## 隐式与显式接口方法实现（幕后发生了什么）

当一个类型被加载到CLR中时，会为该类型创建并初始化一个方法表（如第1章“CLR的执行模型”所讨论的）。此方法表包含该类型引入的每个新方法的一个条目，以及该类型继承的任何虚方法的条目。继承的虚方法包括继承层次结构中基类型定义的方法，以及接口类型定义的任何方法。因此，如果你定义了一个简单的类型，如下所示：

```csharp
internal sealed class SimpleType : IDisposable {
    public void Dispose() { Console.WriteLine("Dispose"); }
}
```

该类型的方法表包含以下内容的条目：

- `Object`（隐式继承的基类）定义的所有虚实例方法。
- `IDisposable`（继承的接口）定义的所有接口方法。在此例中，只有一个方法`Dispose`，因为`IDisposable`接口只定义了一个方法。
- `SimpleType`引入的新方法`Dispose`。

为了简化程序员的操作，C#编译器假定`SimpleType`引入的`Dispose`方法就是`IDisposable`的`Dispose`方法的实现。C#编译器之所以做出此假定，是因为该方法是公共的，并且接口方法和新引入的方法的签名相同。也就是说，这些方法具有相同的参数和返回类型。顺便说一句，如果新的`Dispose`方法被标记为`virtual`，C#编译器仍然会认为此方法与接口方法匹配。

当C#编译器将新方法与接口方法匹配时，它会发出元数据，指示`SimpleType`方法表中的两个条目应引用同一实现。为了帮助说明更清楚，这里有一些代码演示了如何调用类的公共`Dispose`方法以及如何调用类对`IDisposable`的`Dispose`方法的实现。

```csharp
public sealed class Program {
    public static void Main() {
        SimpleType st = new SimpleType();

        // This calls the public Dispose method implementation
        st.Dispose();

        // This calls IDisposable's Dispose method implementation
        IDisposable d = st;
        d.Dispose();
    }
}
```

在第一次调用`Dispose`时，调用的是`SimpleType`定义的`Dispose`方法。然后我定义一个变量`d`，其类型是`IDisposable`接口类型。我将`d`变量初始化为引用`SimpleType`对象。现在当我调用`d.Dispose()`时，我调用的是`IDisposable`接口的`Dispose`方法。因为C#要求公共`Dispose`方法同时也是`IDisposable`的`Dispose`方法的实现，所以相同的代码会执行，并且在此示例中，你看不到任何可观察到的差异。输出如下。

```
Dispose
Dispose
```

现在，让我重写前面的`SimpleType`，以便你能看到可观察的差异。

```csharp
internal sealed class SimpleType : IDisposable {
    public void Dispose() { Console.WriteLine("public Dispose"); }
    void IDisposable.Dispose() { Console.WriteLine("IDisposable Dispose"); }
}
```

如果不更改前面展示的`Main`方法，只是重新编译并重新运行程序，输出将是以下内容。

```
public Dispose
IDisposable Dispose
```

在C#中，当你使用定义该方法的接口名称作为方法名的前缀（如此例中的`IDisposable.Dispose`）时，你就是在创建显式接口方法实现（EIMI）。注意，在C#中定义显式接口方法时，不允许指定任何可访问性（如`public`或`private`）。然而，当编译器为该方法生成元数据时，其可访问性被设置为`private`，从而防止使用类实例的任何代码直接调用该接口方法。调用该接口方法的唯一方式是通过接口类型的变量。

还要注意，EIMI方法不能被标记为`virtual`，因此不能被重写。这是因为EIMI方法实际上不是类型对象模型的一部分；它是一种将接口（一组行为或方法）附加到类型上而不会让这些行为/方法变得明显的方式。如果这一切对你来说似乎有点笨拙，那么你理解得没错——这确实有点笨拙。在本章后面，我将展示使用EIMI的一些合理理由。

## 泛型接口

C#和CLR对泛型接口的支持为开发者提供了许多出色的功能。在本节中，我想讨论使用泛型接口时带来的好处。

首先，泛型接口提供了出色的编译时类型安全性。一些接口（如非泛型的`IComparable`接口）定义的方法具有`Object`参数或返回类型。当代码调用这些接口方法时，可以传递任何类型实例的引用。但这通常不是我们所期望的。下面的代码演示了这一点。

```csharp
private void SomeMethod1() {
    Int32 x = 1, y = 2;
    IComparable c = x;

    // CompareTo expects an Object; passing y (an Int32) is OK
    c.CompareTo(y);     // y is boxed here

    // CompareTo expects an Object; passing "2" (a String) compiles
    // but an ArgumentException is thrown at runtime
    c.CompareTo("2");
}
```

显然，接口方法强类型化更为可取，这就是为什么FCL中包含一个泛型`IComparable<in T>`接口的原因。

以下是使用泛型接口修改后的新版本代码。

```csharp
private void SomeMethod2() {
    Int32 x = 1, y = 2;
    IComparable<Int32> c = x;

    // CompareTo expects an Int32; passing y (an Int32) is OK
    c.CompareTo(y);    // y is not boxed here

    // CompareTo expects an Int32; passing "2" (a String) results
    // in a compiler error indicating that String cannot be cast to an Int32
    c.CompareTo("2");  // Error
}
```

泛型接口的第二个好处是，在处理值类型时，装箱会少得多。注意在`SomeMethod1`中，非泛型`IComparable`接口的`CompareTo`方法期望一个`Object`；传递`y`（`Int32`值类型）会导致`y`中的值被装箱。然而，在`SomeMethod2`中，泛型`IComparable<in T>`接口的`CompareTo`方法期望一个`Int32`；传递`y`会按值传递，不需要装箱。

> **注意** FCL定义了`IComparable`、`ICollection`、`IList`和`IDictionary`接口以及一些其他接口的非泛型和泛型版本。如果你正在定义类型，并且想要实现这些接口中的任何一个，通常应该实现这些接口的泛型版本。非泛型版本在FCL中是为了向后兼容，以便与.NET Framework支持泛型之前编写的代码一起工作。非泛型版本还为用户提供了一种以更通用、更少类型安全的方式操作数据的途径。
>
> 一些泛型接口继承了相应的非泛型版本，因此你的类必须同时实现接口的泛型和非泛型版本。例如，泛型`IEnumerable<out T>`接口继承了非泛型`IEnumerable`接口。因此，如果你的类实现了`IEnumerable<out T>`，你的类还必须实现`IEnumerable`。
>
> 有时在与其它代码集成时，你可能不得不实现非泛型接口，因为接口的泛型版本根本不存在。在这种情况下，如果接口的任何方法采用或返回`Object`，你将失去编译时类型安全性，并且值类型会发生装箱。你可以通过使用我在本章末尾“使用显式接口方法实现提高编译时类型安全性”一节中描述的技术，在一定程度上缓解这种情况。
