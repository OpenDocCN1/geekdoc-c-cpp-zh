
```csharp
using System;
using System.Globalization;

namespace Chapter32CS
{
    public partial class Page : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            DateTime dt = DateTime(2013, 8, 11, 12, 10);
            System.Threading.CurrentThread.CurrentCulture = new CultureInfo("en-US");
            Response.Write("<b>en-US</b><br>");
        }
    }
}
```

## 代码列表 32-8（继续）

```csharp
Response.Write(dt.ToString() + "<br>");

System.Threading.CurrentThread.CurrentCulture = new CultureInfo("ru-RU");
Response.Write("<b>ru-RU</b><br>");
Response.Write(dt.ToString() + "<br>");

System.Threading.CurrentThread.CurrentCulture = new CultureInfo("fi-FI");
Response.Write("<b>fi-FI</b><br>");
Response.Write(dt.ToString() + "<br>");

System.Threading.CurrentThread.CurrentCulture = new CultureInfo("th-TH");
Response.Write("<b>th-TH</b><br>");
Response.Write(dt.ToString() + "<br>");
```

此代码构建了一个 `DateTime` 并利用四个不同的区域向浏览器显示该值。图 32-6 显示了执行此代码的结果。

![](img/67a6707ff505c052edb96c0128fb3096_193_0.png)

你可以看到，表示日期/时间值的格式彼此截然不同，其中一个区域——泰国区域（`th-TH`），甚至使用了完全不同的日历，将 2012 年显示为 2553。

## 理解数字和货币的差异

除了日期/时间值外，不同区域之间的数字构造方式也不同。数字在不同区域如何不同表示？这与数字本身的关系较小，尽管某些区域使用不同的数字符号，并且数字分隔符用于小数或用于显示千、百万等金额。例如，在美国英语区域（`en-US`）中，你看到的数字格式如下：

5,123,456.00

从这个示例可以看出，`en-US` 区域使用逗号作为千位分隔符，并用点表示任何小数的开始。当与其他区域一起工作时，这个数字看起来完全不同。代码列表 32-9 显示了在其他区域表示数字的示例（代码下载中的 Numbers.aspx.vb）。

## 代码列表 32-9：在不同区域处理数字

### VB

```vb
Imports System.Globalization
Public Class Numbers
Inherits System.Web.UI.Page

Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
Handles Me.Load
Dim myNumber As Double = 5123456.0
System.Threading.CurrentThread.CurrentCulture = New CultureInfo("en-US")
Response.Write("<b>en-US</b><br>")
Response.Write(myNumber.ToString("n") & "<br>")

System.Threading.CurrentThread.CurrentCulture = New CultureInfo("vi-VN")
Response.Write("<b>vi-VN</b><br>")
Response.Write(myNumber.ToString("n") & "<br>")

System.Threading.CurrentThread.CurrentCulture = New CultureInfo("fi-FI")
Response.Write("<b>fi-FI</b><br>")
Response.Write(myNumber.ToString("n") & "<br>")

System.Threading.CurrentThread.CurrentCulture = New CultureInfo("de-CH")
Response.Write("<b>de-CH</b><br>")
Response.Write(myNumber.ToString("n") & "<br>")

End Sub
```

### C#

```csharp
using System;
using System.Globalization;
namespace Chapter32CS
{
    public partial class Numbers : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            double myNumber = 5123456.0;
            System.Threading.CurrentThread.CurrentCulture = new CultureInfo("en-US");
            Response.Write("<b>en-US</b><br>");
        }
    }
}
```

### 列表 32-9（续）

```csharp
Response.Write(myNumber.ToString("n") + "<br>");

System.Threading.CurrentThread.CurrentCulture = new CultureInfo("fi-FI");
Response.Write("<u>fi-FI</u>" + "<br>");
Response.Write(myNumber.ToString("n") + "<br>");

System.Threading.CurrentThread.CurrentCulture = new CultureInfo("de-CH");
Response.Write("<u>de-CH</u>" + "<br>");
Response.Write(myNumber.ToString("n"));
```

运行此示例将产生图 32-7 所示的结果。

从这个示例中，你可以看到这里表示的其他文化所显示的数字格式与 `en-US` 文化格式不同。图中列出的第二种文化 `vi-VN`（越南的越南语）显示的数字其构造方式与 `en-US` 的构建方式完全相反。越南语使用点作为千分位分隔符，使用逗号表示小数。另一方面，芬兰语使用空格作为千分位分隔符，并使用逗号作为小数分隔符。最后，说德语的瑞士人使用高逗号分隔千位，使用点作为小数分隔符。正如你所看到的，将数字“翻译”为相应的构造方式，以便你的应用程序用户能够正确理解所表示的数字是非常重要的。

