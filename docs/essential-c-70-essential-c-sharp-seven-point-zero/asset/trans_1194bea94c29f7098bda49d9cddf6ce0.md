
*成为*，尽管在这些委托是谓词的情况下，通常将 lambda 运算符读作 *满足* 或 *其中*。你可能会将清单 13.16 中的 lambda 读作“*第一个和第二个，满足第一个小于第二个*”。

与 `null` 字面量类似，匿名函数没有与之关联的类型；相反，其类型由它被转换到的目标类型决定。换句话说，我们之前看到的 lambda 表达式在本质上并非 `Func<`int, int, bool>`（或 `Comparer`）类型，但它们与该类型兼容，并可以被转换为该类型。因此，你无法在匿名方法上使用 `typeof()` 运算符，并且只有在将匿名方法转换为特定类型之后，才能调用 `GetType()`。

表 13.1 提供了有关 lambda 表达式特性的补充说明。

## 表 13.1：Lambda 表达式注意事项与示例

| 陈述 | 示例 |
| :---------- | :-------- |
| Lambda 表达式本身没有类型。因此，无法直接从 lambda 表达式访问任何成员，甚至包括 object 的方法。 | `// ERROR: Operator "." cannot be applied to // operand of type "lambda expression"`\n`string s = ((int x) => x).ToString();` |
| Lambda 表达式没有类型，因此不能出现在 `is` 运算符的左侧。 | `// ERROR: The first operand of an "is" or "as"`\n`// operator may not be a lambda expression or`\n`// anonymous method`\n`bool b = ((int x) => x) is Func<`int, int>;` |
| Lambda 表达式只能转换为兼容的委托类型；在此处，一个返回 `int` 的 lambda 不能转换为表示返回 `bool` 方法的委托类型。 | `// ERROR: lambda expression is not compatible`\n`// with Func<`int, bool>` type`\n`Func<`int, bool>` f = (`int x) => x;` |
| Lambda 表达式没有类型，因此不能用于推断局部变量的类型。 | `// ERROR: Cannot assign lambda expression to`\n`// an implicitly typed local variable`\n`var v = x => x;` |
| 位于 lambda 表达式内部的跳转语句（break, goto, continue）不能用于跳转到 lambda 表达式外部的位置，反之亦然。在此处，lambda 内部的 break 语句将跳转到 lambda 外部的 switch 语句的末尾。 | `// ERROR: Control cannot leave the body of an anonymous method or lambda expression<br>string[] args;<br>Func<string> f;<br>switch(args[0])<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;case "File":<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;f = ( ) =><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (!File.Exists(args[1]))<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return args[1];<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// ...<br>&nbsp;&nbsp;&nbsp;&nbsp;}` |
| 由 lambda 表达式引入的参数和局部变量仅在 lambda 主体内处于作用域中。 | `// ERROR: The name "first" does not exist in the current context<br>Func<int, int, bool> expression =<br>(first, second) => first > second;<br>first++;` |
| 编译器的确定赋值分析无法检测 lambda 表达式中“外部”局部变量的初始化。 | `int number;<br>Func<string, bool> f =<br>text => int.TryParse(text, out number);<br>if (f("1"))<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;// ERROR: Use of unassigned local variable<br>&nbsp;&nbsp;&nbsp;&nbsp;System.Console.Write(number);<br>}` |
| 编译器的确定赋值分析无法检测 lambda 表达式中“外部”局部变量的初始化。 | `int number;<br>Func<int, bool> isFortyTwo =<br>x => 42 == (number = x);<br>if (isFortyTwo(42))<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;// ERROR: Use of unassigned local variable<br>&nbsp;&nbsp;&nbsp;&nbsp;System.Console.Write(number);<br>}` |

## 匿名方法

C# 2.0 不支持 lambda 表达式。相反，C# 2.0 使用一种称为*匿名方法*的语法。匿名方法类似于语句 lambda，但缺少使 lambda 如此紧凑的许多特性。匿名方法必须显式地为每个参数指定类型，并且必须具有语句块。匿名方法在参数列表和代码块之间不使用 lambda 运算符 `->`，而是将关键字 `delegate` 放在参数列表之前，强调匿名方法必须被转换为 `delegate` 类型。清单 13.17 展示了使用匿名方法重写的清单 13.7、13.12 和 13.15 中的代码。

### 清单 13.17：在 C# 2.0 中传递匿名方法

```
// ...
BubbleSort(items,
    delegate(int first, int second)
    {
        return first < second;
    }
);
// ...
```

遗憾的是，在 C# 3.0 及更高版本中定义匿名函数有非常相似的两种方法。

- **指南**
  - 在新代码中**避免**使用匿名方法语法；请优先使用更紧凑的 lambda 表达式语法。

然而，匿名方法支持一个小特性，而 lambda 表达式并不支持：在某些情况下，匿名方法可以完全省略参数列表。

## 高级主题

### 无参数匿名方法

与 lambda 表达式不同，只要匿名方法体不使用任何参数，并且 `delegate` 类型仅需要“值”参数（即，它不需要将参数标记为 `out` 或 `ref`），匿名方法就可以完全省略参数列表。例如，匿名方法表达式 `delegate { return Console.ReadLine() != ";"; }` 可以转换为任何需要返回类型为 `bool` 的委托类型，无论该委托需要多少个参数。这个特性使用频率不高，但你在阅读遗留代码时可能会遇到它。

![](img/ef6a8a417630b222bfb3f3b949facff0_593_0.png)

## 高级主题

### 为什么叫“Lambda”表达式？

匿名方法之所以这样命名是显而易见的：它们看起来非常类似于方法声明，但没有关联的声明名称。但是，“lambda 表达式”中的 lambda 是从哪里来的？

lambda 表达式的概念源自逻辑学家 Alonzo Church 的工作，他在 20 世纪 30 年代发明了一种称为 lambda 演算的技术来研究函数。在 Church 的记号中，一个接受参数 $x$ 并产生表达式 $y$ 的函数，通过在表达式前加上小希腊字母 lambda 并用点分隔参数和值来表示。C# 的 lambda 表达式 `x=>y` 在 Church 的记号中表示为 $\lambda x.y$。由于在 C# 程序中使用希腊字母不方便，且点在 C# 中已有许多含义，C# 的设计者选择了使用“胖箭头”记号而不是原始记号。Lambda 表达式的名称表明，匿名函数概念的理论基础是基于 lambda 演算，即使文本中实际上没有 lambda 字母出现。

## 委托不具有结构相等性

.NET 中的委托类型不表现出**结构相等性**。也就是说，你无法将一个委托类型对象的引用转换为不相关的委托类型，即使两个委托的正式参数和返回类型都相同。例如，即使两个委托类型都表示接受两个 int 参数并返回 `bool` 的方法，你也无法将 `Comparer` 的引用分配给类型为 `Func<int, int, bool>` 的变量。不幸的是，当需要使用结构相同但不相关的委托类型时，使用给定类型委托的唯一方法是

