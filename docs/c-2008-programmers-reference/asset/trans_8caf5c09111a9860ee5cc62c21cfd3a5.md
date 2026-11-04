
要从字符串中删除从特定索引开始的子字符串，请使用 `Remove()` 实例方法：

```csharp
str2 = str1.Remove(10);
Console.WriteLine(str2); //---"This is a"---
```

此语句删除从索引位置 10 开始的字符串。若要删除特定数量的字符，需要在第二个参数中指定要删除的字符数：

```csharp
str2 = str1.Remove(10,5);  //---remove 5 characters from index 10---
Console.WriteLine(str2);  //---"This is a string.."---
```

要用另一个子字符串替换某个子字符串，请使用 `Replace()` 实例方法：

```csharp
str2 = str1.Replace("long", "short");
Console.WriteLine(str2); //---"This is a short string.."---
```

要在不指定确切长度的情况下从字符串中删除子字符串，请使用 `Replace()` 方法，如下所示：

```csharp
str2 = str1.Replace("long ", string.Empty);
Console.WriteLine(str2); //---"This is a string.."---
```

## 更改大小写

要更改字符串的大小写，请使用 `ToUpper()` 或 `ToLower()` 实例方法。以下语句演示了它们的用法：

```csharp
string str1 = "This is a string";
string str2;

str2 = str1.ToUpper();
Console.WriteLine(str2); //---"THIS IS A STRING"---

str2 = str1.ToLower();
Console.WriteLine(str2); //---"this is a string"---
```

## 字符串格式设置

你已经看到使用 `Console.WriteLine()` 方法将输出打印到控制台。例如，以下语句将 `num1` 的值打印到控制台：

```csharp
int num1 = 5;
Console.WriteLine(num1); //---5---
```

也可以像这样打印多个变量的值：

```csharp
int num1 = 5;
int num2 = 12345;
Console.WriteLine(num1 + " and " + num2); //---5 and 12345---
```

但是，如果要打印的变量太多（比如超过五个），代码很快就会变得很乱。更好的方法是使用格式说明符，如下所示：

```
Console.WriteLine("{0} and {1}", num1, num2); //---5 and 12345---
```

格式说明符（{0}、{1} 等）会自动将所有数据类型转换为字符串。格式说明符按顺序标记（{0}、{1}、{2} 等）。然后，每个格式说明符都会替换为要打印的变量的值。编译器查看格式说明符中的数字，取出参数列表中具有相同索引的参数，并进行替换。在前面的示例中，num1 和 num2 是格式说明符的参数。

如果希望打印用 {} 字符括起来的数字值，会发生什么？例如，假设当 num1 的值为 5 时，你想打印字符串 {5}。可以这样做：

```
num1 = 5;
Console.WriteLine("{{0}}", num1); //---{5}---
```

为什么格式说明符要有两对额外的 {} 字符？因为如果只有一对额外的 {} 字符，编译器会将其解释为你想打印字符串字面量 {0}，如下所示：

```
num1 = 5;
Console.WriteLine("{{0}}", num1); //---{0}---
```

这两对额外的 {} 字符向编译器表明，你希望指定一个格式说明符，同时用一对 {} 字符将值括起来。

正如前面所演示的，String 类包含 Format() 静态方法，它使你可以创建新字符串（以及对字符串数据执行格式设置）。前面的语句可以使用以下语句重写：

```
string formattedString = string.Format("{{0}}", num1);
Console.WriteLine(formattedString); //---{5}---
```

要格式化数字，可以使用如下所示的格式说明符：

```
num1=5;
Console.WriteLine("{0:N}", num1);        //---5.00---
Console.WriteLine("{0:00000}", num1);    //---00005---
//---OR---
Console.WriteLine("{0:d5}", num1);       //---00005---
Console.WriteLine("{0:d4}", num1);       //---0005---
Console.WriteLine("{0,5:G}", num1);      //---    5 (4 spaces on left)---
```

有关可用于格式设置字符串的格式说明符的详细列表，请参阅 MSDN 文档中的“标准数字格式字符串”和“自定义数字格式字符串”主题。

还可以根据数字的值打印特定字符串。考虑以下示例：

```csharp
num1 = 0;
Console.WriteLine("{0:yes;;no}", num1); //---no---
num1 = 1;
Console.WriteLine("{0:yes;;no}", num1); //---yes---
num1 = 5;
Console.WriteLine("{0:yes;;no}", num1); //---yes---
```

在这种情况下，格式说明符包含两个字符串：yes 和 no。如果变量（num）的值非零，将返回第一个字符串（yes）。如果值为 0，则返回第二个字符串（no）。下面是另一个示例：

