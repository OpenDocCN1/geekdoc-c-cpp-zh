

## 案例研究

## Claytor's Cottages

修改第 2 章 Claytor's Cottages 案例研究项目中的 Reservations 选项，使用 WCF 服务进行计算。

> 注：如果你愿意，也可以使用日历控件，在这种情况下你不需要用于入住天数的文本框或用于周末/工作日的复选框。

### 表示层

表单应包含用于 King、Queen 或 Double 的下拉列表或单选按钮。包含用于输入客户姓名、电话号码、入住天数、信用卡类型（使用组合框选择 Visa、Mastercard 和 American Express）以及信用卡号码的文本框。姓名、入住天数和信用卡号码为必填字段。使用复选框选择周末或工作日费率，并使用复选框选择 AARP 或 AAA 会员。在表单上显示价格。

### WCF 服务层

使用以下表格计算价格，该表格也出现在第 2 章案例研究中。添加 7% 的房间税。AAA 和 AARP 客户可享受 10% 的折扣费率。

| Beds | Sunday through Thursday rate | Weekend rate (Friday and Saturday) |
| King | 95.00 | 105.00 |
| Queen | 85.00 | 95.00 |
| Double | 69.95 | 79.95 |

## Christian's Car Rentals

修改第 2 章的 Christian's Car Rentals 项目。使用 WCF 服务对 Rentals 表单进行计算编码。

确保已输入驾驶执照，并且租用天数大于 0。

### 表示层

表示层应包括汽车尺寸的数据输入：Economy、Mid size 或 Luxury。包含用于输入租车人姓名、电话号码、驾驶执照、信用卡类型和信用卡号码的文本框。使用组合框选择信用卡类型。分组框应包含租用天数、起始里程表读数和结束里程表读数。

在允许数据发送到服务组件之前，验证结束里程表读数是否大于起始里程表读数。

### WCF 服务

如果行驶里程未超过平均每天租用 100 英里，则不收取里程费。使用以下费率表，该表也出现在第 2 章案例研究中。

| Car size | Daily rate | Mileage rate |
| Compact | 26.95 | .12 |
| Mid size | 32.95 | .15 |
| Luxury | 50.95 | .20 |

## 第 7 章

## Web 应用程序

- 在本章结束时，你将能够 ...
- 
- 1. 讨论基于 Web 的应用程序的概念。
- 2. 了解构成 Web 项目的文件类型。
- 3. 区分各种类型的按钮控件。
- 4. 了解 Web 应用程序使用的事件结构。
- 5. 在页面上包含超链接和链接按钮。
- 6. 从一个 Web 页面导航到另一个 Web 页面。
- 7. 使用 ASP.NET 主页设计一致的布局。
- 8. 创建并应用级联样式表。
- 9. 使用 Validation 控件验证 Web 输入。
- 10. 在页面之间维护状态（数据值）。
- 11. 针对新用户和现有用户集成 Login 控件。
- 12. 使用 AJAX 控件并执行部分页面更新。

在前几章中，你使用 Windows Forms 工作并创建了在 Windows 环境中运行的应用程序。.NET 开发最强大的功能之一是能够创建可在各种平台上运行的应用程序。本章向你介绍 Web 服务器控件和创建 Web 项目。

> 重要软件说明：Microsoft 有一个用于开发 Web 应用程序的产品：Visual Web Developer 2008 Express Edition，它是 Visual Studio 的精简子集。本章使用 Visual Studio Professional Edition 创建，但项目也可以使用 Visual Web Developer（VWD）完成。如果使用 VWD，步骤和屏幕截图可能会略有不同。如果你使用的是 Windows 应用程序的 Visual Basic Express Edition，你需要下载并安装 Visual Web Developer 来进行 Web 应用程序开发。

## Web 应用程序

为 Internet 开发应用程序与创建 Windows 程序有很大不同。Visual Studio 尽可能让你轻松地从一个开发环境过渡到另一个开发环境。但要成为一名有效的 Web 开发人员，你必须了解这些差异。

