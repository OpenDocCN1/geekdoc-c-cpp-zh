
To make sure that the correct page is displayed when you run an application, you should set the start page for the application. To do that, just right-click on the form in the Solution Explorer and select the `Set As Start Page` command from the shortcut menu. Note that this only sets the start page that Visual Studio uses when you run an application. It doesn't set the page IIS displays by default when you run the application from a browser outside of Visual Studio. To do that, you have to use IIS. See appendix B (Windows 7 and Windows Vista) or appendix C (Windows XP) for more information.

#### Solution Explorer 窗口中正在重命名的 Web 表单文件

![A web form file being renamed in the Solution Explorer window](img/c024ccf88e28c30c07dd410d4342288f_108_0.png)

### 重命名 Web 表单的两种方法

- Right-click the form in the Solution Explorer, and then select the `Rename` command from the shortcut menu. Then, change the name directly in the Solution Explorer window.

- Click on the form in the Solution Explorer to select it. Then, click on it again and change the name directly in the Solution Explorer window.

### How to rename the class that contains the C# code for a web form

- Display the code for the form in the Code Editor window. Then, change the name that's used for the form in the class declaration at the beginning of the file.

- Use the `Rename` command in the smart tag menu that becomes available to change the class name in the `Inherits` attribute of the `Page` directive. Alternatively, display the `aspx` code for the form and then change the `Inherits` attribute manually.

### How to change the starting web form for a web site

- Right-click on the web form that you want to use as the starting form in the Solution Explorer. Then, choose `Set As Start Page` from the shortcut menu.

### Note

- In most cases, you'll give a web form an appropriate name when you add it to the project. If you start a web site from the ASP.NET Web Site template, though, you may want to change the name of the web form that's added by default so it's more descriptive.

Figure 3-6 How to rename a web form and change the starting web form

## How to redirect or transfer to another page

When you develop an application with two or more pages, you'll need to know how to display one page from another page. When the user clicks the Add to Cart button on the Order page of the Shopping Cart application, for example, the Cart page should be displayed. Similarly, when the user clicks the Continue Shopping button on the Cart page, the Order page should be displayed. Three ways to do that are presented in Figure 3-7.

When you use the `Transfer` method of the `HttpServerUtility` class, ASP.NET immediately terminates the execution of the current page. Then, it loads and executes the page specified in the `Transfer` method and returns it to the browser. The drawback to using this method is that when the new page is sent to the browser, the browser has no way of knowing that the application returned a different page. As a result, the URL for the original page is still displayed in the browser's address box. This can be confusing to the user and prevents the user from bookmarking the page.

The `Redirect` method of the `HttpResponse` class works somewhat differently. When this method is executed, it sends a special message called an *HTTP redirect message* back to the browser. This message causes the browser to send a new HTTP request to the server to request the new page. Then, the server processes the page and sends it back to the browser.

Note that because of the way the `Redirect` method works, it requires an extra round trip to the browser. If this extra round trip will cause a performance problem, you may want to use the `Transfer` method instead. For most applications, however, the user friendliness of the `Redirect` method outweighs the small performance gain you get when you use the `Transfer` method.

Unlike the `Transfer` and `Redirect` methods, the `RedirectPermanent` method, which is new to ASP.NET 4, is typically used when a page is physically moved or renamed within a web site. For example, suppose you create a web site that includes a page named `Products.aspx` that's stored in the project folder. Later, suppose you decide to create a subfolder named `Customer`, and you move the Products page to this folder. Then, you can use the `RedirectPermanent` method as shown in the third example in this figure to redirect to the page. The main advantage of using this method is that search engines will store the new URL. That way, if the page is requested at the old location, it can be displayed from its new location.

### HttpServerUtility 类的 Transfer 方法

| 方法 | 说明 |
| :--- | :--- |
| `Transfer(URL)` | 终止当前页面的执行，并将控制权转移到指定 URL 所对应的页面。 |

### HttpResponse 类的 Redirect 和 RedirectPermanent 方法

| 方法 | 说明 |
| :--- | :--- |
| `Redirect(URL)` | 将客户端重定向到指定 URL，并终止当前页面的执行。 |
| `RedirectPermanent(URL)` | 永久重定向到指定 URL，并终止当前页面的执行。 |

### 将控制权转移到另一个页面的代码

```csharp
Server.Transfer ("Cart.aspx");
```

### 将客户端重定向到另一个页面的代码

```csharp
Response.Redirect("Cart.aspx");
```

### 将客户端永久重定向到另一个页面的代码

```csharp
Response.RedirectPermanent ("Customer/Products.aspx");
```

### 说明

- `Transfer` 方法是 `HttpServerUtility` 类的成员，该类包含用于处理 Web 请求的辅助方法。若要引用此类，请使用页面的 `Server` 属性。

- `Redirect` 和 `RedirectPermanent` 方法是 `HttpResponse` 类的成员，该类包含有关响应的信息。若要引用此类，请使用页面的 `Response` 属性。

