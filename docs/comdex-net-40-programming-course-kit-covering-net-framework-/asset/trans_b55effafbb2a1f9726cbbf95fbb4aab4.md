
## 清单 9.2：显示 Default.aspx 页面的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Label3.Text = DateTime.Now.ToString("T");
    }
    static string GetTime(HttpContext context)
    {
        return DateTime.Now.ToString("T");
    }
}
```

在清单 9.2 中，`Label3` 控件的 `Text` 属性被设置为当前时间。还声明了一个名为 `GetTime` 的方法，该方法返回当前时间。要使 `Substitution` 控件正常工作，需要将 `GetTime` 方法添加到 `Substitution` 控件的 `MethodName` 属性中。每次刷新页面时，该方法都会将当前时间返回给 `Substitution` 控件。

- 10. 将 `Substitution` 控件的 `MethodName` 属性设置为 `GetTime`，如图 ASP-9.4 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_667_0.png)

图 ASP-9.4

- 11. 按键盘上的 `F5` 键运行网站。输出结果出现，如图 ASP-9.5 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_667_1.png)

图 ASP-9.5

- 12. 单击**刷新**按钮刷新网页。请注意，Label3 上显示的时间是缓存时间，但 **Substitution** 控件显示的是当前时间，如图 ASP-9.6 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_668_0.png)

图 ASP-9.6

这表明，每次刷新页面时，替换时间都会变化。缓存时间只有在代码中指定的时间段（10 秒）到期后才会变化。

> 您已经在第三部分“标准控件”的第 2 章中学习了 AdRotator。

现在，我们来讨论数据缓存以及使用数据缓存可以执行的不同操作。

## 数据缓存

**数据缓存**也称为应用程序缓存，是整个 ASP.NET 缓存场景中最强大的功能之一。到目前为止，您已经了解了在 ASP.NET 应用程序中启用缓存的声明性方式。但是，数据缓存完全是以编程方式启用缓存。当您需要将自定义数据缓存到缓存内存中时，数据缓存非常有用。例如，如果您需要缓存数据集以便稍后在网站中使用，则可以使用数据缓存。

在 ASP.NET 中，缓存通过两种机制实现：应用程序缓存和页面输出缓存。应用程序缓存允许您缓存生成的数据，例如 **DataSet** 或自定义报表。页面输出缓存保存网页的输出，并在将来重用相同的输出。它支持以下基本类型的依赖模型：

- 文件依赖
- 键依赖
- SQL 依赖
- 聚合依赖
- 时间依赖
- 自定义依赖

.NET 中的数据缓存由 **Cache** 类实现，该类包含在 **System.Web.Caching** 命名空间中。如果要处理简单数据，使用 Cache 类将数据存储到缓存中很容易。**Cache** 类通过使用 **KEY/Value** 格式为您提供了一种存储和访问数据的简单机制，如下面的代码片段所示：

```csharp
Cache["myvalue"] = value
```

使用数据缓存，可以执行以下三项主要任务：

- 向缓存中添加项
- 从缓存中检索项
- 从缓存中删除项

下面逐一详细讨论这些操作。

### 向缓存中添加项

根据向缓存中添加项的需求，您可以使用多种可用技术，从简单到复杂。以下代码片段显示了如何向缓存中添加项：

```csharp
Cache["myvalue"] = value;
```

Cache 类还提供 Cache.Add 和 Cache.Insert 方法向缓存中添加项。当您需要管理缓存的各个方面（例如过期和依赖项）时，这两个方法都很有用，但它们之间有一些差异。Cache.Add 方法始终返回一个对象，而 Cache.Insert 方法不返回任何对象。此外，如果使用 Cache.Insert 方法添加缓存中已存在的项，则 Cache.Insert 方法会替换该项。Cache.Add 方法无法做到这一点。

以下代码片段显示了如何使用 Cache.Insert 方法向缓存中添加项：

```csharp
Cache.Insert("myvalue", value);
```

前面代码片段中使用 Cache.Insert 方法类似于 Cache["myvalue"] = value。但是，使用 Cache.Insert 方法可以做更多事情，例如将依赖项与 Cache.Insert 方法一起使用。依赖项允许基于外部文件来验证缓存项。

例如，缓存完整的可扩展标记语言（XML）文档而不关联依赖功能可能会产生问题。此外，假设用户访问一个未指定依赖项的 XML 文档。在这种情况下，在缓存过期并重新生成之前，用户无法看到服务器中所做的任何修改。因此，在将项插入缓存时会使用文件依赖功能。以下代码片段显示了如何指定项的依赖项：

```csharp
Cache.Insert("MyData", data, new CacheDependency(Server.MapPath("data.xml")));
```

使用 Cache.Insert() 方法时，可以使用时间依赖模型指定绝对过期策略和滑动过期策略。绝对过期设置缓存项过期的绝对时间，而滑动过期会在每次请求页面时重置网页的过期时间。以下代码片段显示了如何使用 Cache.Insert 方法向缓存中添加一个绝对过期时间为五分钟的项：

```csharp
Cache.Insert("Myvalue", value, null, DateTime.Now.AddMinutes(5),
    TimeSpan.Zero)
