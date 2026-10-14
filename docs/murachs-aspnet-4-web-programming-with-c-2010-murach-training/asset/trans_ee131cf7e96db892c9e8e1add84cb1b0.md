

## 订单表单的代码隐藏文件 (Order.aspx.cs)

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data;

public partial class Order : System.Web.UI.Page
{
    private Product selectedProduct;

    protected void Page_Load(object sender, EventArgs e)
    {
        if (!IsPostBack)
            ddlProducts.DataBind();

        selectedProduct = this.GetSelectedProduct();
        lblName.Text = selectedProduct.Name;
        lblShortDescription.Text = selectedProduct.ShortDescription;
        lblLongDescription.Text = selectedProduct.LongDescription;
        lblUnitPrice.Text = selectedProduct.UnitPrice.ToString("c");
        imgProduct.ImageUrl = "Images/Products/" + selectedProduct.ImageFile;
    }

    private Product GetSelectedProduct()
    {
        DataView productsTable = (DataView)
            AccessDataSource.Select(DataSourceSelectArguments.Empty);
        productsTable.RowFilter =
            "ProductID = '" + ddlProducts.SelectedValue + "'";
        DataRowView row = (DataRowView)productsTable[0];

        Product p = new Product();
        p.ProductID = row["ProductID"].ToString();
        p.Name = row["Name"].ToString();
        p.ShortDescription = row["ShortDescription"].ToString();
        p.LongDescription = row["LongDescription"].ToString();
        p.UnitPrice = (decimal)row["UnitPrice"];
        p.ImageField = row["ImageFile"].ToString();
        return p;
    }

