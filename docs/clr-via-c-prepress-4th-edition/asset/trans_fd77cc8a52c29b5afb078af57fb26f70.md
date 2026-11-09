
```csharp
Counter(1, 3, new Feedback(p.FeedbackToFile));

Console.WriteLine();
}

private static void ChainDelegateDemo1(Program p) {
    Console.WriteLine("----- Chain Delegate Demo 1 -----");
    Feedback fb1 = new Feedback(FeedbackToConsole);
    Feedback fb2 = new Feedback(FeedbackToMsgBox);
    Feedback fb3 = new Feedback(p.FeedbackToFile);

    Feedback fbChain = null;
    fbChain = (Feedback) Delegate.Combine(fbChain, fb1);
    fbChain = (Feedback) Delegate.Combine(fbChain, fb2);
    fbChain = (Feedback) Delegate.Combine(fbChain, fb3);
    Counter(1, 2, fbChain);

    Console.WriteLine();
    fbChain = (Feedback)
        Delegate.Combine(fbChain, new Feedback(FeedbackToMsgBox));
    Counter(1, 2, fbChain);
}

private static void ChainDelegateDemo2(Program p) {
    Console.WriteLine("----- Chain Delegate Demo 2 -----");
    Feedback fb1 = new Feedback(FeedbackToConsole);
    Feedback fb2 = new Feedback(FeedbackToMsgBox);
    Feedback fb3 = new Feedback(p.FeedbackToFile);

    Feedback fbChain = null;
    fbChain += fb1;
    fbChain += fb2;
    fbChain += fb3;
    Counter(1, 2, fbChain);

    Console.WriteLine();
    fbChain -= new Feedback(FeedbackToMsgBox);
    Counter(1, 2, fbChain);
}

private static void Counter(Int32 from, Int32 to, Feedback fb) {
    for (Int32 val = from; val <= to; val++) {
        // If any callbacks are specified, call them
        if (fb != null)
            fb(val);
    }
}

private static void FeedbackToConsole(Int32 value) {
    Console.WriteLine("Item=" + value);
}

private static void FeedbackToMsgBox(Int32 value) {
    MessageBox.Show("Item=" + value);
}

private void FeedbackToFile(Int32 value) {
    using (StreamWriter sw = new StreamWriter("Status", true)) {
        sw.WriteLine("Item= " + value);
    }
}
}
```

现在我来描述这段代码在做什么。在顶部，请注意内部委托 Feedback 的声明。委托指示回调方法的签名。在此示例中，Feedback 委托标识一个接受一个参数（Int32）并返回 void 的方法。在某种程度上，委托非常像表示函数地址的非托管 C/C++ typedef。

Program 类定义了一个名为 Counter 的私有静态方法。此方法从 from 参数计数到 to 参数。Counter 方法还接受一个 fb，它是对 Feedback 委托对象的引用。Counter 遍历所有整数，并且对于每个整数，如果 fb 变量不为 null，则调用（由 fb 变量指定的）回调方法。此回调方法会接收正在处理的项的值，即项号。回调方法可以设计和实现为以任何认为合适的方式处理每一项。

## 使用委托回调静态方法

现在你已经理解了 Counter 方法是如何设计的以及它如何工作，让我们看看如何使用委托来回调静态方法。上一代码示例中出现的 StaticDelegateDemo 方法是本节的重点。

StaticDelegateDemo 方法调用 Counter 方法，在第三个参数中传入 null，该参数对应于 Counter 的 fb 参数。由于 Counter 的 fb 参数接收到 null，因此处理每一项时不会调用任何回调方法。

接下来，StaticDelegateDemo 方法第二次调用 Counter，在方法调用的第三个参数中传入一个新构造的 Feedback 委托对象。此委托对象是方法的包装器，允许通过该包装器间接调用该方法。在此示例中，静态方法 Program.FeedbackToConsole 的名称被传递给 Feedback 类型的构造函数，指示它就是要被包装的方法。从 new 运算符返回的引用被作为第三个参数传递给 Counter。现在，当 Counter 执行时，它会为该系列中的每一项调用 Program 类型的静态 FeedbackToConsole 方法。FeedbackToConsole 只是向控制台写入一个字符串，指示正在处理的项。

**注意** FeedbackToConsole 方法在 Program 类型内部被定义为 private，但 Counter 方法能够调用 Program 的私有方法。在这种情况下，你可能不会预期有问题，因为 Counter 和 FeedbackToConsole 都定义在同一类型中。然而，即使 Counter 方法定义在另一个类型中，这段代码也能正常工作。简而言之，只要委托对象是由具有足够安全/可访问性的代码创建的，一个类型拥有通过委托调用另一个类型私有成员的代码，并不构成安全性或可访问性违规。

