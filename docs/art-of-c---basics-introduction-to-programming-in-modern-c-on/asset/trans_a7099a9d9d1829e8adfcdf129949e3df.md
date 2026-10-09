

凯撒密码是最简单且最著名的加密技术之一。它是一种替换密码，其中明文中的每个字母都由字母表中固定距离处的某个字母替换。例如，在向左移动 3 位的情况下，A 会被替换为 D，B 会变成 E，以此类推。

移位 13 是最常用的，被称为 "rot13"。在 Rot13 中，对于一组英文字母（26 个字母）来说，“加密”和“解密”是相同的操作。

在 rot13 方案中，例如，大写字母的映射如下：

![](img/25af69ec45b3c0b589a8dccd0c2a88be_253_0.png)

以下是演示我们自定义类型 Cipher 用法的 main 程序。

**caesar-cipher/Program.cs (第 3-12 行)**

```csharp
3 var cipher = new Cipher(10);
  var text = "Hello Programming Artist!";
4 Console.WriteLine($"plaintext = {text}");

5 var encrypted = cipher.Encrypt(text);
  Console.WriteLine($"encrypted = {encrypted}");

  var decrypted = cipher.Decrypt(encrypted);
  Console.WriteLine($"decrypted = {decrypted}");
```

它首先使用 new 运算符创建一个类型 Cipher 的实例，并将其引用赋值给一个新变量 cipher。它在该变量上调用 Encrypt() 和 Decrypt() 方法，并打印出结果。

> 完整的示例代码可在本书末尾找到，代码列表 - 第二部分。如所述，本书中的所有示例代码都使用 System 和其他系统命名空间的隐式命名空间导入（C# 10.0）。现在应该已经熟悉了，Console 静态类定义在 System 命名空间中。

类型 `Cipher` 定义如下：

### caesar-cipher/Cipher.cs (第 4-34 行)

```csharp
4 public sealed class Cipher {
    public int Shift { get; init; }

7 public Cipher(int shift = 13) => Shift = Mod(shift);

9 public string Encrypt(string clearText) => Rotate(clearText,
  Shift);
10
11 public string Decrypt(string cipherText) => Rotate(cipherText,
   -Shift);

12
13 private static int Mod(int shift) => (shift % 26 + 26) % 26;
14
15 private static string Rotate(string text, int shift) {
16 shift = Mod(shift);

18 var sb = new StringBuilder();
19 foreach (var c in text) {
20 if (char.IsLetter(c)) {
21 if (char.IsUpper(c)) {
22 var u = (char)(((c - 'A' + shift) % 26) + 'A');
23 sb.Append(u);
24 } else {
25 var l = (char)(((c - 'a' + shift) % 26) + 'a');
26 sb.Append(l);
27 }
28 } else {
29 sb.Append(c);
30 }
31 }
32 return sb.ToString();
33 }
```

![](img/25af69ec45b3c0b589a8dccd0c2a88be_256_0.png)

Cipher 类定义在 Caesar 命名空间中。如有必要，您可以参考本书末尾的完整代码示例。在本书的所有代码示例中，我们使用 C# 10.0 的文件范围命名空间语法声明命名空间，如第一部分所述。

## 16.3. 结对编程 - 用户定义类型、引用类型、构造函数、对象初始化器

在此示例中，使用 class 来创建自定义引用类型。Cipher 是一种引用类型。cipher 是一个引用变量。

在这个小示例中，区别很小，但通常这是一个重要的设计决策，例如，对于给定的对象或概念，哪种类型的最佳。

- 我们使用 class 或 record (class) 来创建引用类型，并使用 struct 或 record struct 来创建值类型。
- 如果说，就数据和行为而言，“类型”为变量定义了一个“模板”或“模具”。
- 作为一般原则，对于主要是“数据”的东西，最好使用 struct 值类型或 record struct。对于主要是“行为”的东西（也可以包含数据），则使用 class 引用类型或 record class。
- record 或 record class 类型规定了一种（不可变的）遵循值语义的引用类型。record 通常用于创建数据类型，就像 struct 和 record struct 一样。

如果你是编程新手，这可能听起来很混乱。但不用担心。我们会在整本书中反复讨论这个主题。☺

