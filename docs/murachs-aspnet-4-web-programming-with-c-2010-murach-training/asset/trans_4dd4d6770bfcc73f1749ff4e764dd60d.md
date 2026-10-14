

# HttpServerUtility 类的 Transfer 方法

| 方法 | 说明 |
| :--- | :--- |
| **Transfer** (URL) | 终止当前页面的执行，并将控制权转移到指定 URL 所对应的页面。 |

# HttpResponse 类的 Redirect 和 RedirectPermanent 方法

| 方法 | 说明 |
| :--- | :--- |
| **Redirect** (URL) | 将客户端重定向到指定 URL，并终止当前页面的执行。 |
| **RedirectPermanent** (URL) | 永久重定向到指定 URL，并终止当前页面的执行。 |

# 将控制权转移到另一个页面的代码

```
Server.Transfer ("Cart.aspx");
```

# 将客户端重定向到另一个页面的代码

```
Response.Redirect("Cart.aspx");
```

# 将客户端永久重定向到另一个页面的代码

```
Response.RedirectPermanent ("Customer/Products.aspx");
```

# 说明

- * Transfer 方法是 HttpServerUtility 类的成员，该类包含用于处理 Web 请求的辅助方法。若要引用此类，请使用页面的 Server 属性。
- * Redirect 和 RedirectPermanent 方法是 HttpResponse 类的成员，该类包含有关响应的信息。若要引用此类，请使用页面的 Response 属性。
- * 这三种方法都会使浏览器显示 URL 所指定的页面。有关 URL 编码的更多信息，请参阅图 3-9。
- * 使用 Transfer 方法时，当前页面会被终止，并在其位置处理一个新页面。此处理在服务器上进行，因此效率很高。但是，浏览器不会更新以反映新页面的地址。
- * 使用 Redirect 方法时，服务器会向浏览器发送一条称为 **HTTP 重定向消息**的特殊消息。浏览器收到此消息后，会向服务器发送 HTTP 请求以请求新页面。然后，服务器处理新页面并将其发送回浏览器。由于这需要与浏览器进行往返，因此其效率低于 Transfer 方法。
- * 通常情况下，应使用 Redirect 方法来显示另一个网页。只有在应用程序性能至关重要时，才应使用 Transfer 方法。
- * 如果更改了页面的名称或位置，可以使用 RedirectPermanent 方法为该页面指定新的 URL。然后，搜索引擎会存储该 URL，并在收到对旧 URL 的请求时使用它来显示该页面。

![](img/c024ccf88e28c30c07dd410d4342288f_110_0.png)

# 如何使用跨页回发

转至另一个网页的第四种方式是使用*跨页回发*，如图 3-8 所述。要使用跨页回发，请在按钮控件的 **PostBackUrl** 属性中指定另一个页面的 **URL**。然后，当用户单击按钮时，包含 **PostBackUrl** 属性所指定 URL 的 HTTP POST 消息会被发送回服务器。结果是，加载并执行该 URL 对应的页面，而不是最初显示的页面。

例如，Order 页面上的 Go to Cart 按钮使用跨页回发转到 Cart 页面。因此，该按钮的 **PostBackUrl** 属性被设置为 Cart.aspx，如图所示。然后，当用户单击 Go to Cart 按钮时，ASP.NET 会加载并执行 Cart.aspx 页面，而不是 Order.aspx 页面。

请注意，此控件的 **PostBackUrl** 属性中的 URL 以波浪符 (~/) 运算符开头。当你从属性窗口设置 **PostBackUrl** 属性时，会自动添加该运算符；你将在下一个主题中了解更多相关信息。

如果用户在采用跨页回发的页面的一个或多个控件中输入数据，则可以使用 **PreviousPage** 属性检索用户输入的数据。如图中的代码示例所示，你应先检查并确保 **PreviousPage** 属性引用有效对象。如果该属性未引用有效对象，则意味着该页面不是因跨页回发而加载的，或者请求来自另一个网站。无论哪种情况，都没有可用的上一页面。

如果 **PreviousPage** 属性引用有效对象，则可以使用 **FindControl** 方法查找上一页面上的控件。然后，可以将其强制转换为文本框（如果该控件是文本框）。最后，可以使用 **Text** 属性检索文本框包含的数据。