- 这三种方法都会使浏览器显示 URL 所指定的页面。有关 URL 编码的更多信息，请参阅图 3-9。

- 使用 `Transfer` 方法时，当前页面会被终止，并在其位置处理一个新页面。此处理在服务器上进行，因此效率很高。但是，浏览器不会更新以反映新页面的地址。

- 使用 `Redirect` 方法时，服务器会向浏览器发送一条称为 **HTTP 重定向消息**的特殊消息。浏览器收到此消息后，会向服务器发送 HTTP 请求以请求新页面。然后，服务器处理新页面并将其发送回浏览器。由于这需要与浏览器进行往返，因此其效率低于 `Transfer` 方法。

- 通常情况下，应使用 `Redirect` 方法来显示另一个网页。只有在应用程序性能至关重要时，才应使用 `Transfer` 方法。

- 如果更改了页面的名称或位置，可以使用 `RedirectPermanent` 方法为该页面指定新的 URL。然后，搜索引擎会存储该 URL，并在收到对旧 URL 的请求时使用它来显示该页面。

![](img/c024ccf88e28c30c07dd410d4342288f_110_0.png)

## 如何使用跨页回发

转至另一个网页的第四种方式是使用*跨页回发*，如图 3-8 所述。要使用跨页回发，请在按钮控件的 `PostBackUrl` 属性中指定另一个页面的 **URL**。然后，当用户单击按钮时，包含 `PostBackUrl` 属性所指定 URL 的 HTTP POST 消息会被发送回服务器。结果是，加载并执行该 URL 对应的页面，而不是最初显示的页面。

例如，Order 页面上的 Go to Cart 按钮使用跨页回发转到 Cart 页面。因此，该按钮的 `PostBackUrl` 属性被设置为 `Cart.aspx`，如图所示。然后，当用户单击 Go to Cart 按钮时，ASP.NET 会加载并执行 `Cart.aspx` 页面，而不是 `Order.aspx` 页面。

请注意，此控件的 `PostBackUrl` 属性中的 URL 以波浪符（`~/`）运算符开头。当你从属性窗口设置 `PostBackUrl` 属性时，会自动添加该运算符；你将在下一个主题中了解更多相关信息。

如果用户在采用跨页回发的页面的一个或多个控件中输入数据，则可以使用 `PreviousPage` 属性检索用户输入的数据。如图中的代码示例所示，你应先检查并确保 `PreviousPage` 属性引用有效对象。如果该属性未引用有效对象，则意味着该页面不是因跨页回发而加载的，或者请求来自另一个网站。无论哪种情况，都没有可用的上一页面。

如果 `PreviousPage` 属性引用有效对象，则可以使用 `FindControl` 方法查找上一页面上的控件。然后，可以将其强制转换为文本框（如果该控件是文本框）。最后，可以使用 `Text` 属性检索文本框包含的数据。

由于检索用户输入的数据需要额外的编程，因此跨页回发最适合在无需处理用户输入的情况下使用。例如，由于用户单击 Go to Cart 按钮时无需处理任何数据，因此我使用了跨页回发，而不是 `Response.Redirect` 或 `Server.Transfer`。但是，对于 Order 页面上的 Add to Cart 按钮，我使用了 `Response.Redirect`，以便轻松检索所选产品和用户输入的数量。

### Button 控件的 `PostBackUrl` 属性

| 属性 | 说明 |
| :------- | :---------- |
| `PostBackUrl` | 指定用户单击按钮时应请求的页面的 URL。 |

### 与跨页回发一起使用的 `Page` 类成员

| 属性 | 说明 |
| :------- | :---------- |
| `PreviousPage` | 返回表示上一页面的 `Page` 对象。 |

| 方法 | 说明 |
| :----- | :---------- |
| `FindControl(id)` | 返回具有指定 `id` 的 `Control` 对象。如果该控件是文本框，则可以将 `Control` 对象强制转换为 `TextBox`，然后使用 `Text` 属性访问用户输入的数据。 |

### 用于将页面回发到另一个页面的按钮的 `aspx` 代码

```html
<asp:Button ID="btnCart" runat="server" Text="Go to Cart"
   CausesValidation="False" PostBackUrl="~/Cart.aspx" />
```

### 从上一页面检索数据的代码

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (PreviousPage != null)
    {
        TextBox txtQuantity =
            (TextBox) PreviousPage.FindControl("txtQuantity");
        lblQuantity.Text = txtQuantity.Text;
    }
}
```

### 说明

- *跨页回发*允许你使用按钮的 `PostBackUrl` 属性来指定用户单击按钮时应请求的页面。

- 当回发到另一个页面时，可以通过 `PreviousPage` 属性访问上一页面。然后，可以使用 `FindControl` 方法检索用户输入的数据。

- 通常情况下，跨页回发比 `Server.Transfer` 和 `Response.Redirect` 方法更高效。但是，跨页回发使得从原始页面检索数据更加困难。

- 如果不需要从原始页面检索数据，则跨页回发显然比 `Server.Transfer` 和 `Response.Redirect` 方法更好。
