

```csharp
{
var context = TempData["context"] as AcmeLibraryDataEntities;
var book = TempData["book"] as Book;
if (context != null && book != null) {
    UpdateModel(book, collection.ToValueProvider());
    context.SaveChanges();
    context.Dispose();
}
return RedirectToAction("Index");
}
catch {
    return View();
}
```

The UpdateModel method has several over-loads. The one used in the example updates the book variable (representing the model) from the controller's value provider. The FormCollection instance passed to the method can be converted to a value provider with the ToValueProvider method. All the mechanic work is done by this simple method — like parsing the string of properties, and converting them to the appropriate types (such as handling the DateTime value of the Published property).

`UpdateModel` 方法有多个重载。示例中使用的版本是从控制器的值提供程序更新代表模型的 `book` 变量。传递给方法的 `FormCollection` 实例可以通过 `ToValueProvider` 方法转换为值提供程序。所有的机械工作都由这个简单的方法完成——例如解析属性字符串并将其转换为适当类型（例如处理 `Published` 属性的 `DateTime` 值）。

With binding, you can go even further. Let's see the original implementation of the Create actions in the controller:

```csharp
public ActionResult Create() {
    var context = new AcmeLibraryDataEntities();
    var book = new Book {
        Author = "*Author*",
        Title = "*Title*",
        ISBN = "*ISBN*"
    };
    context.AddToBooks(book);
    TempData["context"] = context;
    TempData["book"] = book;
    return View(book);
}
```

```csharp
[HttpPost]
public ActionResult Create(FormCollection collection) {
    return Edit(-1, collection);
}
```

第一个 `Create` 方法实例化了 `AcmeLibraryDataEntities`，使得 `Create` 方法可以简单地调用 `Edit` 操作。在显示视图时，实际上不需要这个上下文，因为它只会在第二个 `Create` 方法中起积极作用。

Let's change the implementation of these methods:

```csharp
public ActionResult Create()
{
    var book = new Book
    {
        Author = "Author",
        Title = "Title",
        ISBN = "ISBN"
    }
    return View(book);
}

[HttpPost]
public ActionResult Create(Book newBook)
{
    try
    {
        using (var context = new AcmeLibraryDataEntities())
        {
            context.AddToBooks(newBook);
            context.SaveChanges();
        }
        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```

现在，第一个 `Create` 方法创建一个 `Book` 实例只是为了设置几个默认值。看第二个方法的签名。它已经被更改，现在它接受一个 `Book` 实例。既然知道 `Create` 方法是通过 HTTP POST 请求调用的，而且 `Book` 是一个 HTTP 完全未知的 .NET 类型，那么 HTTP 请求和路由是如何处理该方法调用并提供 `Book` 实例的呢？

答案再次在于模型绑定（model binding）。传入的数据会被解析并用于填充方法操作的参数。通过这种解决方案，`Create` 操作看起来更自然了，并且不再需要通过 `TempData` 传递实体上下文。

使用模型绑定功能，你可以更改整个 `BookController` 类的操作，如列表 18-15 所示。

# 列表 18-15：更新 BookController 类

```csharp
using System.Linq;
using System.Web.Mvc;
using AcmeLibrary.Models;

namespace AcmeLibrary.Controllers
{

public class BookController : Controller
{
    public ActionResult Index()
    {
        var context = new AcmeLibraryDataEntities();
        var books = context.Books;
        return View(books);
    }

    public ActionResult Details(int id)
    {
        var context = new AcmeLibraryDataEntities();
        var book = context.Books.First(b => b.Id == id);
        return View(book);
    }

    public ActionResult Create()
    {
        var book = new Book
        {
            Author = "Author",
            Title = "Title",
            ISBN = "ISBN"
        };
        return View(book);
    }

[HttpPost]
    public ActionResult Create(Book newbook)
    {
        try
        {
            using (var context = new AcmeLibraryDataEntities())
            {
                context.AddToBooks(newbook);
                context.SaveChanges();
            }
            return RedirectToToAction("Index");
        }
        catch
        {
            return View(newbook);
        }
    }

    public ActionResult Edit(int id)
    {
        using (var context = new AcmeLibraryDataEntities())
        {
            var book = context.Books.First(b => b.Id == id);
            context.Detach(book);
        }
        return View(book);
    }
}

# 列表 18-15（续）

```csharp
[HttpPost]
public ActionResult Edit(Book editedBook)
{
    try
    {
        using (var context = new AcmeLibraryDataEntities())
        {
            context.Books.Attach(editedBook);
            context.Books.ApplyOriginalValues(new Book { Id = editedBook.Id });
            context.SaveChanges();
        }
        return RedirectToAction("Index");
    }
    catch
    {
        return View(editedBook);
    }
}

