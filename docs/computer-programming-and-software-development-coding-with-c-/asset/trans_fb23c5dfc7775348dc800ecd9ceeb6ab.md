
字符串。所以你在这里看到我使用了双等号。这个操作将返回一个布尔值，你可能已经猜到结果会是 false。所以我在这里做的是相等性检查，C# 会进行比较，并且默认情况下还会考虑该字符是小写还是大写。所以在这种情况下，这两个字符串是不相等的。如果我要检查 name1 是否等于另一个字符串 Bethany，让我们把这一行注释掉，结果确实是 True。因此，尽管我在比较两个不同的字符串，但它们是相等的。在这种情况下，我现在检查 name2 是否等于大写的 Bethany。但在这种情况下，我没有使用双等号，而是使用了 .Equals 方法。

```
//Console.WriteLine("Are both names equal? " + (name1 == name2));
//Console.WriteLine("Is name equal to Bethany? " + (name1 == "Bethany"));
//Console.WriteLine("Is name equal to BETHANY? " + name2.Equals("BETHANY"));
Console.WriteLine("Is lower name equal to bethany? " + (name1.ToLower() == "bethany"));

Console.ReadLine();
```

结果确实是相同的，因为双等号和 .Equals 方法做的事情一样。如果我想进行不区分大小写的比较，我可以再次使用 ToLower 或 ToUpper。在这种情况下，我只需在两边都使用 ToLower 或 ToUpper，然后就可以在不考虑大小写的情况下进行比较。在这种情况下，我将检查 name1.ToLower() 是否等于 bethany（也是小写）。这将返回 True。假设我们有一个包含单词 Hello 的字符串。然后我创建一个新字符串 b，并在下一行将它设置为 a。然后在下一行，我使用 `+=` 向 b 添加空格和 world。然后，我们询问 a 是什么。

看一下截图中的这个代码片段。我正在创建一个新的 StringBuilder。不要担心这里的新东西。这又是构造函数，我们稍后会学习它。然后，在我的 StringBuilder 上，我调用 Append 方法来追加字符串。我多次使用 AppendLine，它会在新的一行上追加我传入的字符串。使用 StringBuilder，这些操作都不会导致字符串被多次复制，而对于普通字符串来说情况并非如此。最后，我可以让 StringBuilder 返回实际的字符串值，我们可以使用 StringBuilder 类的 ToString 方法来实现。

## 第8章 字符串是不可变的

是时候回到 Visual Studio，确保我们理解字符串不可变性和 StringBuilder。到目前为止，我们一直在使用字符串，而且在不知不觉中，我们实际上已经遇到了字符串不可变性。因为我们目前使用的所有这些方法，比如 ToLower，它们实际上并不作用于原始字符串。它们返回原始字符串的一个副本。好吧，让我向你展示字符串是不可变的，无论我们做什么，我们都在处理一个不同的字符串。假设我再次创建一个字符串 name，并将其设置为 Bethany。我创建另一个变量，称之为 anotherName，并将其设置为 name。所以现在我有两个变量 name 和 anotherName，它们都指向一个字符串 Bethany。

```csharp
class Program
{
    static void Main(string[] args)
    {
        string name = "Bethany";
        string anotherName = name;

        Console.ReadLine();
    }
}
```

字符串是引用类型。我不期望你已经完全理解引用类型，但这实际上意味着字符串 Bethany 存储在堆上的某个位置，也就是主内存中。我有两个“指针”指向该字符串，即 name 和 anotherName。如果我说，让我的 name 字符串附加另一个字符串，我将在这里使用这个增量运算符，它将用（在这种情况下，比如说 Smith）扩展原始字符串。让我们在前面加一个空格。我所做的是创建了另一个字符串 Smith，并将其附加到 Bethany，但我没有将它附加到原始的 name 字符串。不，事实上，创建了一个新字符串，name 现在指向一个新创建的字符串。如果我现在将 name 和 anotherName 写入控制台，让我们看看输出。看看会发生什么。

![](img/0155736aec718cf18821e9f10a5d308d_688_0.png)

Name 现在指向拼接后的字符串 Bethany Smith，但 anotherName 仍然显示只是 Bethany。这是正确的。因为我将 anotherName 设置为等于 name，这意味着它们最初都指向 Bethany。name 变量已经改变。它指向拼接后的新字符串，但 anotherName 仍然指向原始字符串 Bethany，该字符串未被修改。字符串不可变性是一件总会发生的事情。例如，如果我说我想要小写的 name，我说，好吧，对 name 执行 ToLower，这不会影响原始字符串，它会返回原始字符串的一个副本，每个字符都被转换为其对应的小写形式。原始字符串 name 保持不变。我们总是得到一个副本。由于这种字符串不可变性，某些操作实际上会导致创建大量字符串，这实际上可能对应用程序中的内存消耗不利。假设我有一个非常简单的循环，我将循环 2500 次。我总是将 i 的值连接到 indexes（最初是一个空字符串）上。现在，通过这种方式，我们将创建该字符串的 2500 个副本。每次我们追加到原始字符串时，我们都会得到一个新字符串。原始字符串每次都保持不变。

```csharp
name += " Smith";

Console.WriteLine("Name: " + name);
Console.WriteLine("Another name: " + anotherName);

string lowerCaseName = name.ToLower();

string indexes = string.Empty;
for (int i = 0; i < 2500; i++)
{
    indexes += i.ToString();
}

Console.ReadLine();
```

虽然我说这实际上可能会使用更多内存，但不要开始恐慌。这实际上仍然是处理字符串的典型方式。但是，如果你必须在应用程序中进行大量拼接，例如在循环中，使用 StringBuilder 实际上可能是有益的。让我们使用 StringBuilder。我将创建一个新的 StringBuilder。当你开始输入 StringBuilder 这个词时，你会看到 Visual Studio 会给这个词加上波浪线。它不知道 StringBuilder。那是因为它位于不同的命名空间中，你必须将其引入。你实际上可以将鼠标悬停在 StringBuilder 上，然后 Visual Studio 会给你一些帮助，它会说你应该引入一个名为 System.Text 的命名空间。好吧，我们先接受这个建议，我们稍后会讨论版本。让我们看看结果，让我们注释掉这里的这些行。现在我们确实看到所有内容都在一行上。

```csharp
26  string firstName = "Bethany";
27  string lastName = "Smith";
28
29  StringBuilder builder = new StringBuilder();
30
31  builder.Append("Last name: ");
32  builder.Append(lastName);
33  builder.Append("First name: ");
34  builder.Append(firstName);
35  string result = builder.ToString();
36
37  Console.ReadLine();
38
39  }
40 }
41
```

那是因为我使用了 Append。我实际上应该使用 AppendLine，这会在末尾包含一个换行符。我们研究了从一种类型转换为另一种类型。现在对于字符串，我们实际上可以做更多事情，我们可以将字符串值解析为另一种类型。让我们看看。假设我们允许用户使用我们的控制台应用程序输入员工的工资值。捕获的值实际上始终是一个字符串。

```csharp
string w = Console.ReadLine();

double wage = double.Parse(w);

bool active = bool.Parse("true");
```

而且我们可能想要使用输入的值进行一些计算，因此我们需要根据输入的值创建一个 double。所以我们需要将其从字符串转换为 double。我们将在这里将字符串解析为 double，这可以使用 double 上的 Parse 方法来完成。如果该值可以被解析，并且它
