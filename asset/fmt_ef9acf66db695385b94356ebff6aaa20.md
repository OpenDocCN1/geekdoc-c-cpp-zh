
- 获取子目录中的文件列表 1396
- 创建、重命名和删除目录 1397
- 使用文件 1398
- 检查文件是否存在及其属性 1404
- 创建、写入和读取文本文件中的数据 1408
- 读取和写入二进制文件 1410

## 第 30 章：使用 XML 和 .NET 1417

### 深入探讨 1418

- .NET Framework 4.0 对 XML 的支持 1418
- `System.Xml` 命名空间 1418
- 使用流式 XML 1419
- `XmlReader` 类 1419
- 使用 `XmlReader` 类验证 XML 文档 1420
- `XmlWriter` 类 1420
- .NET Framework 4.0 中的 DOM 实现 1420
- .NET Framework 4.0 中的 XPath 和 XSLT 1421
- `System.Xml.XPath` 命名空间 1421
- `System.Xml.Xsl` 命名空间 1423
- 使用 ADO.NET 处理 XML 1423
- 使用 XML 进行对象序列化 1423

### 即时解决方案 1425

- 使用流式 XML 1425
- 读取数据 1426
- 验证数据 1427
- 写入数据 1430
- 在 .NET 中实现 DOM 1432
- 按标签名查找元素 1432
- 插入节点 1434
- 导航和转换数据 1435
- 按属性值导航和查找元素 1435
- 转换 XML 1437
- 转换 ADO.NET 和 XML 数据 1438
- 将 ADO.NET 数据转换为 XML 数据 1438

## 第 31 章：C# 2010 中的线程 1447

### 深入探讨 1448

- `Thread` 类 1448
- 多线程 1450
- 线程优先级 1451

### 即时解决方案 1454

- 创建线程 1454
- 启动线程 1454
- 使线程休眠 1455
- 挂起线程 1456
- 恢复线程 1457
- 停止线程 1458
- 创建多线程应用程序 1460
- 设置线程优先级 1461
- 确定线程状态 1463
- 连接线程 1465
- 同步线程 1467
- 总结 1470

## 第 32 章：集合和泛型 1471

### 深入讲解 1472

- 理解集合 1472
- .NET 中的集合类 1473
- `ArrayList` 类 1473
- `Hashtable` 类 1474
- `SortedList` 类 1475
- `Stack` 类 1477
- `Queue` 类 1478
- `BitArray` 类 1479
- 理解泛型 1480
- .NET 中的泛型集合类 1480
- `List<T>` 类 1481
- `LinkedList<T>` 类 1482
- `SortedList<TKey, TValue>` 类 1483
- `Dictionary<TKey, TValue>` 类 1484
- `SortedDictionary<TKey, TValue>` 类 1484
- `Stack<T>` 类 1485
- `Queue<T>` 类 1486
- `HashSet<T>` 类 1486
- 集合和泛型有什么新内容？ 1487
- 泛型中的协变和逆变 1489

### 即时解决方案 1491

- 使用集合类 1491
- 使用 `ArrayList` 类 1491
- 使用 `Hashtable` 类 1494
- 使用 `SortedList` 类 1498
- 使用 `Stack` 类 1501
- 使用 `Queue` 类 1504
- 使用 `BitArray` 类 1507
- 使用泛型集合类 1510
- 使用 `List<T>` 类 1510
- 使用 `LinkedList<T>` 类 1512
- 使用 `SortedList<TKey, TValue>` 类 1516
- 使用 `Dictionary<TKey, TValue>` 类 1518
- 使用 `SortedDictionary<TKey, TValue>` 类 1521
- 使用 `Stack<T>` 类 1523
- 使用 `Queue<T>` 类 1525
- 使用 `HashSet<T>` 类 1527
- 创建自己的泛型集合类 1530
- 在泛型中实现协变和逆变 1535
- 总结 1536

## 第 33 章：.NET 程序集 1537

### 深入讲解 1538

- .NET 程序集 1538
- 程序集清单 1538
- 类型元数据 1540
- 资源 1540
- 程序集类型 1540
- 程序集属性 1541
- 程序集签名 1542
- 程序集存储 1545
- 程序集信息文件 1546
- 程序集配置文件 1546

### 即时解决方案 1549

- 创建共享程序集 1549
- 为程序集强命名 1550
- 将程序集放入全局程序集缓存 1550
- 创建简单客户端 1551
- 创建共享程序集的新版本 1552
- 使用共享程序集的新版本 1552
- 共享程序集的并排执行 1555
- 创建私有程序集 1556
- 创建多文件程序集 1557
- 原生映像生成 1560
- 延迟签名 1561
- 配置程序集查找 1562
- 配置探测 1562
- 为签名程序集配置 `Codebase` 设置 1564
- 为未签名程序集配置 `CodeBase` 设置 1566
- 创建发布者策略 1566
- 总结 1566

## 第 34 章：C# 2010 中的反射 1567

### 深入探讨 1568

- 探索反射过程 1568
- 反射的需求 1568
- 使用反射 1569
- 使用反射进行程序集的动态加载 1570

