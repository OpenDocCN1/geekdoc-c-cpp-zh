

## 表 12.1: Lambda 表达式注释和示例

| Statement | Example |
| :--- | :--- |
| C# 不允许在匿名函数中使用跳转语句（break、goto、continue），如果跳转目标位于 Lambda 表达式之外。同样，你也不能从 Lambda 表达式（或匿名方法）之外将跳转语句定向到 Lambda 表达式内部。 | `// ERROR: Control cannot leave the body of an<br>// anonymous method or Lambda expression<br>string[] args;<br>Func<string> expression;<br>switch(args[0])<br>{<br>    case "/File":<br>    expression = () =><br>    {<br>        if (!File.Exists(args[1]))<br>        {<br>            break;<br>        }<br>        // ...<br>        return args[1];<br>    };<br>    // ...<br>}` |
| Lambda 表达式内部引入的变量仅在 Lambda 表达式主体的作用域内可见。 | `// ERROR: The name 'first' does not<br>// exist in the current context<br>Func<int, int, bool> expression =<br>    (first, second) => first > second;<br>first++;` |
| 编译器的流分析无法检测 Lambda 表达式中局部变量的初始化。 | `int number;`<br>`Func<string, bool> expression =`<br>`text => int.TryParse(text, out number);`<br>`if (expression("1"))`<br>`{`<br>`// ERROR: Use of unassigned local variable`<br>`System.Console.Write(number);`<br>`}` |
| | `int number;`<br>`Func<int, bool> isFortyTwo =`<br>`x => 42 == (number = x);`<br>`if (isFortyTwo(42))`<br>`{`<br>`// ERROR: Use of unassigned local variable`<br>`System.Console.Write(number);`<br>`}` |

## 高级主题

### Lambda 表达式和匿名方法的内部实现

Lambda 表达式（和匿名方法）并非 CLR 中的内置构造。相反，C# 编译器在编译时生成其实现。Lambda 表达式为内联声明的委托模式提供了语言构造。因此，C# 编译器为该模式生成实现代码，以便编译器自动编写代码，而无需开发人员手动编写。鉴于前面的示例，因此，C# 编译器生成的 CIL 代码与清单 12.20 中显示的 C# 代码类似。

### 清单 12.20: 编译器为 Lambda 表达式生成的 CIL 的 C# 等效代码

```csharp
class DelegateSample
{
    // ...

    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        for (i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer: ");
            items[i] = int.Parse(Console.ReadLine());
        }

        BubbleSort(items,
            DelegateSample.__AnonymousMethod_00000000());

        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }
    }

    private static bool __AnonymousMethod_00000000(
        int first, int second)
    {
```

```csharp
return first < second;
}
}
```

在此示例中，匿名方法被转换为单独声明的静态方法，然后将其实例化为委托并作为参数传递。

## 外部变量

在 Lambda 表达式之外声明（包括参数）但被 Lambda 表达式捕获（访问）的局部变量，是该 Lambda 的外部变量。this 也是一个外部变量。匿名函数捕获的外部变量会一直存活，直到匿名函数的委托被销毁后。在清单 12.21 中，使用外部变量来计算 BubbleSort() 执行比较的次数相对简单。输出 12.2 显示了此清单的结果。

### 清单 12.21: 在 Lambda 表达式中使用外部变量

```csharp
class DelegateSample
{
    // ...

    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        int comparisonCount=0;

        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }

        BubbleSort(items,
            (int first, int second) =>
            {
                comparisonCount++;
                return first < second;
            }
```

```csharp
});
for (i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}

Console.WriteLine("Items were compared {0} times.",
    comparisonCount);
}
```

### 输出 12.2:

```
Enter an integer:5
Enter an integer:1
Enter an integer:4
Enter an integer:2
Enter an integer:3
5
4
3
2
1
Items were compared 10 times.
```

comparisonCount 出现在 Lambda 表达式之外，并在其中递增。调用 BubbleSort() 方法后，comparisonCount 会打印到控制台。

正如此代码所示，C# 编译器负责生成 CIL 代码，在匿名方法和调用站点之间共享 comparisonCount，尽管在匿名委托中没有传递 comparisonCount 的参数，BubbleSort() 方法中也没有。鉴于变量的共享，它在引用它的委托被垃圾回收之前不会被垃圾回收。换句话说，捕获变量的生命周期至少与捕获它的最长寿命委托对象一样长。

## 高级主题

### 外部变量的 CIL 实现

C# 编译器为外部变量生成的 CIL 代码比简单匿名方法的代码更复杂。清单 12.22 显示了用于实现外部变量的 CIL 代码的 C# 等效代码。

### 清单 12.22: 编译器为外部变量生成的 CIL 代码的 C# 等效代码

```csharp
class DelegateSample
{
    // ...

    private sealed class __LocalsDisplayClass_00000001
    {
        public int comparisonCount;
        public bool __AnonymousMethod_00000000(
            int first, int second)
        {
            comparisonCount++;
            return first < second;
        }
    }

    ...

    static void Main(string[] args)
    {
        int i;
        __LocalsDisplayClass_00000001 locals =
            new __LocalsDisplayClass_00000001();
        locals.comparisonCount=0;
        int[] items = new int[5];

        for (i=0; i<items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }

        BubbleSort(items, locals.__AnonymousMethod_00000000);
        for (i = 0; i < items.Length; i++)
        {
            Console.WriteLine(items[i]);
        }

        Console.WriteLine("Items were compared {0} times.",
            locals.comparisonCount);
    }
}
```

请注意，捕获的局部变量从未被“传递”到任何地方，也从未被“复制”到任何地方。相反，捕获的局部变量（comparisonCount）是一个单一变量，我们通过将其实现为实例字段而非局部变量来扩展其生命周期。对局部变量的所有引用都重写为对字段的引用。

生成的类 __LocalsDisplayClass 是一个闭包——一种数据结构（C# 中的类），包含表达式以及计算表达式所需的变量（C# 中的公共字段）。变量（如 comparisonCount）使得在表达式的一次调用到下一次调用之间传递数据成为可能，而无需更改表达式的签名。

## 表达式树

Lambda 表达式为在代码中内联定义方法提供了简洁的语法。编译器会转换代码，使其稍后可执行和可调用，可能将委托传递给另一个方法。然而，它不提供内置支持的一个功能是将表达式表示为数据——可遍历甚至可序列化的数据。

## 将 Lambda 表达式用作数据

请考虑以下代码中的 Lambda 表达式：

```
persons.Where(
    person => person.Name.ToUpper() == "INIGO MONTOYA");
```

假设 persons 是 Persons 数组，编译器将 Lambda 表达式编译为 Func<Person, bool> 委托类型，然后将委托实例传递给 Where() 方法。这样的代码和执行效果很好。（Where() 方法是类 System.Linq.Enumerable 的 IEnumerable 扩展方法，但这在本节中无关紧要。）

如果 persons 不是 Person 数组，而是远程计算机或数据库中存放的 Person 对象集合，该怎么办？与其返回 persons 集合中的所有项目，不如通过网络发送描述表达式的数据，并在远程执行筛选，这样只有最终选择才会通过网络返回。在这种情况下，需要的是关于表达式的数据，而不是编译后的 CIL。然后远程计算机会编译或解释表达式数据。

解释是向语言添加表达式树的动机。表示关于表达式的数据而非