由于检索用户输入的数据需要额外的编程，因此跨页回发最适合在无需处理用户输入的情况下使用。例如，由于用户单击 Go to Cart 按钮时无需处理任何数据，因此我使用了跨页回发，而不是 **Response.Redirect** 或 **Server.Transfer**。但是，对于 Order 页面上的 Add to Cart 按钮，我使用了 **Response.Redirect**，以便轻松检索所选产品和用户输入的数量。

# Button 控件的 **PostBackUrl** 属性

| 属性 | 说明 |
| :------- | :---------- |
| PostBackUrl | 指定用户单击按钮时应请求的页面的 URL。 |

# 与跨页回发一起使用的 Page 类成员

| 属性 | 说明 |
| :------- | :---------- |
| PreviousPage | 返回表示上一页面的 Page 对象。 |

| 方法 | 说明 |
| :----- | :---------- |
| FindControl(id) | 返回具有指定 id 的 Control 对象。如果该控件是文本框，则可以将 Control 对象强制转换为 TextBox，然后使用 Text 属性访问用户输入的数据。 |

# 用于将页面回发到另一个页面的按钮的 aspx 代码

```html
<asp:Button ID="btnCart" runat="server" Text="Go to Cart"
   CausesValidation="False" PostBackUrl="~/Cart.aspx" />
```

# 从上一页面检索数据的代码

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

# 说明

- *跨页回发*允许你使用按钮的 PostBackUrl 属性来指定用户单击按钮时应请求的页面。
- 当回发到另一个页面时，可以通过 PreviousPage 属性访问上一页面。然后，可以使用 FindControl 方法检索用户输入的数据。
- 通常情况下，跨页回发比 Server.Transfer 和 Response.Redirect 方法更高效。但是，跨页回发使得从原始页面检索数据更加困难。
- 如果不需要从原始页面检索数据，则跨页回发显然比 Server.Transfer 和 Response.Redirect 方法更好。

在第 1 章中，你已经了解了 URL 的基本组成部分。你在那一章中看到的 URL 都是*绝对 URL*。绝对 URL 包含网站的域名。在 Transfer 或 Redirect 方法中编写绝对 URL 时，可以显示另一个网站上的页面。例如，图 3-9 中的前两个语句显示域名为 www.murach.com 的网站上的页面。第一条语句显示网站根目录中名为 Default.aspx 的页面。第二条语句显示网站 Books 目录中名为 Search.aspx 的页面。

若要显示同一网站内的页面，可以使用*相对 URL*。这种 URL 指定页面相对于当前页面所在目录的位置。图中第三条和第四条语句对此进行了说明。第三条语句显示与当前页面存储在同一目录中的页面。第四条语句显示当前页面所在目录的 Login 子目录中的页面。

接下来的两条语句演示如何使用相对 URL 从当前目录向上导航目录结构。若要向上导航一级目录，请编写两个句点后跟一个斜杠，如第五条语句所示。若要向上导航两级目录，请编写两个句点和一个斜杠，然后再编写两个句点和一个斜杠，如第六条语句所示。若要继续向上导航更多级目录，请为每一级目录编写两个句点和一个斜杠。

若要导航到主机的根目录，请编写一个斜杠，如第七条语句所示。你也可以在斜杠后面编写该目录的路径，以导航到根目录内的某个目录，如第八条语句所示。

除了在 Transfer、Redirect 和 RedirectPermanent 方法中编写 URL 之外，还可以为某些服务器控件的属性编写 URL。图中最后两个示例对此进行了说明。倒数第二个示例演示如何设置按钮控件的 PostBackUrl 属性。最后一个示例演示如何设置图像控件的 ImageUrl 属性。

请注意，这两个 URL 都以波浪符 (~) 运算符开头。该运算符使 URL 基于网站的根目录。例如，第一个 URL 中的 Cart.aspx 文件直接位于根目录中，第二个 URL 中的 banner.jpg 文件位于根目录的 Images 子目录中。

尽管在这些示例中也可以使用相对 URL，但当你将页面或文件从一个文件夹移动到另一个文件夹时，使用波浪符运算符的 URL 更容易维护。这是因为，维护相对于网站根目录的 URL 比维护相对于另一个页面的 URL 更容易。因此，我建议你在为服务器控件的属性编写 URL 时，始终使用波浪符运算符。

# 如何编写绝对 URL 和相对 URL

