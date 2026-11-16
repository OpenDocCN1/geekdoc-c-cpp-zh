
现在，当你运行应用程序时，应该在主页上看到呈现的附加消息 "Hello from the controller!"。

在本节中，我们介绍了在 ASP.NET Core 3 MVC 应用程序中创建控制器和视图的过程，这两者是处理请求和呈现动态内容的核心组件。我们学习了如何创建控制器、添加操作方法，并使用 Razor 语法创建相应的视图。我们还探讨了如何将数据从控制器传递到视图，从而生成动态和个性化的内容。掌握这些知识后，你现在可以构建更复杂、更具交互性的 Web 应用程序，利用控制器和视图的力量来打造引人入胜的用户体验。

## 处理用户输入和表单提交

Web 应用程序依赖交互而蓬勃发展。它们使用户能够提供输入、提交数据和触发操作，从而使体验更加动态和引人入胜。在 ASP.NET Core 3 中，处理用户输入和表单提交已无缝集成到 MVC 框架中，使你能够捕获和处理来自各种来源的数据，包括 HTML 表单、查询字符串和路由参数。在本节中，我们将探讨有效管理用户输入、确保数据验证以及维护 Web 应用程序安全性和完整性的技术和最佳实践。

## HTML 表单：用户输入的入口

HTML 表单为用户与 Web 应用程序交互提供了主要机制。它们允许用户通过各种输入元素（如文本字段、复选框、单选按钮和提交按钮）输入数据、进行选择和触发操作。

让我们在 Razor 视图中创建一个简单的表单：

```
Razor CSHTML

@model MyViewModel

<form asp-controller="Home" asp-action="Submit" method="post">
<div>
<label asp-for="Name"></label>
<input asp-for="Name" />
<span asp-validation-for="Name"></span>
</div>
<div>
<label asp-for="Email"></label>
<input asp-for="Email" />
<span asp-validation-for="Email"></span>
</div>
<button type="submit">Submit</button>
</form>
```

此表单捕获用户的姓名和电子邮件地址，并使用 HTTP POST 请求将数据提交到 HomeController 中的 Submit 操作方法。asp-* 标签辅助程序简化了将表单元素绑定到模型属性和生成验证消息的过程。

## 模型绑定：连接表单到控制器

模型绑定是将传入请求中的数据映射到控制器操作方法中的参数或属性的过程。ASP.NET Core 3 提供了强大的模型绑定功能，可自动从表单字段、查询字符串和路由参数中提取数据，并填充控制器中的相应对象。

让我们看看如何在 HomeController 中处理表单提交：

```
C#
public IActionResult Submit(MyViewModel model)
{
if (ModelState.IsValid)
{
// Process the submitted data
// ...
return RedirectToAction("Success");
}
return View(model); // Redisplay the form with validation errors
}
```

Submit 操作方法接收一个 MyViewModel 对象，该对象会自动使用表单字段中的数据填充。ModelState.IsValid 属性检查提交的数据是否符合模型中定义的任何验证规则。如果数据有效，你可以继续处理它；否则，可以重新显示带有验证错误的表单。

## 数据验证：确保数据完整性

数据验证对于维护应用程序的完整性和安全性至关重要。它涉及检查用户输入，以确保其符合预期的格式、范围或其他约束。ASP.NET Core 3 提供了内置的数据验证支持，使用模型属性上的数据注释特性。

让我们向 MyViewModel 类添加一些验证特性：

```
C#
public class MyViewModel
{
[Required]
public string Name { get; set; }
[Required]
[EmailAddress]
public string Email { get; set; }
}
```

Required 特性确保 Name 和 Email 字段不为空，而 EmailAddress 特性验证电子邮件地址的格式。

## 安全注意事项

处理用户输入时，必须将安全性放在首位，以保护应用程序免受潜在漏洞（例如跨站点脚本 (XSS) 和 SQL 注入攻击）的影响。在处理或存储用户输入之前，始终对其进行清理和验证。

