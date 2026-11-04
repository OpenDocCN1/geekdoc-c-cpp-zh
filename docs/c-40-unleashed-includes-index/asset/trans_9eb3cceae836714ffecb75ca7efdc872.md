
instance. 如果我们现在调用 Apple 特定的 Peel 方法，事情就会出错：能够在对象上调用一个该对象不可用的方法，是对系统类型安全的破坏。你不想尝试剥开一颗椰子！

问题出在哪里？看起来在每一步编译器都得出了正确的结论。这里的根本问题在于允许数组类型被协变地处理，如第二行所示。这是否意味着 CLR 可以被欺骗以破坏类型安全？幸运的是，没有，因为设计者意识到了这个确切的问题并引入了运行时检查来防止它。其结果是第三行代码会抛出 ArrayTypeMismatchException，如图 15.36 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_773_0.png)

图 15.36 CLR 会防止向数组中插入类型不正确的元素。

## 他们知道吗？

如果设计者知道数组协变是一种不安全的操作，为什么一开始还要允许它？如常，知道一些历史有助于提供良好的解释。回想一下 CLR 是怀着跨语言互操作性的目标被发明的。CLR 创建时期的一个流行语言是 Java，其中损坏的数组协变已被允许很久了。为了使 Java 代码能够在 CLR 上运行（例如使用 J#）而不产生编译时错误，决定让数组协变。

正如你所能想象的，这个设计上就损坏的选择在设计小组内部是一个热议话题，但最终，跨语言互操作性的目标被认为重要到足以推动数组协变的引入。幸运的是，泛型在方差方面做得好得多，如你接下来所见。

## 安全保证

协变和逆变是增加类型系统灵活性的手段，理想情况下同时确保类型安全不会被违反。灵活性部分很清楚：能够把一个 Apple 数组当作 Coconut 数组处理，比不能这样做更有力量。

但为什么这个数组协变的例子不安全？真正的答案在于数组的可写特性：

```csharp
// We're putting a Coconut, which is a Fruit, in a Fruit-array. This is
// actually not fine if the underlying array has a more specific element type.
fruits[2] = new Coconut();
```

如果 fruits 变量引用的是元素类型比 Fruit 更具体的数组，那么前面的代码就不合适。原因是有个人可能会使用更具体的元素类型（在我们的例子中是 Apple）查看同一个数组，观察到一个不兼容类型的对象被放了进去。协变和输入是敌人。

假设我们有只能读取元素的数组（我们没有），协变可以以安全的方式被允许：

```csharp
Apple[] apples = new Apple[] { apple1, apple2, apple3 };

// Because of array type covariance we can write the following.
readonly /* hypothetical keyword use */ Fruit[] fruits = apples;

// Reading from the array is a safe operation.
Fruit fruit1 = fruits[0];

// This wouldn't compile anymore, because the array is read-only!
fruits[2] = new Coconut();
```

事实上，数组使用协变的能力并非全无好处。想想你想要打印一个 Fruit 对象数组的情况。如果用户不能把一个 Apple 对象数组交给你，这个好意的 方法就没什么用处。这个方法可以安全实现的原因是它只会从输入数组中读取。正如你将看到的，使用 IEnumerable<Fruit> 作为参数类型会是更好的选择，因为该接口对协变是安全的。

协变在概念上类似于将函数的输出视为更不派生的类型。例如，即使 Console.ReadLine 给我返回一个 string，我把它看作不过是一个 object 也没问题：

```csharp
object input = Console.ReadLine();
```

在方法调用的领域再停留一小会儿，我们可以问自己逆变对应什么。直觉上，你可以猜到它应该与输入参数有关。当一个方法期望某种类型的对象时，给它一个更派生类型的对象是可以的。例如，接收两个 Fruit 对象的 方法可以安全地传入一个 Apple 和一个 Coconut：

```csharp
Yogurt appleAndCoconut = CreateFruitYogurt(apple, coconut); // Yum?
```

## 泛型协变和逆变

让我们更仔细地看看泛型接口类型上的协变和逆变。本章开始时，你看到下面的代码在 .NET 3.5 中无法编译，假设 MakeJuice 接收一个 IEnumerable<Fruit>：

```csharp
IEnumerable<Apple> apples = ...;
var juice = MakeJuice(from apple in apples
                    where apple.Color == Color.Red
                    select apple);
```