public ActionResult Delete(int id)
{
    return Edit(id);
}

[HttpPost]
public ActionResult Delete(Book bookToDelete)
{
    try
    {
        using (var context = new AcmeLibraryDataEntities())
        {
            context.Books.Attach(bookToDelete);
            context.Books.DeleteObject(bookToDelete);
            context.SaveChanges();
        }
        return RedirectToAction("Index");
    }
    catch
    {
        return View(bookToDelete);
    }
}
```

# 验证

AcmeLibrary 应用中存在一个严重问题——验证（validation）。当你创建一个新书并在点击 Create 按钮时留标题或 ISBN 信息为空时，你会在无效字段的右侧看到验证消息。然而，当你正在编辑书籍时，发生了一些事情。如果你设置了一个无效的字段值并保存书籍，无效字段的值将恢复到其原始值，且没有任何通知。尝试设置一个超过 13 个字符的 ISBN 码，你将得到一个异常。

是时候处理验证了。在 MVC 中，模型根据其元数据进行验证。模型（例如 `Book`）具有隐式元数据，例如验证过程中使用的属性的类型和可空性。例如，`Book` 类的 `Published` 属性是 `DateTime`。因此，你无法从代表属性的文本框输入任何类型的字符串。

隐式元数据很少足以提供验证。该库有一个名为 `System.DataAnnotations` 的命名空间，包含了你可以使用的特性（attributes）。例如，你可以在属性上使用数据注解，如列表 18-16 所示。

# 验证属性

18-16：应用于 Book 类的数据注解

```csharp
public class Book
{
    public int Id { get; set; }

    [Required(ErrorMessage = "Please provide author name")]
    public string Author { get; set; }

    [Required(ErrorMessage = "Please provide a title")]
    public string Title { get; set; }

    [RegularExpression("[0-9]{13}$",
    ErrorMessage = "This must be 13 digits")]
    public string ISBN { get; set; }

    public DateTime Published { get; set; }

    public string Publisher { get; set; }
}
```

表格 18-1 总结了 `System.ComponentModel.DataAnnotations` 命名空间提供的验证属性。

# 表格 18-1：验证属性

| 特性 | 说明 |
| --- | --- |
| RequiredAttribute | 此特性指定当表单上的字段进行验证时，该字段必须包含值。如果属性为空、包含空字符串或仅包含空白字符，将抛出验证异常。对于字符串，通过将 `AllowEmptyStrings` 设置为 `true`，你可以告诉特性空值是有效的。默认情况下为 `false`。 |
| StringLengthAttribute | 此特性用于验证字符串的长度。你可以指定 `MinimumLength` 和 `MaximumLength` 值。该特性的错误消息支持本地化。它的默认值为“字段 (0) 最大长度为 (1)”。第一个占位符通常是字段名称；第二个是字段的最大长度。最小长度规则也相同。 |
| RangeAttribute | 此特性用于验证数值是否在范围内。值本身不需要是数值，但必须通过 `Converter` 转换为数值。如果满足这些条件，该特性将在验证期间执行自动类型转换。对于类型转换，你可以在 `OperandType` 中给出值的类型。 |
| RegularExpressionAttribute | 此特性用于将属性值与正则表达式进行匹配。它可以包含格式化的电话号码验证，例如，但由于缺乏正则表达式，可能性是的。 |
| DataTypeAttribute | 此特性不是真正的验证特性，但它派自 `ValidationAttribute`。此特性用于指定给定属性内部持有的数据类型（例如当属性的 .NET 类型为 `string` 时）。 |

