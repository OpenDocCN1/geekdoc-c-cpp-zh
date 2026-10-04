
以下代码演示了文化对于字符串排序有多么重要，并展示了执行字符串比较的方法。

```csharp
using System;
using System.Text;
using System.Windows.Forms;
using System.Globalization;
using System.Threading;
```

```csharp
public sealed class Program {
    public static void Main() {
        String output = String.Empty;
        String[] symbol = new String[] { "<", "=", ">" };
        Int32 x;
        CultureInfo ci;

// 以下代码演示了不同文化下字符串比较有何不同。
String s1 = "cote";
String s2 = "côte";

// 在法国进行法语字符串排序。
ci = new CultureInfo("fr-FR");
x = Math.Sign(ci.Compare(s1, s2));
output += String.Format("{0}: {1} {2}",
ci.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;

// 在日本进行日语字符串排序。
ci = new CultureInfo("ja-JA");
x = Math.Sign(ci.Compare(s1, s2));
output += String.Format("{0}: {1} {2}",
ci.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;

// 使用线程文化的字符串排序
ci = Thread.CurrentCulture;
x = Math.Sign(ci.Compare(s1, s2));
output += String.Format("{0}: {1} {2}",
ci.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;

// 以下代码演示了如何对两个日语字符串使用 
// CompareInfo.Compare 的高级选项。其中一个字符串代表
// 平假名（日语写作的一个子集）中的“shinkansen”（日本高铁的名称），
// 另一个代表片假名（日语写作的另一个子集）中的相同单词。

s1 = "\u3057\u3093\u30a4\u3093\u3093";
s2 = "\u30f3\u30f3\u30a3\u30a3\u30f3\u30bb\u30f3";

// 这里是默认比较的结果
ci = new CultureInfo("ja-JA");
x = Math.Sign(String.Compare(s1, s2, true, ci));
output += String.Format("{0}: {1} {2}",
ci.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;

// 这里是忽略假名（一种日语写法）的比较结果。
CompareInfo compareInfo = CompareInfo.GetCompareInfo("ja-JP");
x = Math.Min(compareInfo.Compare(s1, s2, CompareOptions.IgnoreKanaType));
output = String.Format("Advanced {} Compare: {1} {3} {2}",
ci.Name, s2, symbol[x]);

MessageBox.Show("Comparing Strings for Sorting");
}
```

> 注意，此源代码不会以 ANSI 格式保存，否则日文字符将丢失。要在 Microsoft Visual Studio 中保存此文件，请转到文件另存为对话框，点击“保存”按钮上的箭头并选择“保存编码”。选择 Unicode (带有 BOM 的 UTF-8) – 代码页 65001。微软的 C# 编译器可以使用此代码页成功解析源代码文件。

编译并运行此代码将产生图 14-1 所示的输出。

| 用于排序字符串比较 |
| :--- |
| frFR Compare: cote > côte |
| jaJP Compare: côte < côte |
| enUS Compare: cote < côte |
| Simple ja-JP Compare: しんかんせん = ジンガンセン |
| Advanced ja-JP Compare: しんかんせん = ジンガンセン |
| OK |

除了 Compare 之外，CompareInfo 类还提供了 IndexOf、LastIndexOf、IsPrefix 和 IsSuffix 方法。由于所有这些方法都存在接受 `CompareOptions` 枚举作为参数的重载，它们为你对 String 类定义的 `Compare`、`IndexOf`、`LastIndexOf`、`StartsWith` 和 `EndWith` 方法提供了更多的控制。你还应该意识到，FCL 有一个 `System.String` 类，你也可以使用它来执行字符串比较。当你需要对许多不同的字符串重复执行相同类型的比较时，该类非常有用。

## 字符串池 (String Interning)

正如我在上一节提到的，检查字符串的相等性是许多应用程序的常见操作——此任务可能会显著损害性能。在执行序等相等检查（ordinal equality check）时，CLR 会快速测试两个字符串是否具有相同的字符数。如果不同，则字符串肯定不相等；如果相同，字符串可能相等，此时 CLR 必须比较每个单独字符以确定。在执行具有文化知的比较时，CLR 必须始终比较所有单独字符，因为不同长度的字符串可能会被认为是相等的。

此外，如果你在内存中存在多个重复的字符串实例，你就会浪费内存，因为字符串是不可变的。如果内存中只存在一个字符串实例，所有需要引用该字符串的变量都可以指向该实例，你使用内存将将高效得多。

如果你的应用程序频繁使用大小敏感的序等比较来检查字符串相等性，或者你预计会有许多具有相同值的字符串对象，利用 CLR 中的字符串池机制，你可以大幅提升性能。当 CLR 初始化时，它会创建一个内部哈希表，其键是字符串，值是指向托管堆中 String 对象的引用。初始时，该表是空的（当然）。String 类提供了两个方法，允许你访问此内部哈希表。

```csharp
public static String Intern(String str);
public static String IsInterned(String str);
```

第一个方法 `Intern` 接收一个字符串，获取其哈希码并检查内部哈希表是否有匹配项。如果已经存在完全相同的字符串，则返回已存在 String 对象的引用。如果不存在相同的字符串，则创建字符串的副本，将其添加到内部哈希表中并返回该副本的引用。如果应用程序不再持有原始 String 的引用，垃圾回收器无法释放该字符串的内存。注意，垃圾回收器无法释放引用了 String 对象的哈希表。