![](img/67a6707ff505c052edb96c0128fb3096_1195_0.png)

货币也使用数字表示。在货币的情况下，使这些数字在不同的文化中正确呈现不仅是一个视觉呈现的问题，而且为了确保表示了正确的数值。

每种文化都有独特的货币符号，用于表示所代表的数字是实际的货币价值。例如，`en-US` 文化以以下格式表示货币：

$5,123,456.00

`en-US` 文化使用美元符号 (`$`)，且该符号的位置与符号本身一样重要。对于 `en-US` 而言，`$` 符号位于货币值之前，符号与数字的第一个字符之间没有空格。其他文化使用不同的符号表示货币，并通常将这些货币符号放在不同的位置。它现在将数字表示为货币。列表 32-10 修改了之前的列表 32-9，使其呈现了必要的更改（本章节代码下载中的 Currency.aspx.vb 和 Currency.aspx.vb）。

# 列表 32-10：在不同文化中处理货币

## VB

```vb
Imports System.Globalization

Public Class Currency
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        Handles Me.Load
        Dim myNumber As Double = 5123456.0
        System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("en-US")
        Response.Write("<br><u>en-US</u><br>")
        Response.Write(myNumber.ToString("c") + "<br>")

        System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("vi-VN")
        Response.Write("<br><u>vi-VN</u><br>")
        Response.Write(myNumber.ToString("c") + "<br>")

        System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("fi-FI")
        Response.Write("<br><u>fi-FI</u><br>")
        Response.Write(myNumber.ToString("c") + "<br>")

        System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("de-CH")
        Response.Write("<br><u>de-CH</u><br>")
        Response.Write(myNumber.ToString("c") + "<br>")
    End Sub
End Class
```

## C#

```csharp
using System;
using System.Globalization;

namespace Chapter32CS
{
    public partial class Currency : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            double myNumber = 5123456.0;
            System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("en-US");
            Response.Write("<br><u>en-US</u><br>");
            Response.Write(myNumber.ToString("c") + "<br>");

            System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("vi-VN");
            Response.Write("<br><u>vi-VN</u><br>");
            Response.Write(myNumber.ToString("c") + "<br>");

            System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("fi-FI");
            Response.Write("<br><u>fi-FI</u><br>");
            Response.Write(myNumber.ToString("c") + "<br>");

            System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("de-CH");
            Response.Write("<br><u>de-CH</u><br>");
            Response.Write(myNumber.ToString("c") + "<br>");
        }
    }
}
```

## 理解排序中的差异

全球化不仅影响数字的显示，还影响货币、日期和时间。文化设置可以影响诸如排序的行为。通常大多数文化以相同的方式排序，但某些文化在构造上存在差异。列表 32-12 显示了在 `en-US` 文化下的排序方式。图 32-9 显示了该操作的结果。

## 列表 32-11：指定特定的文化

### VB

```vb
Dim myNumber As Double = 5123456.0
Dim usCurr As CultureInfo = New CultureInfo("en-US")
Response.Write(myNumber.ToString("c"))
```

### C#

```csharp
double myNumber = 5123456.0;
CultureInfo usCurr = new CultureInfo("en-US");
Response.Write(myNumber.ToString("c"));
```

## 列表 32-12：在不同文化中工作

### VB

```vb
Imports System.Globalization

Public Class SortingEN
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        Handles Me.Load
        System.Threading.Thread.CurrentThread.CurrentCulture = New CultureInfo("en-US")

        Dim myList As List(Of String) = New List(Of String)

        myList.Add("Washington D.C.")
        myList.Add("Helsinki")
        myList.Add("Moscow")
        myList.Add("Warsaw")
        myList.Add("Vienna")
        myList.Add("Tokyo")

        myList.Sort()

        For Each item String In myList
            Response.Write(item.ToString() + "<br>")
        Next
    End Sub
End
```

### C#

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;

namespace Chapter32CS
{
    public partial class Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("en-US");

            List<string> myList = new List<string>();

            myList.Add("Washington D.C.");
            myList.Add("Helsinki");
            myList.Add("Moscow");
            myList.Add("Warsaw");
            myList.Add("Vienna");
            myList.Add("Tokyo");

            myList.Sort();

            foreach (string item in myList)
            {
                Response.Write(item.ToString() + "<br>");
            }
        }
    }
}
```

在这个示例中，以随机顺序创建了来自世界各地国家的首都的通用列表。然后调用了通用 `List(Of String)` 对象的 `Sort()` 方法。此排序操作根据运行 ASP.NET 线程的文化的排序方式对字符串进行排序。列表 32-12 显示了在 `en-US` 文化下的排序情况。

# 1150 | 第32 章 构建全球化应用程序
