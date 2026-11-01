
可能在 System.Globalization 命名空间中最重要的类是 CultureInfo。CultureInfo 表示一种文化并定义了日历、数字和日期的格式，以及与该文化一起使用的字符串排序。

类 RegionInfo 表示区域设置（例如货币）并显示该区域是否使用公制。某些区域可以使用多种语言。一个例子是西班牙地区，它拥有巴斯克语（eu-ES）、加泰罗尼亚语（ca-ES）、西班牙语（es-ES）和加利西亚语（gl-ES）文化。与一个区域拥有多种语言类似，一种语言可以在不同的区域使用；例如，西班牙语在墨西哥、西班牙、危地马拉、阿根廷和秘鲁等国家使用，仅举几个例子。

本章后面您将看到一个示例应用程序，演示文化和区域的这些特性。

## 特定、中性与不变文化

在使用 .NET Framework 中的文化时，您必须区分三种类型：特定、中性 和 不变文化。

特定文化与 RFC 1766 中定义的真实、现有文化相关联，如前一节所述。特定文化可以映射到中性文化。例如，de 是特定文化 de-AT、de-DE、de-CH 等的中性文化。de 是德语（Deutsch）的简写；AT、DE 和 CH 分别是奥地利、德国和瑞士的国家简写。

在翻译应用程序时，通常不需要为每个区域做翻译；奥地利和德国的德语之间并没有多少差异。与其使用特定文化，您可以使用中性文化来本地化应用程序。

不变文化独立于真实文化。当将格式化的数字或日期存储在文件中，或通过网络发送到服务器时，使用独立于任何用户设置的文化是最好的选择。

图 22-2 显示了文化类型之间的关系。

![](img/d7d2ffa0a76feaab821930e95daace93_632_0.png)

图 22-2

## CurrentCulture 和 CurrentUICulture

设置文化时，您需要区分用户界面的文化和数字与日期格式的文化。文化与线程相关联，并且使用这两种文化类型，可以为线程应用两种文化设置。Thread 类具有 CurrentCulture 和 CurrentUICulture 属性。CurrentCulture 属性用于设置与格式和排序选项一起使用的文化，而 CurrentUICulture 属性用于用户界面的语言。

用户可以通过 Windows 控制面板中的区域和语言选项更改 CurrentCulture 的默认设置（参见图 22-3）。使用此配置，还可以更改文化的默认数字、时间和日期格式。

CurrentUICulture 不依赖于此配置。CurrentUICulture 设置取决于操作系统的语言。不过有一个例外：如果在 Windows 7、Windows Vista 或 Windows XP 上安装了多语言用户界面（MUI），则可以使用区域配置更改用户界面的语言，这会影响 CurrentUICulture 属性。

这些设置是一个非常好的默认值，在许多情况下无需更改默认行为。如果需要更改文化，可以通过将线程的两种文化都更改为例如西班牙文化来轻松完成，如以下代码片段所示：

```csharp
System.Globalization.CultureInfo ci = new System.Globalization.CultureInfo("es-ES");
System.Threading.Thread.CurrentThread.CurrentCulture = ci;
System.Threading.Thread.CurrentThread.CurrentUICulture = ci;
```

现在您已经了解了如何设置文化，以下各节讨论数字和日期格式化，它们受 CurrentCulture 设置的影响。

## 数字格式化

System 命名空间中的数字结构 Int16、Int32、Int64 等具有重载的 ToString() 方法。此方法可用于根据区域设置创建数字的不同表示形式。对于 Int32 结构，ToString() 重载了以下四个版本：

```
public string ToString();
public string ToString(IFormatProvider);
public string ToString(string);
public string ToString(string, IFormatProvider);
```

不带参数的 ToString() 返回不带格式选项的字符串。您还可以传递一个字符串和一个实现 IFormatProvider 的类。

