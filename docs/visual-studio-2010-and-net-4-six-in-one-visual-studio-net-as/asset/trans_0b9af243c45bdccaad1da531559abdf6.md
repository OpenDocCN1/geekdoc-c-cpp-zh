

> 提供关于 Entity Framework 4.0（EF 4.0 — AcmeLibraryModel.edmx 文件使用该框架生成代码）的详细概述超出了本章的范围。这里使用的示例足够直观，使得即使你没有 EF 4.0 经验，只要你用过 ADO.NET 或 LINQ to SQL 等 .NET 数据访问技术，就能理解它们。如果你正在使用 EF 4.0，在 MSDN 上搜索“ADO.NET Entity Framework 入学者指南”将可以找到丰富的资源。

## 列出书籍

现在你已经有了一个数据库，并使用 EF 4.0 定义了一个模型。要显示书籍列表，你需要一个控制模型和视图的控制器（controller）。从左到右读取“MVC”中的字母，你可能会认为下一步是创建一个视图，然后你可以开始构建控制器。另一种可行的方法是先创建控制器，这比“先创建视图”的方法方法具有某些优势。

在处理书籍时，你可能希望通过视图（页面）提供诸如向列表添加新书籍或修改现有书籍属性等的功能。在大多数情况下，你希望在显示书籍列表的页面上提供指向这些功能的链接（按钮或其他 UI 元素），这意味着这些页面将共享一个控制器，并包含 Create、Edit、Delete 等操作（actions）。

所以，让我们创建一个负责操作书籍的控制器吧。

## 创建 BookController 类

在解决方案管理器（Solution Explorer）中选择 Controllers。右键点击，并从上下文菜单中选择“添加控制器”（Add Controller）。弹出“添加控制器”对话框，如图 18-14 所示。

在“控制器名称”（Controller Name）文本框中输入 `BookController`，并勾选复选框为控制器添加书籍操作的操作，如 Create、Edit、Delete 和 Details。

如果你留空复选框，控制器将只生成一个 Index 操作。代码列表 18-10 显示了 BookController 类的源代码。

![](img/b5597c749e848b27b0d305153ae16106_814_0.png)

图 18-14：添加控制器对话框

## 列表 18-10：BookController.cs

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using AcmeLibrary.Models;

namespace AcmeLibrary.Controllers
{
    public class BookController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }

        public ActionResult Details(int id)
        {
            return View();
        }

        public ActionResult Create()
        {
            return View();
        }

        [HttpPost]
        public ActionResult Create(FormCollection collection)
        {
            try
            {
                // TODO: Add insert logic here
                return RedirectToAction("Index");
            }
            catch
            {
                return View();
            }
        }

        public ActionResult Edit(int id)
        {
            return View();
        }

        [HttpPost]
        public ActionResult Edit(int id, FormCollection collection)
        {
            try
            {
              // TODO: Add update logic here
              return RedirectToAction("Index");
            } catch {
              return View();
            }
        }

        public ActionResult Delete(int id) {
          return View();
        }

        [HttpPost]
        public ActionResult Delete(int id, FormCollection collection)
        {
          try {
            // TODO: Add delete logic here
            return RedirectToAction("Index");
          } catch {
            return View();
          }
        }
    }
}
```

代码文件 [BookController.cs] 可在 Wromax.com 下载。

> 为了简洁起见和提高可读性，此列表省略了操作头部注释。原始源代码包含每个操作的头部，告知你访问该操作的请求 URL。

注意，Create、Edit 和 Delete 这三个操作都拥有带有 `[HttpPost]` 特性并接受 `FormCollection` 参数的重载方法。`[HttpPost]` 用于限制操作方法，使其方法只处理 POST 请求。`FormCollection` 实例表示表单值提供程序。当用户填写表单（例如，创建新 Book 实例所需的表单）时，它将作为 `FormCollection` 传递给处理它们的操作。

BookController 类只是一个空骨架，尚未将操作与模型或相应的视图集成。

在文件头部的现有 `using` 句中添加以下 `using` 句：

```csharp
using AcmeLibrary.Models;
```

通过将 Index 操作的主体更改为以下代码将操作与模型集成：

```csharp
public ActionResult Index()
{
    var context = new AcmeLibraryDataEntities();
    var books = context.Books;
    return View(books);
}
```

这段代码检索所有书籍并将数据传递给 View 方法，该方法将书籍解释为模型中的集合。

## 创建 Index 视图

尽管 Index 操作访问了模型，但还没有显示书籍列表的视图。与 Visual Studio 2010 集成的 MVC 2 工具创建新视图变得非常简单。

如果已加载 UserController.cs 文件，请点击 Index 方法的主体以放置光标。右键点击代码编辑器，并从上下文菜单中选择“添加视图”（Add View）命令。

> Visual Studio 2010 的 RTM 版本有一个小 Bug。

视图对话框，允许你为新视图指定参数。（注意：第 817-818 页剩余的 OCR 文本已损坏，未包含在内）。