原因在于 IEnumerable<T> 在其类型参数 T 上是不变的。不变性简单地意味着在类型 IEnumerable<Base> 和 IEnumerable<Derived> 之间没有建立类型关系。它们被视为彼此无关。

在 .NET 4 中，IEnumerable<T> 通过在类型参数 T 上放置 out 关键字被标记为协变：

```csharp
public interface IEnumerable<out T> : IEnumerable {
    IEnumerator<T> GetEnumerator();
}
```

通过使用 out 关键字，你向编译器承诺只在输出位置使用泛型参数。以 IEnumerable<T> 为例，这就是因为 T 只在 GetEnumerator 的返回类型中使用。反过来，IEnumerator<T> 需要被声明为协变：

```csharp
public interface IEnumerator<out T> : IDisposable, IEnumerator {
    T Current { get; }
}
```

同样，T 只出现在输出位置，作为 get-only 属性的返回类型。在接口使用者一方，这意味着 IEnumerable<Derived> 可以安全地赋给 IEnumerable<Base>。例如，使用 Apples 和 Coconuts：

```csharp
IEnumerable<Apple> apples = new Apple[] { apple1, apple2, apple3 };

// Because of IEnumerable<T>'s covariance we can write the following.
IEnumerable<Fruit> fruits = apples;

// There is no way to put a Coconut in an IEnumerable<Fruit>, hence this does
// not work anymore:    fruits[2] = new Coconut();
```

如果你将类型参数标记为协变但在输入位置如方法参数或非 get-only 的属性中使用它，编译器会抱怨（参见图 15.37 的方差违规错误消息）：

```csharp
interface IArray<out T> {
    T this[int index] {
        get; // This is fine
        set; // Having a setter is not fine!
    }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_776_0.png)

图 15.37 对泛型类型参数协变安全使用的违反。

逆变与协变完全相反，但对大多数人来说不太直观。协变类型参数只能在输出位置使用，而逆变类型参数只能在输入位置使用，如 in 关键字所示。一个很好的例子可以在 IComparer<T> 接口上找到：

```csharp
public interface IComparer<in T> {
    int Compare(T first, T second);
}
```

这里，T 只作为 Compare 方法的输入参数使用。从使用者的角度看，逆变允许写下以下内容：

```csharp
IComparer<Fruit> compareFruits = new CompareFruitBySize();
IComparer<Apple> compareApples = compareFruits;
```

如果一个对象可以比较两个 Fruit 对象，它就可以在需要比较两个 Apple 对象的地方使用。当然，我们不会使用 Apple 的特定属性来进行比较，但将 Apple 当作 Fruit 进行比较是安全的。这完全类似于如果一个基于 Fruit 的 Compare 方法被调用时传入两个 Apple 对象所能实现的情况：

```csharp
public int Compare(Fruit first, Fruit last) {
    return first.Size - last.Size;
}
...
int res = Compare(apple1, apple2); // Fine for method overload resolution
```

当将类型参数标记为逆变时，在输出位置使用它是一个错误，编译器会阻止你犯这个错误。

## 为什么方差不会被自动推断

你可能会想知道为什么在定义泛型接口或委托类型时，使用 in 和 out 关键字的方差注释必须显式提供。（方差仅支持这两种泛型类型。）毕竟，似乎编译器本可以自己弄明白：如果泛型参数只在输入位置使用，它就变成逆变（in），而当它只出现在输出位置时，它就变成协变（out）。

原因在于泛型类型在开发过程中可能仍在演进，而其他代码可能开始依赖使用该类型的对象以协变或逆变方式使用。一旦类型被扩展（例如向接口添加方法），方差注释可能会静默消失，因为类型参数现在也在“相反”位置使用，使得类型变为不变。这会导致依赖先前推断方差的代码开始失效。出于这个原因，语言要求你明确说明预期的方差注释。如果没有方差修饰符，类型参数将被视为不变（就像在 C# 4.0 之前一样）。

关于表观子类型化与协变和逆变使用的关系示意概述，显示在图 15.38 中。

## 底层实现

接口和委托类型的协变和逆变自 .NET 2.0 时代引入泛型以来就一直被 CLR 支持。并且在运行时和 IL 级别得到支持使其再次适用于跨语言支持。给定以下两种类型，让我们看看底层实现：

```csharp
interface IReadOnly<out T> {
    T Give();
}
```

```csharp
interface IWriteOnly<in T> {
    void Take(T input);
}
```
