

```cs
{
    // 返回一个随机选择的包优先级：
    // 需要 0, 1 或 2（小于 3 的值）。
    int rand = _randGen.Next(3);
    // 使用该值生成一个新的数据包。
    // 将 int 转换为枚举虽然很笨拙，但它可以避免
    // 使用 if 语句或 switch 语句。
    return new Package((Priority)rand);
}
```

`PackageFactory` 类包含一个数据成员和一个方法。（你同样容易地将一个简单的工厂实现为方法而不是类——例如，实现为 `Program` 类中的一个方法。）当你实例化一个 `PackageFactory` 对象时，它会创建一个 `Random` 类的对象并存储在数据成员 `rand` 中。`Random` 是 .NET 库类，用于生成随机数。

![](img/6df7bb88e9302e98442acc219cfbd7fc_198_0.png)

查看 csharp102.info 上的 `PackageFactoryWithIterator` 示例。

## 使用 PackageFactory

要生成一个具有随机优先级的 `Package` 对象，你按照如下方式调用工厂对象的 `CreatePackage()` 方法：

```cs
PackageFactory fact = new PackageFactory();
IPrioritizable pack = fact.CreatePackage(); // 注意这里的接口类型。
```

`CreatePackage()` 告诉它的随机数生成器生成一个 0 到 2（包含）之间的数字，并使用该数字设置新 `Package` 的优先级，然后由方法返回（返回给 `Package` 或者更好地，返回给 `IPrioritizable` 变量）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_198_1.png)

注意，我让 `CreatePackage` 返回 `IPrioritizable` 的引用，这比返回 `Package` 的引用更通用。这个示例展示了**间接性**（indirection）——`Main()` 通过 `Package` 实现的接口间接引用一个 `Package`。间接性使 `Main()` 免受 `CreatePackage` 返回的具体细节的影响。这样你就有更大的自由来更改工厂的底层实现，而不影响 `Main()`。

## 关于工厂的更多信息

![](img/6df7bb88e9302e98442acc219cfbd7fc_198_2.png)

工厂对于生成大量测试数据非常有帮助。（工厂不需要使用随机数——那只是 `PriorityQueue` 示例所需的。）

![](img/6df7bb88e9302e98442acc219cfbd7fc_198_3.png)

工厂通过隔离对象创建来改进程序。每当你在代码中通过名称提到一个特定的类时，你就创建了对该类的依赖。这种依赖越多，你的类之间的耦合（结合在一起）就越紧密。

程序员长期以来知道应该避免紧密耦合。（更解耦的方法之一是通过接口（如 `IPrioritizable`）间接使用工厂，而不是使用具体的类（如 `Package`）。程序员们仍然经常使用 `new` 操作符直接创建对象，这没问题。但工厂可以使代码的耦合度更低——从而更具活性。

## 处理未完成的任务

`PriorityQueue` 需要一些细小的“修补”。以下是待解决的问题：

- `PriorityQueue` 本身不会阻止你尝试对其实例化，例如针对 `int`、`string` 或 `Student`——这些元素没有优先级。你需要约束该类，使其仅能对实现了 `IPrioritizable` 的类型进行实例化。尝试为非 `IPrioritizable` 类实例化应该导致编译错误。

- `PriorityQueue` 的 `Dequeue()` 方法返回的是值 `null` 而不是实际对象。但泛型类型如 `<T>` 并不像 `int`、`string` 和对象引用那样具有自然的默认 `null` 值。那部分也需要泛型化。

## 添加约束

`PriorityQueue` 必须能够询问对象其优先级是什么。为了让其工作，存储在 `PriorityQueue` 中的所有类都必须实现 `IPrioritizable` 接口，就像 `Package` 一样。`Package` 在类声明头部列出了 `IPrioritizable`，如下：

```cs
class Package : IPrioritizable
```

然后它实现了 `IPrioritizable` 的 `Priority` 属性。

`PriorityQueue` 需要一个匹配的限制。你希望在尝试为没有实现 `IPrioritizable` 的类型实例化时，编译器报错。在 `PriorityQueue` 的非泛型形式（假设专门为 `Package` 类型编写）中，当其中一个优先级队列方法尝试调用 `Package` 不具备的方法时，编译器会自动尖叫（我建议带上耳塞）。但对于泛型类，你可以通过显式约束进入更深层次。因为你可以用字面上的任何类型实例化泛型类，所以你需要一种方法告诉编译器哪些类型是可以接受的——因为它们保证拥有正确的方法。

你通过在 `PriorityQueue` 的头部指定 `IPrioritizable` 来添加约束，如下：

```cs
class PriorityQueue<T> where T: IPrioritizable
```

你注意到刚才的 `where` 子句了吗？这个**加粗**的 `where` 子句指定了 `T` 必须实现 `IPrioritizable`。这就是执行者。这意味着：“确保 `T` 实现了 `IPrioritizable` 接口——否则！”

你通过在 `where` 子句中列出以下一个或多个元素（用逗号分隔）来指定约束：

- `T` 必须派生自（或是）的所需的基类名称。
- `T` 必须实现的接口名称。
- 具有无参数构造函数的要求。

| 泛型约束 | 含义 |
| :--- | :--- |
| 基类 (Base class) | T 必须派生自该基类。 |
| 接口 (Interface) | T 必须实现该接口。 |
| new() | T 必须有一个无参数构造函数。 |

![](img/6df7bb88e9302e98442acc219cfbd7fc_200_0.png)

```cs
class PriorityQueue<T> where T: IPrioritizable
{ ... }
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_201_0.png)

```cs
class MyClass<T, U> where T: IPrioritizable, U: new()
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_201_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_201_2.png)

如果你认为 `PriorityQueue` 已经灵活，那么请查看本章节提供的 `ProgrammingToAnInterface` 程序中一个更灵活的版本——并可以在其中遇到一些面向对象的设计原则。

