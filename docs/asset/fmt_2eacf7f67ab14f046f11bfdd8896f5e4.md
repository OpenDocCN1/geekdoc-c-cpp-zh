
使用 `DataRequested` 事件向控制器请求数据。`IDisplayBooksReadView` 如下所示：

```cs
public interface IDisplayBooksReadView
{
    event EventHandler DataRequested;
    List<BookRead> Data { get; set; }
    void Bind();
}
```

IDDisplayBooksReadView.cs

如所示，`BookRead` 对象就是模型。此时，你不需要定义它被包含在这个对象中；你只需要创建它，以便你的测试能够通过编译：

```cs
public class BookRead
{
}
```

BookRead.cs

`DisplayBooksReadController` 是应用程序部分的演示器（Presenter）。演示器负责视图（View）和模型（Model）之间的通信。因此，演示器有一个你正在操作的字段，它最终会被传递给演示器对象的构造函数，还有一个从你确定的任何类型的数据源获取数据的函数。以下是 `DisplayBooksReadController` 的代码：

```cs
public class DisplayBooksReadController
{
    public IDisplayBooksReadView View { get; set; }
    public DisplayBooksReadController(IDisplayBooksReadView view)
    {
    }
    public void GetData(object sender, EventArgs e)
    {
    }
}
```

DisplayBooksReadController.cs

如图 9-5 所示，测试仍然失败，但至少通过了编译。在尝试计算控制器传递给视图的数据项数量时，有两种修复方法。你可以使用模拟框架（mocking framework）并模拟数据，或者你可以直接硬编码对象并完之（这也称为桩存，stubbing）。本示例展示了如何对 `BookRead` 数据进行桩存。在本章的稍后部分，你将处理测试、数据库和模拟对象之间的关系。

## ASP.NET Web Forms | 203

![](img/15cb6759e167a2d15e60bc37de753a62_203_0.png)

图 9-5

完成此任务，你需要实现控制器：

```cs
public class DisplayBooksReadController
{
    public IDisplayBooksReadView View { get; set; }
    public DisplayBooksReadController(IDisplayBooksReadView view)
    {
        View = view;
        View.DataRequested += GetData;
    }
    public void GetData(object sender, EventArgs e)
    {
        View.Data = new List<BookRead>
        {
            new BookRead { ReadId = 1, Name = "@Testing ASP.NET Web Applications", Author = "Jeff McKervey/Ben Hall", ISBN = "978-0470496640", StartDate = new DateTime(2010, 2, 12), Rating = 10, PurchaseLink = "http://www.amazon.com" },
            new BookRead { ReadId = 2, Name = "@Test Driven Development: By Example", Author = "Kent Beck", ISBN = "978-0321146533", StartDate = new DateTime(2010, 2, 12), Rating = 9, PurchaseLink = "http://www.amazon.com" },
            new BookRead { ReadId = 3, Name = "Test2", Author = "Author", ISBN = "22222222", StartDate = new DateTime(2010, 3, 12), Rating = 3, PurchaseLink = "http://www.msu.edu" }
        };
        View.Bind();
    }
}
```

DisplayBooksReadController.cs

通过 `DisplayBooksReadController` 类的构造函数，你将 `View` 属性设置为传递给控制器的视图，然后将 `DataRequested` 事件绑定到 `GetData` 方法。`GetData` 返回三个桩存的 `BookRead` 对象。实现控制器意味着是时候按照如下定义模型了：

```cs
public class BookRead
{
    public int ReadId { get; set; }
    public string Name { get; set; }
    public string Author { get; set; }
    public string ISBN { get; set; }
    public DateTime StartDate { get; set; }
    public DateTime EndDate { get; set; }
    public int Rating { get; set; }
    public string PurchaseLink { get; set; }
}
```

BookRead.cs

Web Forms MVP 项目的第一个测试应该。由于 MVP 模式，你可以将类从 ASP.NET 生命周期中隔离出来，并创建测试来确保该类的功能正常工作。

## 创建更多测试

现在控制器已经完全实现。由于示例是从控制器开始的，因此你还没有任何关于视图的测试。你需要测试视图上的构造函数是否连接了所有事件，这只有唯一一点——`DataRequested` 事件。你可以为视图创建一个模拟对象（Mock object），将其注入控制器，然后验证 `DataRequested` 事件是否已绑定到控制器的 `GetData` 函数。由于你已经实现了该功能，这个测试应该能够通过，而无需添加任何更多代码。

```cs
public class test_and_wiring_the_events_by_the_constructor : Specification
{
    IDisplayBooksReadView _view;
    protected override void Establish_context()
    {
        base.Establish_context();
        _view = MockRepository.GenerateMock<IDisplayBooksReadView>();
        _view.Expect(v => v.DataRequested += null).IgnoreArguments();
    }
    protected override void Because_of()
    {
        new DisplayBooksReadController(_view);
    }
    [Test]
    public void then_the_constructor_should_wire_up_events()
    {
        _view.VerifyAllExpectations();
    }
}
```

