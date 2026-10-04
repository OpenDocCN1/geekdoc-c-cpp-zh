

# 使用委托回调静态方法

现在你已经理解了 `Counter` 方法的设计及其工作原理，让我们看看如何使用委托来调用静态方法。上一个代码示例中出现的 `StaticDelegatedDemo` 方法是本节的重点。

`StaticDelegatedDemo` 方法调用 `Counter` 方法，并在第三参数中传递了 `null`，这对应于 `Counter` 的 `fb` 参数。由于 `Counter` 的 `fb` 参数接收到 `null`，因此生成的每个项目都不会调用任何回调。

接下来，`StaticDelegatedDemo` 方法调用了两次 `Counter`，在方法调用的第三参数中传递了一个新的 `Feedback` 委托对象。该委托对象是方法的包装器，允许通过包装器间接调用该方法。在这个示例中，静态方法的名称 `Program.FeedbackToConsole` 被传递给 `Feedback` 委托的构造函数，表示它是要封装的方法。从 `new` 操作符返回的引用被作为第三个参数传递给 `Counter`。现在当 `Counter` 执行时，它将为序列中的每个项目调用 `Program` 类型的静态 `FeedbackToConsole` 方法。`FeedbackToConsole` 只是将一个字符串写入控制台，指示正在处理的项目。

> 注意：`FeedbackToConsole` 方法定义在 `Program` 类型内部为私有，但 `Counter` 方法能够调用 `Program` 的私有方法。在这种情况下，你可能预计不会出现问题，因为 `Counter` 和 `FeedbackToConsole` 都定义在同一个类型中。然而，即使 `Counter` 方法定义在另一个类型中，这段代码也能正常工作。简而言之，只要创建委托对象的类具有足够的安全/访问权限，一个类型通过委托拥有调用另一个类型私有成员的代码就不属于安全或访问违规行为。

`StaticDelegatedDemo` 方法中对 `Counter` 的第三次调用与第二次调用几乎相同。唯一的区别是 `Feedback` 委托对象封装了静态的 `Program`，而 `FeedbackToMsgBox` 构建了一个指示正在处理的项目的字符串。该字符串将显示在消息框中。

此示例中的所有内容都是类型安全的。例如，在构造 `Feedback` 委托对象时，编译器确保 `Program` 的 `FeedbackToConsole` 和 `FeedbackToMsgBox` 方法的签名与 `Feedback` 委托定义的签名兼容。具体来说，这两个方法都必须有一个参数（`Int32`），并且两个方法都具有相同的返回类型（`void`）。如果 `FeedbackToConsole` 定义如下：

```csharp
private static Boolean FeedbackToConsole(String value) {
    ...
}
```

那么 C# 编译器将无法编译代码并发出以下错误：error CS0123: No overload for 'FeedbackToConsole' matches delegate 'Feedback'。

C# 和 CLR 在将方法绑定到委托时，都允许引用类型的协变（covariance）和逆变（contra-variance）。协变意味着方法可以返回派自委托返回类型的派生类型。逆变意味着方法可以接受一个作为委托返回类型基类的参数。例如，给定一个如下所示定义的委托：

```csharp
delegate Object Callback(FileStream s);
```

它可以构造此委托类型的实例，并将其绑定到原型所示的方法。

```csharp
String SomeMethod(Stream s);
```

在这里，`SomeMethod` 的返回类型（`String`）是派自委托返回类型（`Object`）的类型；这种协变是允许的。`SomeMethod` 的参数类型（`Stream`）是委托参数类型（`FileStream`）的基类；这种逆变也是允许的。

注意，协变和逆变仅支持引用类型，不支持值类型或 `void`。因此，例如，我不能将以下方法绑定到 `MyCallback` 委托。

```csharp
Int32 SomeMethod(Stream s);
```

尽管 `SomeMethod` 的返回类型（`Int32`）派自 `MyCallback` 的返回类型（`Object`），但这种形式的协变是不允许的，因为 `Int32` 是值类型。值类型和 `void` 不能用于协变或逆变的原因是它们的内存结构，而引用类型的内存结构始终是一个指针。幸运的是，如果你尝试这样做，C# 编译器将产生错误。

# 使用委托调用实例方法

我已经解释了如何使用委托调用静态方法，但委托方法的调用特定对象的实例方法。要要原理，请查看本章开头代码中的 `InstanceDelegateMethod`。

注意 `InstanceDelegateMethod` 中构造了一个 `Program` 对象 `p`。这个 `Program` 对象没有任何实例字段或属性；我仅仅是为了演示而创建它。当在调用 `Counter` 方法时构造新的委托对象时，其构造函数传递了 `p.FeedbackToFile`。这导致委托封装了对 `FeedbackToFile` 方法的引用，该方法是一个实例方法（而不是静态方法）。当 `Counter` 调用其 `fb` 参数标识的回调方法时，`FeedbackToFile` 实例方法被调用，最近构造的对象 `p` 的地址将作为隐式的 `this` 参数传递给该实例方法。

`FeedbackToFile` 方法的工作方式类似于 `FeedbackToConsole` 和 `FeedbackToMsg` 方法，它在文件末尾追加字符串。（你可以在应用程序的 AppBase 目录中找到该状态文件。）再次，此示例的目的是演示委托可以封装实例方法。对于实例方法，委托需要知道它所操作的实例。封装实例方法是有用的，因为委托内部的代码可以访问实例成员。

# 揭秘委托

从表面上看，委托似乎易于使用：你使用 `delegate` 关键字定义它们，使用 `new` 操作符构造实例，并使用熟悉的方法语法调用它们。然而，实际情况比示例说明的要复杂。编译器和 CLR 做了很多底层工作。在本节中，我将重点关注编译器和 CLR 如何协作工作。拥有这些知识将提高对委托的理解。让我们重新检查这行代码：

```csharp
internal delegate void Feedback(Int32);
```

当编译器看到这一行时，它实际上定义了一个类似于这样的类：

```csharp
internal class Feedback : System.MulticastDelegate {
  // 构造函数
  public Feedback(Object object, IntPtr method);

  // 与代码指定的相同的的方法
  public virtual void Invoke(Int32 value);

  // 允许异步调用回调
  public virtual AsyncResult BeginInvoke(Int32 value, AsyncCallback callback, Object object);
  public virtual void EndInvoke(IAsyncResult result);
}
```

在这个示例中，编译器定义了一个类 `Feedback`，它派生自类库（FCL）中定义的 `System.MulticastDelegate` 类型。

由于所有委托类型都派自 `MulticastDelegate`，它们继承了 `MulticastDelegate` 的字段、属性和方法。在所有成员中，三个非公有字段可能是最重要的。表 17-1 描述了这些重要字段。