    protected void btnAdd_Click(object sender, EventArgs e)
    {
        CartItemList cart = CartItemList.GetCart();
        CartItem cartItem = cart[selectedProduct.ProductID];

        if (cartItem == null)
            cart.AddItem(selectedProduct, Convert.ToInt32(txtQuantity.Text));
        else
            cartItem.AddQuantity(Convert.ToInt32(txtQuantity.Text));

        Response.Redirect("Cart.aspx");
    }
}
```

![](img/c024ccf88e28c30c07dd410d4342288f_44_0.png)

## ASP.NET 应用程序如何编译和运行

图 1-12 中的图表显示了当用户请求 ASP.NET 应用程序的页面时幕后实际发生的情况。在步骤 1 中，ASP.NET 运行时读取请求的网页的 aspx 文件并生成一个类和一个 partial 类。partial 类包含表单及其包含的控件的声明，并取名为代码隐藏文件中定义的 partial 类相同的名称（本例中为 Order）。在步骤 2 中，这些 partial 类被编译以创建一个提供页面所有事件处理代码的单个类。结果存储在单个程序集（dll 文件）中。

ASP.NET 运行时生成的类包含实际创建 ASP.NET 页面的代码。该类以网页的 aspx 文件的名称加上 _aspx 为名，因此本例中名称为 Order_aspx。在步骤 3 中，该类被编译并存储在另一个程序集中。因为该类继承自 Order 类，所以从 Order_aspx 类实例化对象将包含创建页面的代码，以及 Order 类提供的事件处理代码。

在步骤 4 中，在页面类编译后，ASP.NET 运行时调用 C# 编译器编译应用程序 App_Code 文件夹中的任何类文件。对于购物车应用程序而言，这意味着 CartItem、CartItemList 和 Product 类被编译，结果保存在单个程序集中。

所有文件编译成程序集后，ASP.NET 创建页面的一个实例并引发适当的事件。然后，事件由页面的事件处理程序处理，页面的 HTML 被渲染。为了完成往返，页面的 HTML 文档被传回 Web 服务器并发送到用户的浏览器。

请注意，前四个步骤仅在第一次访问 aspx 页面时执行。这是因为 ASP.NET 缓存了这些步骤创建的程序集。然后，当再次访问页面时，重用已保存的程序集，因此应用程序无需重新编译。但是，ASP.NET 会比较源文件的时间戳与 dll 文件的时间戳。如果任何源文件自上次编译以来已被修改，ASP.NET 会自动重新编译它们。

## ASP.NET 应用程序如何编译

![](img/c024ccf88e28c30c07dd410d4342288f_46_0.png)

## 当请求 ASP.NET 页面时会发生什么

- 1. ASP.NET 运行时处理 .aspx 文件并生成一个 partial 类（Order），其中包含表单及其控件的声明，以及一个类（Order_.aspx），其中包含将初始化表单、实例化控件并生成网页 HTML 的代码。
- 2. C# 编译器将包含控件声明的 partial 类与表单的代码隐藏文件定义的 partial 类编译成一个 *程序集*（.dll），为请求的页面提供事件处理代码。
- 3. C# 编译器编译 Order_.aspx 类，该类继承第一个编译的类（Order），并将结果保存为在请求页面时执行的程序集。
- 4. 如有必要，C# 编译器编译存储在应用程序 App_Code 文件夹中的任何其他类文件。这些类保存在单个程序集中。
- 5. ASP.NET 从页面的最终程序集创建页面的一个实例。然后，ASP.NET 引发适当的事件，这些事件由页面的事件处理程序处理，页面生成传回 Web 服务器以供响应的 HTML。

## 描述

- * 此过程的前四个步骤仅在第一次请求 aspx 页面时执行。此后，页面直接从编译后的程序集中处理。
- 你添加到网站的 Web 表单的默认名称是 Default.aspx，而该表单的代码隐藏类的名称是 _.Default。

图 1-12 ASP.NET 4 应用程序如何编译和运行

## 视角

现在你已经阅读了本章，你应该对 ASP.NET 应用程序的工作原理以及开发这些应用程序所需的软件有大致的了解。以此为背景，你已准备好学习如何自行开发 ASP.NET 应用程序。而这正是你在接下来的两章中将学习的内容。

## 术语

- web application
- web page
- web form
- client/server application
- client
- server
- HTTP (Hypertext Transfer Protocol)
- web browser
- web server
- IIS (Internet Information Services)
- DBMS (database management system)
- LAN (local area network)
- intranet
- static web page
- HTML document
- HTML (Hypertext Markup Language)
- URL (Uniform Resource Locator)
- HTTP request
- HTTP response
- domain name
- dynamic web page
- server control
- application server
- application mapping
- round trip
- postback
- state
- stateless protocol
- view state
- session state
- session state object
- session ID
- application state
- application state object
- profile
- .NET Framework
- .NET Framework Class Library
- class
- namespace
- CLR (Common Language Runtime)
- IL (Intermediate Language)
- MSIL (Microsoft Intermediate Language)
- Common Type System
- standalone environment
- development server
- SQL Server Express
- FPSE (FrontPage Server Extensions)
- FTP (File Transfer Protocol)
- FTP server
- business class
- aspx code
- code-behind file
- page directive
- attribute
- render
- assembly

## 关于本书的应用程序

你可以从我们的网站（www.murach.com）下载本书中介绍的所有应用程序。然后，你可以运行这些应用程序，查看其所有代码，并在自己的系统上进行实验。有关下载和运行这些应用程序的更多信息，请阅读附录 A。

## 关于练习

如果你是 ASP.NET Web 编程的新手，我们建议你在完成本书前三个部分中每章的学习后练习所学内容。为帮助你做到这一点，我们为这些章节提供了练习。这些练习中的大多数使用可以从我们网站下载的目录和文件。因此，在开始练习之前，你需要安装这些目录和文件。安装后，它们将被放置在 C 盘上的一个名为 aspnet4_cs 的目录中。

## 练习 1-1 使用你的 Web 浏览器运行 Internet 应用程序

- 1. 打开你的 Web 浏览器并输入此 URL：
  `http://www.microsoft.com`
  然后，搜索有关 Visual Web Developer 2010 Express Edition 的信息。这当然是你可以免费下载 Visual Web Developer 2010 Express 和 SQL Server 2008 Express 的网站。随着你从一个页面移动到另一个页面，注意大多数都是动态的 aspx 页面。
- 2. 在你的 Web 浏览器中输入此 URL：
  `http://www.discountasp.net`
  然后，单击主页上的一些链接，并注意哪些页面是静态的，哪些是动态的。