```csharp
num1 = 0;
Console.WriteLine("{0:OK;;Cancel}", num1); //---Cancel---
num1 = 1;
Console.WriteLine("{0:OK;;Cancel}", num1); //---OK---
num1 = 5;
Console.WriteLine("{0:OK;;Cancel}", num1); //---OK---
```

对于十进制数字格式设置，请使用以下格式说明符：

```csharp
double val1 = 3.5;
Console.WriteLine("{0:#.##00}", val1); //---3.50---
Console.WriteLine("{0:#.###00}", val1); //---3.500---
Console.WriteLine("{0:000.###}", val1); //---003.500---
```

有时数字会以字符串形式表示。例如，值 9876 可能在字符串中用逗号表示千位。在这种情况下，不能像这样简单地从 int 类使用 Parse() 方法：

```csharp
string str2 = "9,876";
int num3 = int.Parse(str2); //---error---
```

要正确解析该字符串，请使用以下语句：

```csharp
int num3 = int.Parse(
    str2,
    System.Globalization.NumberStyles.AllowThousands);
Console.WriteLine(num3); //---9876---
```

下面是另一个示例：

```csharp
string str3 = "1,239,876";
num3 = int.Parse(
    str3,
    System.Globalization.NumberStyles.AllowThousands);
Console.WriteLine(num3); //---1239876---
```

反过来——使用逗号分隔符格式化数字呢？解决方案如下：

```csharp
num3 = 9876;
Console.WriteLine("{0:#,0}", num3); //---9,876---
```

```csharp
num3 = 1239876;
Console.WriteLine("{0:#,0}", num3); //---1,239,876---
```

最后，要格式化特殊数字（例如电话号码），请使用以下格式说明符：

```csharp
long phoneNumber = 1234567890;
Console.WriteLine("{0:###-###-####}", phoneNumber); //---123-456-7890---
```

## StringBuilder 类

在本章前面，你已经看到如何使用 + 运算符轻松连接两个字符串。如果要连接的字符串数量较少，这没问题，但不建议用于大量字符串。原因在于 .NET 中的 `String` 对象是*不可变的*，这意味着一旦字符串变量被初始化，其值就不能更改。当你将另一个字符串连接到现有字符串时，实际上会丢弃其旧值，并创建一个包含连接结果的新字符串对象。当你多次重复此过程时，由于会创建新的临时对象并丢弃旧对象，因此会造成性能损失。

> > **`StringBuilder` 类的一个重要应用是在 .NET 与接受字符串参数并修改字符串的本机 C/C++ API 进行互操作时使用。其中一个示例是 Windows API 函数 `GetWindowText()`。此函数有一个接受 `TCHAR*` 参数的第二个参数。要在 .NET 代码中使用此函数，需要传递一个 `StringBuilder` 对象作为此参数。**

考虑以下示例，其中连接从 0 到 9999 的所有数字：

```csharp
int counter = 9999;
string s = string.Empty;
for (int i = 0; i <= counter; i++) {
    s += i.ToString();
}
Console.WriteLine(s);
```

## 第 I 部分：C# 基础知识

乍一看，这段代码似乎没有问题。但让我们使用 Stopwatch 对象来为操作计时。如下所示修改代码：

```csharp
int counter = 9999;
System.Diagnostics.Stopwatch sw = new System.Diagnostics.Stopwatch();
sw.Start();
```

```csharp
string s = string.Empty;
for (int i = 0; i <= counter; i++) {
    s += i.ToString();
}
```

```csharp
sw.Stop();
Console.WriteLine("Took {0} ms", sw.ElapsedMilliseconds);
Console.WriteLine(s);
```

在我的计算机上，运行此操作平均大约耗时 374 ms。现在让我们使用 .NET 中的 StringBuilder 类，通过其 Append() 方法执行字符串连接：

```csharp
System.Diagnostics.Stopwatch sw = new System.Diagnostics.Stopwatch();
sw.Start();
```

```csharp
StringBuilder sb = new StringBuilder();
for (int i = 0; i <= 9999; i++) {
    sb.Append(i.ToString());
}
```

```csharp
sw.Stop();
Console.WriteLine("Took {0} ms", sw.ElapsedMilliseconds);
Console.WriteLine(sb.ToString());
```

在我的计算机上，执行此操作平均大约耗时 6 ms。正如你可以推断出的，改进非常显著——98%（(374-6)/374）。如果增大循环变量（counter）的值，你会发现改进甚至更加显著。

StringBuilder 类表示可变的字符字符串。其行为类似于 String 对象，不同之处在于它的值在创建后可以修改。

StringBuilder 类还包含一些其他重要方法，下表对它们进行了描述。