`GetData` 函数和 `DataRequested` 事件，控制器调用视图上的 `Bind` 方法。视图内部将数据绑定到 ASPX 页面上的控件。显示最近阅读书籍的“管道”代码现在实现。在向你展示连接这一切的代码之前，我想简要解释一下辅助方法的概念。

## Helpers

辅助方法帮助其他方法执行任务。它们通常是方法之间共享的任务。例如，在 Web 上，将文本截断到特定的字符数并在末尾附加省略号以指示文本已被截断是种常见的方法。这种类型的方法并不特定于阅读视图；它可以用于此应用程序中的任何其他视图，因此你可以创建一个包含 `Truncate` 方法的 `HTMLHelper` 类来帮助你这种方式显示文本。如果我以前没说过，现在我说：TDD 关乎重复。你首先为 `Truncate` 方法创建一个测试：

```cs
public class when_using_the_html_helper_to_truncate_text : Specification
{
    protected string _textToTruncate;
    protected string _expected;
    protected string _actual;
    protected int _numberToTruncate;
    protected override void BecauseOf()
    {
        _actual = HTMLHelper.Truncate(_textToTruncate, _numberToTruncate);
    }
}
public class class__passing_a_string_that_needs_to_be_truncated : when_using_the_html_helper_to_truncate_text
{
    protected override void Establish_context()
    {
        _textToTruncate = "This is my text";
        _expected = "This...";
        _numberToTruncate = 5;
    }
    [Test]
    public void then_the_text_should_be_truncated_with_ellipses()
    {
        _expected.ShouldEqual(_actual);
    }
}
```

接下来，你实现代码使测试通过：

```cs
public static string Truncate(string input, int length)
{
    if (input.Length <= length)
        return input;
}
```

HTMLHelper.cs

然后重构实现以使测试通过：

```cs
public static string Truncate(string input, int length)
{
    if (length == 0)
        return input;
    if (String.IsNullOrEmpty(input))
        return string.Empty;
    if (input.Length <= length)
        return input;
    else
        return input.Substring(0, length) + "...";
}
```

HTMLHelper.cs

## 将所有部分整合

到此时，显示书籍（Books）所需的所有逻辑已经创建。剩下的工作是将这些逻辑连接到 Web 表单（Web Form）。以下代码是 Books Web 应用程序的默认页面。首先要的是，Default 页面需要实现 `IDisplayBooksReadView` 接口，并为 `DataRequested` 添加一个事件。在 `Page_Load` 函数中，你只需创建一个新的控制器并触发 `DataRequested` 事件。

由于 `DataRequested` 事件的触发，`Bind` 函数被调用，数据被绑定到屏幕上。一旦你理解了这个概念，这就变得清晰易读：

```cs
public partial class Default : System.Web.UI.Page, IDisplayBooksReadView
{
    private DisplayBooksReadController Controller;
    public event EventHandler DataRequested;
    public List<BookRead> Data { get; set; }
    protected void Page_Load(object sender, EventArgs e)
    {
        Controller = new DisplayBooksReadController(this);
        DataRequested(sender, e);
    }
    public void Bind()
    {
        rptBooksRead.DataSource = Data;
        rptBooksRead.DataBind();
    }
}
```

作为开发者，你可能没有考虑设计人员在收到你的代码时必须经历什么。与后代码（code-behind）中的所有代码一样，你的目标应该是保持标记（markup）尽可能简洁。下面的示例使用了重复器（repeater）。你可能希望尝试避免使用难以测试且设计人员难以于操作的 datagrids。尽量将 `<%` 标签减少到最少；仅在需要显示字段时实现它们。这些策略允许你创建大多数设计人员或开发者都能轻松进入并理解的标记。

```html
<asp:Repeater Id="RepeaterId" runat="server">
  <ItemTemplate>
    <div class="readBook">
      <div class="bookInfo">
        <h2><%# Wrox.BooksRead.Web.Helpers.HTMLHelper.Truncate(((Wrox.BooksRead.Web.BookRead)Container.DataItem).Name, 25) %></h2>
        <p>Author: <%# ((Wrox.BooksRead.Web.BookRead)Container.DataItem).Author %></p>
        <p>ISBN: <%# ((Wrox.BooksRead.Web.BookRead)Container.DataItem).ISBN %></p>
        <p>Date Finished: <%# ((Wrox.BooksRead.Web.BookRead)Container.DataItem).EndDate.ToString("MM/dd/yyyy") %></p>
      </div>
      <a href="<%# ((Wrox.BooksRead.Web.BookRead)Container.DataItem).PurchaseLink %>" target="_blank">Purchase</a>
    </div>
    <div class="ratingContainer">
      <span class="rating"><%# ((Wrox.BooksRead.Web.BookRead)Container.DataItem).Rating %></span>
    </div>
    <hr style="clear:both;" />
  </ItemTemplate>
</asp:Repeater>
```