```

在前面的代码片段中，我们将最后一个参数设置为 TimeSpan.Zero，因为我们不想为项指定滑动过期时间。以下代码片段显示了如何使用滑动过期时间策略：

```csharp
Cache.Insert("Myvalue", value, null, DateTime.MaxValue,
    TimeSpan.FromSeconds(20))
```

前面的代码片段使用滑动过期时间策略将项 Myvalue 插入缓存中 20 秒。

使用滑动过期时间策略时，绝对过期值根本不重要，因为该值会根据滑动过期时间而变化。您还可以通过使用 DateTime.MaxValue 参数来禁用绝对过期时间。例如，如果指定滑动时间为 20 秒，并且该项在第 18 秒被访问，那么整个时间会再次计算为再延长 20 秒，该项在缓存中再保留 20 秒。这意味着，如果最后 20 秒内未访问该项，则 18 秒 + 20 秒 = 38 秒是该项在缓存被销毁之前存在于缓存中的时间。

您还可以在缓存项时通过指定 CacheItemPriority 枚举中的值来定义项的优先级。此优先级设置会告知 Web 服务器该项的重要性。因此，在从缓存中移除项时，Web 服务器会先从缓存中移除低优先级项，再移除高优先级项。**CacheItemPriority** 枚举的可能值列于表 9.8：

**表 9.8：CacheItemPriority 枚举的可能值**

| 值 | 描述 |
|---|---|
| AboveNormal | 指定当服务器释放系统内存时，此级别的缓存项不会频繁被删除 |
| BelowNormal | 指定当服务器释放系统内存时，此级别的缓存项会频繁被删除 |
| Default | 指定缓存项的默认值为 Normal |
| High | 指定当服务器释放系统内存时，此级别的缓存项最不可能被删除 |
| Low | 指定当服务器释放系统内存时，此级别的缓存项最可能被删除 |
| Normal | 指定此级别的缓存项在 **Low** 和 **BelowNormal** 优先级项被删除之后被删除；这是所有缓存项的默认值 |
| NotRemovable | 指定此级别的缓存项不会被自动删除 |

您可以在将项插入缓存时定义 **CacheItemPriority** 枚举，如下面的代码片段所示：

```csharp
Cache.Insert("MyValue", value, null, DateTime.MaxValue,
             TimeSpan.FromSeconds(20), CacheItemPriority.High, null)
```

前面的代码将该项以高优先级插入缓存。

### 从缓存中检索数据

从缓存中检索数据并显示在网页上是 ASP.NET 中最简单的任务之一。要检索数据，需要指定表示数据的键和值，如下面的代码片段所示：

```csharp
value = Cache["MyValue"];
```

需要注意的是，从缓存中检索数据时，应检查数据是否存在于缓存中，如下面的代码片段所示：

```csharp
value = Cache["MyValue"];
if (value == null)
    // Do something here
else
    // Do something here
```

### 从缓存中删除项

通常，使用过期策略来实现数据缓存。此过期策略会根据其中指定的时间限制自动移除数据。但是，有时您需要手动从缓存中删除数据。以下代码片段显示了如何手动删除数据：

```csharp
Cache.Remove("MyData1");
```

### 实现数据缓存

数据缓存用于将自定义数据存储到缓存中。让我们通过在一个新网站中实现数据缓存来理解其概念。请执行以下步骤创建一个名为 **DataCachingExample** 的新网站（该网站也可在随附 CD 上获得）：

- 1. *打开* Microsoft Visual Studio 2010。
- 2. *单击* **文件→新建→网站**。出现“新建网站”对话框。
- 3. *选择* ASP.NET 网站模板，将其*命名*为 **DataCachingExample**，然后单击“确定”按钮。