该字符串指定表示的格式。格式可以是标准数字格式字符串或图片数字格式字符串。对于标准数字格式，字符串是预定义的，其中 C 指定货币表示，D 创建十进制输出，E 创建科学输出，F 创建定点输出，G 创建常规输出，N 创建数字输出，X 创建十六进制输出。使用图片数字格式字符串，可以指定数字位数、部分和组分隔符、百分比表示等。图片数字格式字符串 ###,### 表示由组分隔符分隔的两个 3 位数字块。

IFormatProvider 接口由 NumberFormatInfo、DateTimeFormatInfo 和 CultureInfo 类实现。该接口定义了单个方法 GetFormat()，它返回一个格式对象。

NumberFormatInfo 可用于定义数字的自定义格式。使用 NumberFormatInfo 的默认构造函数，会创建一个与文化无关或不变的对象。使用 NumberFormatInfo 的属性，可以更改所有格式选项，例如正号、百分比符号、数字组分隔符、货币符号等。只读的与文化无关的 NumberFormatInfo 对象由静态属性 InvariantInfo 返回。格式值基于当前线程的 CultureInfo 的 NumberFormatInfo 对象由静态属性 CurrentInfo 返回。

要创建下一个示例，您可以从一个简单的控制台项目开始。在此代码中，第一个示例显示了按线程文化格式显示的数字（此处：英语-US，即操作系统的设置）。第二个示例使用带 IFormatProvider 参数的 ToString() 方法。CultureInfo 实现 IFormatProvider，因此使用法语文化创建一个 CultureInfo 对象。第三个示例更改线程的文化。通过使用 Thread 实例的 CurrentCulture 属性将文化更改为德语：

```
using System;
using System.Globalization;
using System.Threading;

namespace NumberAndDateFormatting
{
    class Program
    {
        static void Main(string[] args)
        {
            NumberFormatDemo();
        }

        private static void NumberFormatDemo()
        {
            int val = 1234567890;

            // culture of the current thread
            Console.WriteLine(val.ToString("N"));

            // use IFormatProvider
            Console.WriteLine(val.ToString("N", new CultureInfo("fr-FR")));

            // change the culture of the thread
            Thread.CurrentThread.CurrentCulture = new CultureInfo("de-DE");
            Console.WriteLine(val.ToString("N"));
        }
    }
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_633_0.png)

图 22-3

代码片段 NumberAndDateFormatting/Program.cs

输出如下所示。您可以分别比较美国英语、法语和德语的不同输出，

```
1,234,567,890.00
1 234 567 890,00
1.234.567.890,00
```

## 日期格式化

日期也提供与数字相同的支持。DateTime 结构具有一些日期到字符串转换的方法。公共实例方法 ToLongDateString()、ToLongTimeString()、ToShortDateString() 和 ToShortTimeString() 使用当前文化创建字符串表示形式。您可以使用 ToString() 方法指定不同的文化：

```
public string ToString();
public string ToString(IFormatProvider);
public string ToString(string);
public string ToString(string, IFormatProvider);
```

使用 ToString() 方法的字符串参数，您可以指定预定义的格式字符或用于将日期转换为字符串的自定义格式字符串。类 DateTimeFormatInfo 指定了可能的值。使用 DateTimeFormatInfo，格式字符串的大小写具有不同的含义。D 定义长日期格式，d 定义短日期格式。其他可能的格式示例有 ddd 表示星期几的缩写，dddd 表示星期几的全称，yyyy 表示年份，T 表示长时间，t 表示短时间格式。使用 IFormatProvider 参数，您可以指定文化。使用不带 IFormatProvider 参数的重载方法意味着使用当前线程的文化：

```
DateTime d = new DateTime(2009, 06, 02);

// current culture
Console.WriteLine(d.ToLongDateString());

// use IFormatProvider
Console.WriteLine(d.ToString('D', new CultureInfo("fr-FR")));

// use culture of thread
CultureInfo ci = Thread.CurrentThread.CurrentCulture;
Console.WriteLine("{0}: {1}", ci.ToString(), d.ToString("D"));
```