如果我们运行 main 程序，我们将得到以下控制台输出。

```bash
$ dotnet run

plaintext  = Hello Programming Artist!
encrypted = Rovvy Zbygbkvwxsq Kbdscdj!
decrypted = Hello Programming Artist!
```

如您所见，再次加密和解密后的文本与原始文本相同。

以下语法定义了一个（引用）类型 `Cipher`：

```csharp
class Cipher {
    // ...
}
```

访问修饰符 `public` 使该类可能从当前程序集外部访问。关键字 `sealed` 表示该类不能被“继承”或“子类化”。（我们将在本书稍后讨论继承和多态性。）

以下是一个“构造方法”，或简称为“构造函数”。

```csharp
public Cipher(int shift = 13) {
    // ...
}
```

它看起来像是一个方法，但它与类同名。并且，其方法声明语法不包含“返回类型”。公共类的构造函数通常是 public 的，但并不一定是。

构造函数用于“构造”或创建给定类型的新对象。

构造函数可以像其他任何方法一样被“重载”。也就是说，只要参数列表不同，就可以定义多个构造函数。

在此示例中，构造函数 `Cipher(int shift)` 接受一个名为 shift 的 int 参数。符号 `int shift = 13` 表示在调用此构造函数时如果未给出参数，则 shift 的值将默认为 13。像 shift 这样的方法参数被称为“可选参数”。

如果定义一个类时没有构造函数，则编译器会自动创建其“默认构造函数”（一个没有任何参数的构造函数）。

这是一个（显式定义的）默认构造函数示例。

```csharp
public Cipher() {
	Shift = 0;
}
```

构造函数使用 new 运算符创建该类型的实例。例如，以下任何语法都可以用来创建类型 Cipher 的值（在这种情况下是引用值，或“对象”）。该值随后被赋值给名为 cipher 的变量。

```csharp
Cipher cipher = new();
```

```csharp
Cipher cipher = new(2);
```

```csharp
Cipher cipher = new(shift: 5);
```

在第一条语句中，创建了一个 `Cipher` 对象，由于未提供 `Shift` 属性的显式值，其 `Shift` 属性被设置为 13。在第二条语句中，新创建的对象其 `Shift` 为 2。

最后一个示例语句使用了一个“命名参数”，`shift: 5`。注意语法。注意名称 `shift` 是在构造函数方法声明中使用的参数名。命名参数可用于任何方法，而不仅仅是构造函数。

我们也可以对 `cipher` 使用隐式 `var` 声明。在这种情况下，应在 `new` 表达式中显式指定构造函数。例如，以下三个语句中的每一个都等价于上面相应的示例：

```csharp
var cipher = new Cipher();
```

```csharp
var cipher = new Cipher(2);
```

```csharp
var cipher = new Cipher(shift: 5);
```

请注意，此示例中的最后一条语句也使用了“命名参数”。

`class` 或 `struct`（或其 `record` 变体）的实例也可以使用“对象初始化器”语法创建。例如，

```csharp
var cipher = new Cipher { Shift = 2 };
```

它在一对花括号（`{` 和 `}`）内指定必要的参数。注意我们可以使用这种语法，因为 `Cipher` 提供了无参数构造函数（通过可选参数语法）。

我们也可以这样做：

```csharp
var cipher = new Cipher { };
```

或者，甚至

```csharp
Cipher cipher = new() { Shift = 2 };
```

或者

```csharp
Cipher cipher = new() { };
```

使用 Shift 属性的默认值 13。

在许多情况下，特别是对于主要是“数据类型”的类型，通常的做法是摒弃构造函数（除了默认构造函数）而仅使用对象初始化器。

因此，你更有可能在 struct 和 record struct 类型中看到对象初始化器语法，以及在较小程度上在 record class 类型中看到。

注意，使用对象初始化器要求该类型应为必要的数据字段定义公开可设置或至少是 init-only 的属性。

类 Cipher 中的以下一行定义了一个公共属性 Shift。（第 5 行。）

```csharp
public int Shift { get; init; }
```

这被称为“自动属性”（或自动实现属性）。