### 即时解决方案 1572

- 从程序集中获取类和类型信息 1572
- 从类中获取成员信息 1576
- 动态调用程序集中类的方法 1578
- 验证类是否包含方法 1580
- 转储方法及其参数 1582
- 总结 1584

## 第 35 章：C# 2010 中的 .NET Remoting 1585

### 深入探讨 1586

- .NET Remoting 架构 1586
- 应用程序域 1587
- 可远程对象和不可远程对象 1588
- 设置 Remoting 通信 1590
- 通道 1591
- 消息接收器 1594
- 格式化程序 1594
- 代理 1597
- 远程对象的托管 1598
- 设置对象的租约时间 1598

### 即时解决方案 1599

- 创建和使用应用程序域 1599
- 在另一个应用程序域中使用对象 1601

## 第 36 章：.NET 4.0 中的安全 1621

### 深入探讨 1622

- 在 .NET Framework 中介绍代码验证和安全 1622
- 类型安全代码 1623
    - 可验证的类型安全 MSIL 代码 1624
    - .NET Framework 4 中的安全更改 1625
    - 安全策略简化 1625
    - 安全透明度级别 2 1625
    - 已废弃的权限请求 1625
    - 条件 APTCA 1626
    - 证据对象 1626
    - 证据集合 1626
- 介绍身份验证和授权 1626
- 基于角色的安全 1627
- 主体对象 1628
- 身份对象 1629
- 基于角色的安全检查 1630
- `Roles` 类 1634
- 成员资格功能 1652
- `ActiveDirectoryMembershipProvider` 1652
- `SqlMembershipProvider` 1653
- `Membership` 类 1655
- `MembershipUser` 类 1656

### 即时解决方案 1657

- 确定代码是否可验证类型安全 1657
- 使用基于角色的安全对用户进行身份验证和授权 1659
- 执行基于角色的安全检查 1666
- 管理角色和用户 1670
- 在 ASP.NET 中使用匿名身份验证 1675
- 在 ASP.NET 中使用 Windows 身份验证 1677
- 在 ASP.NET 中使用表单身份验证 1683
- 在 ASP.NET 应用程序中使用模拟 1686
- 使用 `Membership` 类创建用户 1689
- 验证和检索用户 1692
- 理解堆栈遍历 1694
- 安全注意事项 1698
- 总结 1698

## 第 37 章：使用 Active Directory 1699

### 深入探讨 1700

- Active Directory 的结构 1700
- Active Directory 的意义 1701
- 探索用户账户和组 1701
- 管理 Active Directory 1702
- `System.DirectoryServices` 命名空间 1703
- 指定绑定路径 1706
- 创建新对象 1706
- 修改活动数据对象 1707

## CD 上的奖励章节/附录

### 在 Active Directory 中搜索对象 170

### 即时解决方案 1709

- 创建用户 170
- 创建组 1709
- 从 Windows Forms 应用程序访问 Active Directory 1714
- 总结 1716

## 第 38 章：案例研究：体育网站 1717

### 索引 1723

### CD-ROM 上的内容 1736

- 第1章：Windows Forms 控件：`Button`、`Label`、`TextBox`、`RichTextBox` 和 `MaskedTextBox`
- 第2章：Windows Forms 控件：`RadioButton`、`CheckBox`、`ListBox`、`CheckedListBox` 和 `ComboBox`
- 第3章：Windows Forms 控件：`ListView`、`TreeView`、`ImageList`、`PictureBox`、`Panel`、`GroupBox` 和 `TabControl`
- 第4章：Windows Forms 控件：`SplitContainer`、`ScrollBar`、`TrackBar`、`ToolTip`、`NotifyIcon`、`MonthCalendar`、`DateTimePicker`、`Timer` 和 `ProgressBar`
- 第5章：Windows Forms 控件：`ToolStrip`、`MenuStrip`、`ContextMenuStrip`、`StatusStrip` 和对话框控件
- 第6章：ASP.NET 中的验证控件
- 第7章：开发 ASP.NET AJAX 应用程序
- 第8章：C# 2010 中使用 COM+ 应用程序
- 第9章：应用程序全球化
- 第10章：.NET 4.0 中的密码学
- 附录 A：介绍 SOA
- 附录 B：介绍云计算
- 附录 C：联合
- 附录 D：介绍 MAF 和 MEF 框架

## 术语表

## 引言

恭喜您购买《C# 2010 编程黑皮书》！这本书表明我们持续致力于根据尊贵读者的需求，通过深入研究来提供高质量的 IT 书籍。本书是 Kogent Learning Solutions Inc. 和 Dreamtech Press 的作者与编辑们丰富的教学智慧和技术精准性的结晶，并承诺为希望在 C# 2010 和 .NET Framework 4.0 领域脱颖而出的学生和 IT 专业人士提供丰富的解决方案。这本书进一步延伸了我们的理念，即提供关于新兴技术的全面且易于理解的参考资料。本书在编写时考虑了 C# 2010 的多样化读者群，并通过呈现相关、恰当和真实的示例，承诺提供卓越的学习体验。此外，本书还包括代码片段和可执行应用程序，以演示与 C# 2010 相关的各种概念的实施。

