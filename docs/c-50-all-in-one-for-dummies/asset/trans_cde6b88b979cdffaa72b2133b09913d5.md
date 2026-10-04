

# 创建 ASMX 服务 759

右键点击 SharpAsmx 项目，通过选择“新建项”并从列表中选择“ADO.NET 实体模型”来添加实体数据模型。

（它在“数据”分类下。）我将其命名为 SHARP.edmx。

当实体数据模型向导出现时，选择“从数据库生成”并点击“下一步”。

在“您的数据连接”中，选择你在第 1 步中添加的 ConferenceDb；保持其余默认值不变。

当系统询问你是否将文件复制到项目时，选择“否”。

你不需要在项目中到处散着数据库副本。

在“您的数据库对象”中，选择除 sysdiagrams 以外的所有表，并将“模型命名空间”更改为 ConferenceDB。

图 2-3 显示了一个示例。

6. 点击“完成”。

这就是你设置 ASMX Web 项目的方法。现在你拥有了一个数据源、一个实体模型（你可以使用组织的领域模型，或者手动编写的过程和 ADO.NET，或者任何东西），以及一个服务的起点。

接下来，你添加一些让你的用户界面产生意义的服务。关于这一点有两种学派。第一，你可以将实体模型封装在服务命名空间本身。第二，你可以编写一个独立的业务层，并仅通过服务调用业务层（BL）方法。

![](img/6df7bb88e9302e98442acc219cfbd7fc_784_0.png)

图 2-3：将 Sharp 表格添加到模型中。

![](img/6df7bb88e9302e98442acc219cfbd7fc_784_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_784_2.png)

# 760 创建 ASMX 服务

决定性因素是复用。如果你以后需要将恰好此逻辑封装进一个独立的应用程序（任何不使用服务的程序），那么就创建一个单独的 BL。为了简单起见，我们将采用前者。

- 1. 使用默认模板，删除默认的 HelloWorld 方法，并为新的 `conferencesAtLocation` 方法编写一个方法签名。

它将接受一个 `conferenceID`（可能来自网站导航）并返回该位置的会议列表。

```
List<Conference> conferencesAtLocation(int location)
{

}
```

- 2. 第一步仅仅是从实体数据模型中获取实体。

通过添加粗体行来实现。这些行为 Entity Data Framework 设置了上下文。然后获取会议列表：

```
List<Conference> conferencesAtLocation(int locationId)
{
ConferenceDbEntities conferenceContext = new ConferenceEntities();
DbSet<Conference> allConferences = conferenceContext.Conferences;
}
```

- 3. 编写一个 Linq 查询来获取具有 locationId 的会议。

这在粗体行中：

```
List<Conference> conferencesAtLocation(int locationId)
{
ConferenceDbEntities conferenceContext = new ConferenceEntities();
DbSet<Conference> allConferences = conferenceContext.Conferences;
var conferenceQuery = from c in allConferences
    where c.LocationId == locationId
    select c;
}
```

- 4. 为了使用 Linq 查询的结果，你必须使用迭代器并释放上下文；最后返回结果。

这些步骤在添加的粗体行中：

```
List<Conference> conferencesAtLocation(int locationId)
{
ConferenceDbEntities conferenceContext = new ConferenceEntities();
DbSet<Conference> allConferences = conferenceContext.Conferences;
var conferenceQuery = from c in allConferences
    where c.LocationId == locationId
    select c;
List<Conference> locationConferences = conferenceQuery.ToList();
conferenceContext.Dispose();

return locationConferences;
}
```

*

# 创建 ASMX 服务

# 5. 要使其成为服务，你需要在方法签名上添加 `[WebMethod]` 装饰器，然后就完成了：

```
[WebMethod]
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet<Conference> allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
        where c.LocationId == locationId
        select
    List<Conference> locationConferences = conferenceQuery.ToList();
    conferenceContext.Dispose();

    return locationConferences;
}
```

# 6. 按 F5 运行测试页面并点击 `conferencesAtLocation` 方法链接；在字段中输入 3。

如果一切正常，结果应该像图 2-4 所示返回。
那么进入 SOAP 的其他所有内容呢？安全性、事务之类的？这些都已内置了，但已远远超出了本文的范围。

例如，查看一下 `SoapHeader` 属性。它允许你在 Web 方法上指定即使是最复杂的安全属性。还有更多内容，请查看 MSDN。

![](img/6df7bb88e9302e98442acc219cfbd7fc_786_0.png)

图 2-4：
服务的运行。

第七 卷
第 2 章
使用 ASMX 构建 Web 服务

# 762 创建 ASMX 服务

# 部署

部署服务就像任何其他服务一样。

ASMX 相比 WCF 的一个优势在于它更简单。事实上，ASMX 仅仅是一组规则。

你需要知道的重要事项：部署后，你将看到图 2-5 中的消息。

![](img/6df7bb88e9302e98442acc219cfbd7fc_787_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_787_1.png)

# 使用服务

使用服务就像任何其他服务一样。事实上，ASMX 设置起来容易得多。

- 1. 创建一个新的控制台应用程序。
- 2. 右键点击项目并添加“服务引用”。
- 3. 选择 URL。
- 4. 选择命名空间。
- 5. 点击确定。

Visual Studio 为你做了大量工作。

```
using System;
using System.Collections.Generic;
using System.Linq;

namespace ConsoleApplication
{
    class Program
    {
        static void Main(string[] args)
        {
        
        
        
        
        
        
        
        }
    }
}
```

# 创建 ASMX 服务

# 764 创建 ASMX 服务

`conferencesLocation` 方法现在返回一个数组而不是 `List<Conference>`。消费语言不需要有泛型，但必须有数组。

```
SharpReference.SoapClient serviceReference = new SharpReference.SoapClient();
SharpReference.Conference[] conferences = serviceReference.conferencesLocation(3);
Console.WriteLine("There will be {0} conferences at location.", conferences.Length);
Console.ReadKey();
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_789_0.png)

图 2-7：运行服务。

右键点击控制台应用程序并按 F5。控制台应用程序应该启动，它应该像在列表中一样，找到数组中的那两行。

