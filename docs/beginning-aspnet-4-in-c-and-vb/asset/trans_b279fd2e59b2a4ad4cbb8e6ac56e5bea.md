
![](img/d7d2ffa0a76feaab821930e95daace93_663_0.png)

使用 CultureAndRegionInfoBuilder 类的构造函数时，可以传递文化的名称。构造函数的第二个参数需要 CultureAndRegionModifiers 类型的枚举。该枚举允许三个值之一：Neutral 表示中性文化，Replacement 如果应替换现有的 Framework 文化，或 None。

在实例化 CultureAndRegionInfoBuilder 对象后，可以通过设置属性来配置文化。借助此类属性，可以定义所有文化和区域信息，例如名称、历法、数字格式、度量信息等。如果文化应基于现有文化和区域，可以使用 LoadDataFromCultureInfo() 和 LoadDataFromRegionInfo() 方法设置实例的属性，然后通过设置属性更改不同的值。

调用 Register() 方法会将新文化注册到操作系统中。实际上，你可以在目录 <windows>\Globalization 中找到描述文化的文件。查找扩展名为 .nlp 的文件。

```csharp
using System;
using System.Globalization;

namespace CustomCultures
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Create a Styria culture
                var styria = new CultureAndRegionInfoBuilder("de-AT-ST",
                    CultureAndRegionModifiers.None);
                var cultureParent = new CultureInfo("de-AT");
                styria.LoadDataFromCultureInfo(cultureParent);
                styria.LoadDataFromRegionInfo(new RegionInfo("AT"));
                styria.Parent = cultureParent;
                styria.RegionNativeName = "Steiermark";
                styria.RegionEnglishName = "Styria";
                styria.CultureEnglishName = "Styria (Austria)";
                styria.CultureNativeName = "Steirisch";
                
                styria.Register();
            }
            catch (UnauthorizedAccessException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

由于在系统上注册自定义语言需要管理员权限，因此需要一个应用程序清单文件来指定请求的执行权限。在项目属性中，需要在应用程序设置中设置清单文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
    <security>
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
        <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
      </requestedPrivileges>
    </security>
  </trustInfo>
</asmv1:assembly>
```

代码片段 CustomCultures/app.manifest

新创建的文化现在可以像其他文化一样使用：

```
var ci = new CultureInfo("de-AT-ST");
Thread.CurrentThread.CurrentCulture = ci;
Thread.CurrentThread.CurrentUICulture = ci;
```

你可以使用该文化进行格式设置，也可用于资源。如果再次启动本章前面编写的 Cultures in Action 应用程序，你也可以看到自定义文化。

## 摘要

本章讨论了 .NET 应用程序的全球化和本地化。

在应用程序全球化的上下文中，你学习了使用 System.Globalization 命名空间来格式化依赖于文化的数字和日期。此外，你了解到默认情况下字符串排序取决于文化，并且你使用了不变文化来进行与文化无关的排序。使用 CultureAndRegionInfoBuilder 类，你学习了如何创建自定义文化。

应用程序的本地化是通过使用资源实现的。资源可以打包到文件、卫星程序集中，或自定义存储如数据库中。用于本地化的类位于 System.Resources 命名空间中。对于从其他位置（如卫星程序集或资源文件）读取资源，可以创建自定义资源读取器。

## 23

## System.Transactions

### 本章内容

- 事务阶段和 ACID 属性
- 传统事务
- 可提交事务
- 事务提升
- 依赖事务
- 环境事务
- 事务隔离级别
- 自定义资源管理器
- Windows 7 和 Windows Server 2008 中的事务

全部或全不 — 这是事务的主要特征。写入几条记录时，要么全部写入，要么全部撤销。如果写入一条记录时出现任何一个失败，事务中完成的所有其他操作都将被回滚。

事务通常与数据库一起使用，但使用 System.Transactions 命名空间中的类，你也可以对易失性或基于内存的对象（如对象列表）执行事务。对于支持事务的列表，如果添加或删除对象且事务失败，列表操作会自动撤销。向基于内存的列表写入可以在与写入数据库相同的事务中完成。

自 Windows Vista 以来，文件系统和注册表也获得了事务支持。写入文件和在注册表中进行更改支持事务。

## 概述

什么是事务？想想从网站订购书籍。订购书籍的过程会从库存中移除你想要购买的书籍并将其放入你的订单箱中，并且你的书籍费用会被计入信用卡。对于这两个操作，要么两个操作都成功完成，要么两个操作都不发生。如果从库存获取书籍时出现故障，就不应扣款。事务处理此类场景。

事务最常见的用途是在数据库中写入或更新数据。事务也可以在向消息队列写入消息，或向文件或注册表写入数据时执行。多个操作可以成为单个事务的一部分。

![](img/d7d2ffa0a76feaab821930e95daace93_667_0.png)

图 23-1 显示了事务中的主要参与者。事务由事务管理器管理和协调，而资源管理器管理影响事务结果的每个资源。事务管理器与资源管理器通信以确定事务的结果。

![](img/d7d2ffa0a76feaab821930e95daace93_667_1.png)

图 23-1

### 事务阶段

事务的三个阶段是活动、准备和提交阶段：

- **活动阶段** — 在活动阶段，事务被创建。管理资源事务的资源管理器可以加入事务。
- **准备阶段** — 在准备阶段，每个资源管理器都可以定义事务的结果。当事务创建者发送提交以结束事务时，该阶段开始。事务管理器向所有资源管理器发送 Prepare 消息。如果资源管理器能够成功产生事务结果，它会向事务管理器发送 Prepared 消息。资源管理器如果准备失败，可以通过向事务管理器发送 Rollback 消息强制回滚来中止事务。在发送 Prepared 消息后，资源管理器必须保证在提交阶段成功完成工作。为此，持久性资源管理器必须记录包含准备状态信息的日志，以便在准备阶段和提交阶段之间出现例如断电等情况时可以从那里继续。
- **提交阶段** — 当所有资源管理器都成功准备后，提交阶段开始。这是在从所有资源管理器收到 Prepared 消息时。然后事务管理器可以通过向所有参与者发送 Commit 消息来完成工作。资源管理器现在可以完成事务的工作并返回 Committed 消息。

