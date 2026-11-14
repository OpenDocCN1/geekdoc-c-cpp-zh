

var small = from int item in collection
where item < 5
select item;

```
var small2 = collection.Cast<int>().Where(item => item < 5).
Select(n => n);
```

该查询生成与上面最后一行代码相同的方法调用。在这两种情况下，Cast<T> 方法都会将序列中的每个项转换为目标类型。Enumerable.Cast<T> 方法使用旧式强制转换，而不是 as 运算符。使用旧式强制转换意味着 Cast<T> 不需要类约束。使用 as 运算符会有所限制，与其实现不同的 Cast<T> 方法，BCL 团队选择创建一个使用旧式强制转换运算符的单一方法。这是你在代码中也应该考虑的一种权衡。在那些需要将对象转换为泛型类型参数之一的场合，你需要权衡类约束的必要性与使用强制转换运算符的不同行为。

在 C# 4.0 中，通过使用 dynamic 和运行时类型检查，可以进一步绕过类型系统。这是第 5 章“C# 中的动态编程”的主题。有相当多的方法可以基于对已知行为的预期来处理对象，而无需了解特定类型或接口的任何信息。你将学习何时使用这些技术以及何时避免使用它们。

良好的面向对象实践表明，你应该避免转换类型，但有时没有其他选择。如果无法避免转换，请使用语言的 as 和 is 运算符来更清晰地表达你的意图。不同的强制类型转换方式有不同的规则。is 和 as 运算符几乎总是正确的语义，并且仅在被测试的对象是正确类型时才会成功。优先使用这些语句，而不是强制转换运算符，因为后者可能会产生意外的副作用，并在你最意想不到的时候成功或失败。

## 条目 4：使用条件特性而非 #if

#if/#endif 块已被用于从同一源代码生成不同的生成版本，最常见的是调试和发布变体。但这些从来都不是我们乐于使用的工具。#if/#endif 块太容易被滥用，导致代码难以理解且更难以调试。语言设计师通过为不同环境生成不同机器代码的更好工具来回应这一问题。C# 添加了 Conditional 特性，以指示方法是否应根据环境设置进行调用。与 #if/#endif 相比，这是一种更清晰的描述条件编译的方式。编译器理解 Conditional 特性，因此在应用条件特性时，它可以更好地验证代码。条件特性在方法级别应用，因此它迫使你将条件代码分离到不同的方法中。在创建条件代码块时，请使用 Conditional 特性而不是 #if/#endif 块。

大多数资深程序员都使用过条件编译来检查对象中的前置条件和后置条件。你会编写一个私有方法来检查所有类和对象不变量。该方法会被条件编译，因此仅出现在调试生成中。

```
private void CheckStateBad()
{
    // The Old way:
    #if DEBUG
    Trace.WriteLine("Entering CheckState for Person");

    // Grab the name of the calling routine:
    string methodName =
        new StackTrace().GetFrame(1).GetMethod().Name;

    Debug.Assert(LastName != null,
        methodName,
        "Last Name cannot be null");

    Debug.Assert(LastName.Length > 0,
        methodName,
        "Last Name cannot be blank");

    Debug.Assert(FirstName != null,
        methodName,
        "First Name cannot be null");

    Debug.Assert(FirstName.Length > 0,
        methodName,
        "First Name cannot be blank");

    Trace.WriteLine("Exiting CheckState for Person");
#endif
}
```

使用 #if 和 #endif 预处理指令，你在发布生成中创建了一个空方法。CheckState() 方法在所有生成版本（发布和调试）中都会被调用。它在发布生成中不执行任何操作，但你需要为方法调用付出代价。你还需要为加载和 JIT 空例程付出少量代价。

这种做法虽然可行，但可能导致仅在发布生成中出现的微妙错误。以下常见错误展示了使用预处理指令进行条件编译时可能发生的情况：

```
public void Func()
{
    string msg = null;

#if DEBUG
    msg = GetDiagnostics();
#endif
    Console.WriteLine(msg);
}
```

在调试生成中一切正常，但发布生成会愉快地打印一条空白消息。这不是你的意图。你出错了，但编译器无法帮助你。你在条件块中放置了对逻辑至关重要的代码。在源代码中到处撒上 #if/#endif 块，会使得诊断不同生成版本之间的行为差异变得困难。

C# 有一个更好的替代方案：条件特性。使用条件特性，你可以隔离那些仅在特定环境变量定义或设置为某个值时才应成为类一部分的函数。此功能最常见的用途是使用调试语句对代码进行插装。.NET Framework 库已经具备你为此目的所需的基本功能。此示例展示了如何使用 .NET Framework 库中的调试功能，向你展示条件特性的工作原理以及何时将它们添加到代码中。

在生成 Person 对象时，你添加一个方法来验证对象不变量：

```
private void CheckState()
{
    // Grab the name of the calling routine:
    string methodName =
        new StackTrace().GetFrame(1).GetMethod().Name;

    Trace.WriteLine("Entering CheckState for Person:");
    Trace.WriteLine("\tcalled by ");
    Trace.WriteLine(methodName);

    Debug.Assert(LastName != null,
        methodName,
        "Last Name cannot be null");

    Debug.Assert(LastName.Length > 0,
        methodName,
        "Last Name cannot be blank");

    Debug.Assert(FirstName != null,
        methodName,
        "First Name cannot be null");

    Debug.Assert(FirstName.Length > 0,
        methodName,
        "First Name cannot be blank");

    Trace.WriteLine("Exiting CheckState for Person");
}
```

你在这个方法中可能没有遇到过多库函数，因此让我们简要地过一遍。StackTrace 类使用反射获取调用方法的名称。它相当昂贵，但大大简化了诸如收集程序流信息等任务。在这里，它确定了名为 CheckState 的方法。如果调用方法被内联，这里存在微小风险，但替代方案是让每个调用 CheckState() 的方法使用 MethodBase.GetCurrentMethod() 传入方法名称。你很快就会明白我为何决定不采用该策略。

其余方法属于 System.Diagnostics.Debug 类或 System.Diagnostics.Trace 类。Debug.Assert 方法测试一个条件，如果该条件为 false，则停止程序。其余参数定义了在条件为 false 时将打印的消息。Trace.WriteLine 将诊断消息写入调试控制台。因此，如果 person 对象无效，此方法会写入消息并停止程序。你会在所有公共方法和属性中作为前置条件和后置条件调用此方法：

```
public string LastName
{
    get
    {
        CheckState();
        return lastName;
    }
    set
    {
        CheckState();
        LastName = value;
        CheckState();
    }
}
```

当有人第一次尝试将姓氏设置为空字符串或 null 时，CheckState 会触发断言。然后你修复 set 访问器以检查用于 LastName 的参数。它正在做你想要的事情。但是，每个公共例程中的这种额外检查需要时间。你只希望在创建调试生成时包含这种额外检查。这就是条件特性派上用场的地方：

```
[Conditional("DEBUG")]
private void CheckState()
{
    // same code as above
}
```

条件特性告诉 C# 编译器，仅当编译器检测到 DEBUG 环境变量时才应调用此方法。条件特性不影响 CheckState() 函数生成的代码；它修改对该函数的调用。如果定义了 DEBUG 符号，你会得到这个：