Windows Forms 允许你开发可在任何安装 Windows 操作系统的系统上运行的应用程序；Web Forms 是你跨平台开发的入口。你会注意到的第一个主要区别是 Web Form 在 Internet Explorer 或 Mozilla Firefox 等浏览器应用程序中显示，而不是在桌面上。最常见的访问方式是通过 Web。

什么是 Internet？许多人定期使用 Internet，但并不真正了解其基础。Internet 实际上只是一个极大的计算机网络，而万维网（WWW）是驻留在 Internet 上的超链接文档系统。没有人拥有或控制该网络。要使用该网络，计算机必须具有某种类型的连接。通常，个人从 AOL、Earthlink 或 MSN 等 Internet 服务提供商（ISP）获取连接。大多数电话公司和有线电视公司也提供服务。

## 客户端/服务器 Web 应用程序

大多数 Windows 应用程序是独立应用程序；Web 应用程序需要服务器和客户端。Web 服务器将 Web 页面发送到客户端，页面在浏览器应用程序中显示（图 7.1）。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_299_0.png)

### 图 7.1

服务器将 Web 页面交付给客户端，页面在浏览器窗口中显示。服务器可以位于远程机器上，也可以与客户端位于同一台机器上。

## Web 服务器

要发布 Web 应用程序，你必须使用远程 Web 服务器或将本地机器设为 Web 服务器。你可以在本地机器上开发应用程序，然后稍后将其发布到 Web 服务器。使开发机器成为服务器的常见方法是通过安装 Internet Information Services（IIS）。IIS 处理 Web 服务器功能，浏览器充当客户端。但是，你不需要 IIS 来创建 Web 项目；Visual Studio IDE 包含一个开发 Web 服务器，你也可以使用任何支持 ASP.NET v3.5 的可用 Web 服务器，例如 Apache。

## Web 客户端

浏览器显示用超文本标记语言（HTML）编写的页面。页面还可能包含以脚本形式存在的编程逻辑，例如 JavaScript、VBScript 或 JScript，或作为 Java 小程序。浏览器呈现页面并在本地系统上显示它。

你可能见过在不同浏览器或同一浏览器的不同版本中显示不同的 Web 页面。尽管有许多浏览器应用程序可用，但最常见的是 Internet Explorer、Mozilla Firefox、Opera、Safari 和 Netscape Navigator。

你可能知道你的用户使用的是哪个浏览器，例如当你为公司内部网络，即内联网编程时。或者你可能开发在 Internet 上运行的应用程序，可能在任何浏览器中显示。如果你的项目将在不同浏览器上运行，你应该在多个浏览器上测试并检查输出。

## 浏览器支持

众所周知，ASP.NET 应用程序在 Internet Explorer 中运行最佳。但是，你可以在任何浏览器中运行应用程序。ASP.NET 应用程序知道它正在运行的浏览器。它发送给客户端的 HTML 会根据浏览器的功能进行定制。例如，如果浏览器能够处理级联样式表，则字体样式信息将使用样式格式化；否则字体格式将以其他方式发送，例如 Font 标签。

## Web 页面

HTML Web 页面的一个特征是它们是无状态的。也就是说，页面不会从一次调用到下一次调用存储其内容的任何信息。已经开发出几种技术来解决这一限制，包括在本地机器上存储“cookie”以及将状态信息作为页面地址的一部分发送，称为统一资源定位符（URL）。服务器然后可以根据需要将状态信息随下一版本的页面一起发送回来。有关管理状态的更多信息，请参阅本章后面的“状态管理”。

当用户请求 Web 页面时，浏览器（客户端）向服务器发送请求。服务器可能会发送预格式化的 HTML 文件，或者服务器上的程序可能会动态生成渲染页面的必要 HTML。Microsoft 用于动态生成 HTML 页面的技术之一是活动服务器页面（ASP）。