StaticDelegateDemo 方法中对 Counter 的第三次调用与第二次调用几乎相同。唯一的区别是，Feedback 委托对象包装的是静态方法 Program.FeedbackToMsgBox。FeedbackToMsgBox 构建一个指示正在处理的项的字符串。然后，此字符串会显示在消息框中。

此示例中的所有内容都是类型安全的。例如，在构造 Feedback 委托对象时，编译器会确保 Program 的 FeedbackToConsole 和 FeedbackToMsgBox 方法的签名与 Feedback 委托定义的签名兼容。具体而言，两个方法都必须接受一个参数（Int32），并且两个方法都必须具有相同的返回类型（void）。如果 FeedbackToConsole 被定义成这样：

```csharp
private static Boolean FeedbackToConsole(String value) {
   ...
}
```

C# 编译器将不会编译代码，并会发出以下错误：“错误 CS0123: 没有与委托‘Feedback’匹配的‘FeedbackToConsole’重载。”

在将方法绑定到委托时，C# 和 CLR 都允许引用类型进行协变和逆变。协变意味着方法可以返回一个派生自委托返回类型的类型。逆变意味着方法可以接受一个作为委托参数类型基类的参数。例如，给定这样定义的委托：

```csharp
delegate Object MyCallback(FileStream s);
```

可以构造此委托类型的实例，并将其绑定到像这样声明原型的方法：

```csharp
String SomeMethod(Stream s);
```

这里，SomeMethod 的返回类型（String）是派生自委托返回类型（Object）的类型；这种协变是允许的。SomeMethod 的参数类型（Stream）是委托参数类型（FileStream）的基类；这种逆变是允许的。

请注意，协变和逆变仅支持引用类型，不支持值类型或 void。因此，例如，我不能将以下方法绑定到 MyCallback 委托：

```csharp
Int32 SomeOtherMethod(Stream s);
```

尽管 SomeOtherMethod 的返回类型（Int32）派生自 MyCallback 的返回类型（Object），但不允许这种形式的协变，因为 Int32 是值类型。显然，值类型和 void 不能用于协变和逆变的原因是，这些事物的内存结构会变化，而引用类型的内存结构始终是一个指针。幸运的是，如果你尝试执行不受支持的操作，C# 编译器会产生错误。

## 使用委托回调实例方法

我刚才解释了如何使用委托回调静态方法，但委托也可以用于调用特定对象的实例方法。要理解回调实例方法如何工作，请看本章开头所示代码中出现的 `InstanceDelegateDemo` 方法。

请注意，在 `InstanceDelegateDemo` 方法中构造了一个名为 p 的 Program 对象。此 Program 对象没有任何关联的实例字段或属性；我创建它仅仅是为了演示目的。在调用 Counter 方法时构造新的 Feedback 委托对象，其构造函数会接收 p.FeedbackToFile。这会使委托包装对 FeedbackToFile 方法的引用，而该方法是一个实例方法（不是静态方法）。当 Counter 调用由其 fb 参数标识的回调方法时，会调用 FeedbackToFile 实例方法，并且最近构造的对象 p 的地址将作为隐式 this 参数传递给该实例方法。

FeedbackToFile 方法的工作方式与 FeedbackToConsole 和 FeedbackToMsgBox 方法类似，不同之处在于它会打开一个文件并将字符串追加到文件末尾。（该方法创建的 Status 文件可以在应用程序的 AppBase 目录中找到。）

同样，此示例的目的是演示委托既可以包装对实例方法的调用，也可以包装对静态方法的调用。对于实例方法，委托需要知道该方法将要操作的对象实例。包装实例方法很有用，因为对象内部的代码可以访问该对象的实例成员。这意味着对象可以具有某种状态，该状态可以在回调方法执行其处理时使用。

## 揭秘委托

从表面上看，委托似乎很容易使用：使用 C# 的 delegate 关键字定义它们，使用熟悉的 new 运算符构造它们的实例，并使用熟悉的方法调用语法调用回调（只是使用方法名时，你使用的是引用委托对象的变量）。

然而，实际发生的情况比前面示例所展示的要复杂得多。编译器和 CLR 做了大量幕后处理来隐藏这种复杂性。在本节中，我将重点介绍编译器和 CLR 如何协同工作来实现委托。掌握这些知识将增进你对委托的理解，并教会你如何高效且有效地使用它们。我还会简要介绍委托提供的一些附加功能。

让我们从重新审视这行代码开始：

```csharp
internal delegate void Feedback(Int32 value);
```
