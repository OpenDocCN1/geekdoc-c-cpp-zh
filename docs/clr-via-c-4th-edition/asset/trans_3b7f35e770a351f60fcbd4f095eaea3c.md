
这里有一个例子，应该能真正帮助我把观点讲清楚。

```csharp
private static Object OneStatement(Stream stream, char charToFind) {
    return (charToFind + ": " + stream.GetType() + String.Empty + (stream.Position + 512M))
        .Where(c=>c == charToFind).ToArray();
}
```

这个略显刻意的方法中只包含一条 C# 语句，但这条语句做了大量工作。实际上，下面是 C# 编译器为此方法生成的中间语言（IL）。（我把其中一些由于正在发生的隐式操作而可能成为故障点的行标成了粗斜体。）

```il
.method private hidebysig static object OneStatement(
        class [mscorlib]System.IO.Stream stream, char charToFind) cil managed {
    .maxstack 4
    .locals init (
        [0] class Program/<>c__DisplayClass1 V_0,
        [1] object[] V_1)
    IL_0000:  newobj    instance void Program/<>c__DisplayClass1::.ctor()
    IL_0005:  stloc.0
    IL_0006:  ldloc.0
    IL_0007:  ldarg.1
    IL_0008:  stfld     char Program/<>c__DisplayClass1::charToFind
    IL_000d:  ldc.i4.5
    IL_000e:  newarr    [mscorlib]System.Object
    IL_0013:  stloc.1
    IL_0014:  ldloc.1
    IL_0015:  ldc.i4.0
    IL_0016:  ldloc.0
    IL_0017:  ldfld     char Program/<>c__DisplayClass1::charToFind
    IL_001c:  box       [mscorlib]System.Char
    IL_0021:  stelem.ref
    IL_0022:  ldloc.1
    IL_0023:  ldc.i4.1
    IL_0024:  ldstr     ": "
    IL_0029:  stelem.ref
    IL_002a:  ldloc.1
    IL_002b:  ldc.i4.2
    IL_002c:  ldarg.0
    IL_002d:  callvirt  instance class [mscorlib]System.Type [mscorlib]System.Object::GetType()
    IL_0032:  stelem.ref
    IL_0033:  ldloc.1
    IL_0034:  ldc.i4.3
    IL_0035:  ldsfld    string [mscorlib]System.String::Empty
    IL_003a:  stelem.ref
    IL_003b:  ldloc.1
    IL_003c:  ldc.i4.4
    IL_003d:  ldarg.0
    IL_003e:  callvirt  instance int64 [mscorlib]System.IO.Stream::get_Position()
    IL_0043:  call      valuetype [mscorlib]System.Decimal
                                 [mscorlib]System.Decimal::op_Implicit(int64)
    IL_0048:  ldc.i4     0x200
    IL_004d:  newobj    instance void [mscorlib]System.Decimal::.ctor(int32)
    IL_0052: call valuetype [mscorlib]System.Decimal [mscorlib]System.Decimal::op_Addition
               (valuetype [mscorlib]System.Decimal, valuetype [mscorlib]System.Decimal)
    IL_0057: box [mscorlib]System.Decimal
    IL_005c: stelem.ref
    IL_005d: ldloc.1
    IL_005e: call string [mscorlib]System.String::Concat(object[])
    IL_0063: ldloc.0
    IL_0064: ldftn instance bool Program/<>c__DisplayClass1::<OneStatement>b__0(char)
    IL_006a: newobj instance
               void [mscorlib]System.Func`2<char, bool>::.ctor(object, native int)
    IL_006f: call class [mscorlib]System.Collections.Generic.IEnumerable`1<!!0>
               [System.Core]System.Linq.Enumerable::Where<char>(
               class [mscorlib]System.Collections.Generic.IEnumerable`1<!!0>,
               class [mscorlib]System.Func`2<!!0, bool>)
    IL_0074: call !!0[] [System.Core]System.Linq.Enumerable::ToArray<char>(
               class [mscorlib]System.Collections.Generic.IEnumerable`1<!!0>)
    IL_0079: ret
}
```

如你所见，在构造 <>c__DisplayClass1 类（一个编译器生成类型）、Object[] 数组、Func 委托，以及对 char 和 Decimal 进行装箱时，都可能发生 OutOfMemoryException。调用 Concat、Where 和 ToArray 时，内部也会分配内存。构造 Decimal 实例可能导致其类型构造器被调用，从而引发 TypeInitializationException。此外，还有对 Decimal 的 op_Implicit 运算符及其 op_Addition 运算符方法的隐式调用，这些调用可能做任何事，包括抛出 OverflowException。

查询 Stream 的 Position 属性很有意思。首先，它是一个虚属性，因此我的 OneStatement 方法根本不知道实际会执行什么代码，而那段代码可能抛出任何异常。其次，Stream 派生自 MarshalByRefObject，所以 stream 参数实际上可能引用一个代理对象，而该代理对象又引用另一个 AppDomain 中的对象。另一个 AppDomain 可能已被卸载，因此这里也可能抛出 AppDomainUnloadedException。

当然，所有被调用的方法都是我个人无法控制的方法，因为它们由 Microsoft 生成。而且 Microsoft 完全可能在未来改变这些方法的实现方式，因此它们可能抛出我在编写 OneStatement 方法那天根本不可能知道的新异常类型。我怎么可能把 OneStatement 方法写得对所有可能的失败都完全健壮呢？顺便说一句，反过来也是问题：一个 catch 块可能捕获到派生自指定异常类型的异常，而此时我却在为另一种失败执行恢复代码。

所以，既然你已经了解了所有可能的失败，你大概就能明白为什么不编写真正健壮可靠的代码会在业界成为一种可接受的做法：这根本不切实际。此外，人们也可以说这实际上是不可能的。错误并不频繁发生，这也是它成为一种可接受做法的另一个原因。由于错误（如 OutOfMemoryException）很少发生，社区决定用真正可靠的代码来换取程序员的生产力。

^5 顺便说一句，System.Char、System.String、System.Type 和 System.IO.Stream 都定义了类构造器，它们都可能在此应用程序的某个时刻导致 TypeInitializationException 被抛出。

异常的好处之一是，未处理的异常会导致应用程序终止。这很好，因为在测试期间你会很快发现问题，而且未处理异常提供的信息（错误消息和堆栈跟踪）通常足以让你修复代码。当然，许多公司不希望自己的应用程序在测试和部署后就直接终止，因此很多开发者会插入代码来捕获 System.Exception，即所有异常类型的基类。然而，捕获 System.Exception 并让应用程序继续运行的问题在于，状态可能已经损坏。

本章前面，我展示了一个 Account 类，它定义了一个 Transfer 方法，其职责是从一个账户向另一个账户转账。如果调用这个 Transfer 方法时，它成功地从 From 账户扣除了钱，然后在向 To 账户加钱之前抛出了异常，会怎样？如果调用代码捕获 System.Exception 并继续运行，那么应用程序的状态就损坏了：From 和 To 两个账户中的钱都比应有的少。因为我们这里谈的是钱，这种状态损坏不会只被视为简单的 bug，它肯定会被视为安全漏洞。如果应用程序继续运行，它会尝试在各个账户之间执行更多转账，于是状态损坏就会在应用程序内肆意蔓延。

有人可能会说，Transfer 方法本身应该捕获 System.Exception，并把钱恢复到 From 账户。如果 Transfer 方法足够简单，这也许确实可行。但如果 Transfer 方法要生成取出款项的审计记录，或者有其他线程同时操作同一个账户，那么尝试撤销操作也可能失败，从而抛出另一个异常。这样一来，状态损坏只会变得更糟，而不是更好。

> **注意** 有人可能会说，知道事情*哪里*出了问题，比知道*什么*错误发生了更有用。例如，知道从某个账户转出钱失败了，可能比知道 Transfer 因 SecurityException 或 OutOfMemoryException 等而失败更有用。事实上，Win32 错误模型就是这样工作的：方法返回 true/false 来表示成功/失败，这样你就知道哪个方法失败了。然后，如果你的程序关心失败原因，它会调用 Win32 的 GetLastError 方法。System.Exception 确实有一个 Source 属性，可以告诉你失败的方法。但这个属性是一个 String，你必须解析它；而且如果两个方法内部调用同一个方法，你仅凭 Source 属性无法判断你的代码调用的是哪个方法失败了。相反，你必须解析 Exception 的 StackTrace 属性返回的 String 才能获得这一信息。由于这太难了，我从未见过有人真正写代码这样做。