我们设计这本书是为了与您一起成长，为您在迈向软件精通的过程中提供所需的参考资料。

C# 是一种专门为与 .NET Framework 配合使用而设计的编程语言，它为您提供了几乎可以开发任何类型应用程序的环境。它是一种简单、高效、富有生产力且类型安全的语言，源自流行的 C 和 C++ 语言。许多公司正在使用 C# 2010 和 .NET Framework 4.0 来构建健壮、可靠和可扩展的应用程序。C# 2010 的影响力正在迅速蔓延，没有停止或回头的余地！我们希望您在阅读本书时的学习体验，能像我们在撰写和编辑本书时所感受到的那样，令您无法抗拒。

## 目标读者

本书对于那些想从头开始学习 C# 的人，以及那些已经在使用 C# 2010 开发应用程序的人来说，同样有益。因此，《C# 2010 编程黑皮书》在真正意义上是一本出色的指南——介绍了瞬息万变的 C# 世界以及与之相关的各种编程技术。

## 关于本书

本书由七个部分组成，如下所示：

- 第一部分 – .NET Framework 4.0 和 Visual Studio 2010 – 介绍 .NET Framework 4.0 和 Visual Studio 2010 的基本知识和基本概念。
- 第二部分 – C# 编程语言 – 介绍 C# 语言的基本概念，例如变量声明、流程控制、异常处理和动态数据类型。
- 第三部分 – Windows Forms 和 Windows Presentation Foundation (WPF) – 介绍 Windows Forms 和 WPF 的基础知识，以及如何创建它们的应用程序。
- 第四部分 – ASP.NET 4.0 和 Silverlight – 说明如何使用 ASP.NET 和 Silverlight 技术创建 Web 应用程序和网站。
- 第五部分 – 服务与部署 – 说明如何创建各种类型的服务（如 Web 服务和 WCF 服务），以及如何在 Visual Studio 2010 中部署应用程序。
- 第六部分 – 在 C# 2010 中与数据库交互 – 说明如何在 .NET Framework 中创建 SQL 对象（如存储过程和触发器），以及如何在 .NET 应用程序中从数据库访问数据，包括 ADO.NET 和 LINQ。

## 如何使用本书

在本书中，所有应用程序都是使用 Visual Studio 2010 IDE 开发的。Visual Studio 2010 提供了用于开发控制台、Windows、WPF、WCF、WF、Silverlight 和 Web 应用程序的内置模板。

## 约定

我们在整本书中使用了标准约定。本节帮助您熟悉这些约定，以确保卓越的学习体验。

程序代码以代码清单的形式表示，如下所示：

清单 20.1：显示 Service1.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;
using System.Text;
namespace MywindowsService {
    public partial class MyService : ServiceBase {
        public MyService() {
            InitializeComponent();
        }
        protected override void OnStart(string[] args) {
            EventLog.WriteEntry("Starting MyService");
        }
        protected override void OnStop() {
            EventLog.WriteEntry("Stopping MyService");
        }
    }
}
```

保留字、属性、方法、事件、类、接口、命名空间（在代码片段中使用）、异常等，在正文中使用不同的字体来突出显示。

每个图都有一个标题，以帮助您更好地理解该图。

![](img/e073a4882197be4ab61103cbe0bcb394_40_0.png)

图 8.20：修改 Program.cs 文件

注释以以下格式表示：

#### 注意

当您在计算机上运行应用程序时，应更改代码隐藏文件中的连接字符串。

表格有编号，并放置在章节中引用的正下方，如下所示：

表 30.2：`XmlReader` 类用于读取 XML 数据的方法

| 方法名称 | 说明 |
| --- | --- |
| `Read()` | 将光标位置移动到下一个节点。 |
| `ReadStartElement()` | 在验证当前节点是否为第一个元素后，将光标位置移动到下一个节点。如果当前节点不是开始元素，则会引发 `XmlException` 类型的异常。调用此方法的效果等同于先调用 `IsStartElement()` 方法，然后再调用 `Read()` 方法。 |
| `ReadString()` | 从元素读取文本数据。此方法返回一个包含数据的字符串对象。 |
| `ReadElementString()` | 与 `ReadString()` 方法的工作原理类似。唯一的区别是，您可以选择将元素名称传递给此方法。 |

## 其他资源

C# 2010 附带了大量的文档——有数百本书值得参考。这些文档托管在网上，您可以使用 Web 浏览器访问它们。当然，网上有很多关于 C# 语言的网页。以下是一些：

- http://msdn.microsoft.com
- http://www.asp.net
- http://msdn.microsoft.com/vstudio/
- http://www.w3schools.com
- http://weblogs.asp.net/scottsgu/default.aspx

## 黑皮书哲学

> “复杂性会扼杀一切。它吸走开发者的生命，使产品难以规划、构建和测试，它会引入安全挑战，并导致最终用户和管理员的挫败感。”

Ray Ozzie – 微软公司首席软件架构师