在本节中，我们探讨了在 ASP.NET Core 3 中处理用户输入和表单提交的技术和最佳实践。我们学习了如何创建 HTML 表单、利用模型绑定将表单连接到控制器，以及实施数据验证以确保数据完整性。我们还涉及了安全注意事项，强调了清理和验证用户输入的重要性。掌握这些知识后，你现在已具备构建交互式 Web 应用程序的能力，能够有效地捕获和处理用户数据，同时保持系统的安全性和可靠性。

## 显示数据库中的数据

在 Web 应用程序领域，数据是推动动态和个性化体验的生命线。从数据库中检索信息并以有意义且视觉吸引人的方式呈现给用户，是 Web 开发的基石。在本节中，我们将探讨将数据库交互无缝集成到 ASP.NET Core 3 应用程序中的技术和最佳实践，使你能够清晰高效地从数据存储向用户显示数据。

## Entity Framework Core：你的数据访问网关

如前几章所探讨的，Entity Framework Core (EF Core) 是应用程序与底层数据库之间的桥梁。它提供了一个强大且直观的对象关系映射 (ORM) 框架，允许你将数据作为对象和类来处理，从而抽象掉原始 SQL 查询的复杂性。

## 使用 EF Core 检索数据

让我们说明如何在 ASP.NET Core 3 控制器中使用 EF Core 从数据库检索数据：

```
C#
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore; // Import EF Core namespace
using MyFirstWebApplication.Data; // Import your DbContext class

namespace MyFirstWebApplication.Controllers
{
    public class ProductsController : Controller
    {
        private readonly ApplicationDbContext _context; // Inject the DbContext

        public ProductsController(ApplicationDbContext context)
        {
            _context = context;
        }

        public IActionResult Index()
        {
            var products = _context.Products.ToList(); // Retrieve all products
            return View(products); // Pass the products to the view
        }
    }
}
```

在此示例中，我们使用依赖注入将 ApplicationDbContext 注入到 ProductsController 中。然后，Index 操作方法使用 _context.Products.ToList() 从数据库中检索所有产品，并将它们传递给视图进行呈现。

从数据库检索数据后，你可以在视图中使用 Razor 语法动态将其呈现给用户。让我们创建一个视图来显示产品列表：

```
Razor CSHTML
@model IEnumerable<Product>
<h2>Products</h2>
<ul>
@foreach (var product in Model)
{
<li>@product.Name - $@product.Price</li>
}
</ul>
```

此视图遍历 Model（控制器传递的产品集合），并在列表项中呈现每个产品的名称和价格。

## 筛选和排序数据

EF Core 和 LINQ 在将数据传递给视图之前，提供了强大的筛选和排序功能。让我们修改 Index 操作方法，以仅检索价格大于 $50 的产品，并按名称升序排序：

```
C#
public IActionResult Index()
{
    var products = _context.Products
        .Where(p => p.Price > 50)
        .OrderBy(p => p.Name)
        .ToList();

    return View(products);
}
```

## 分页和数据分页

处理大型数据集时，实现分页或数据分页以分块显示数据至关重要，这可以提高性能和用户体验。EF Core 提供了使用 Skip() 和 Take() 方法的内置分页支持。

## 数据安全和隐私

显示数据库中的数据时，必须考虑安全和隐私影响。避免暴露敏感信息，例如密码或个人身份信息 (PII)，并实施适当的访问控制，以根据用户角色或权限限制数据可见性。

在本节中，我们探讨了在 ASP.NET Core 3 应用程序中显示数据库数据的技术和最佳实践。我们利用 Entity Framework Core 的强大功能检索数据，使用 Razor 语法在视图中动态呈现数据，并实施了筛选、排序和分页以增强用户体验。我们还涉及了数据安全和隐私的重要性，强调了保护敏感信息的必要性。掌握这些知识后，你现在已具备构建数据驱动型 Web 应用程序的能力，能够实现无缝交互。
