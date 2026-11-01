

| 属性 | 值 |
|---|---|
| CssClass | ErrorMessage |
| Display | Dynamic |
| ErrorMessage | 输入您的家庭电话或办公电话 |
| Text | * |
| ClientValidationFunction | validatePhoneNumbers |

5. 在设计视图中双击 CustomValidator 控件，让 VS 为 ServerValidate 事件生成事件处理程序。将以下代码添加到处理程序中：

```vbnet
Protected Sub CustomValidator1_ServerValidate(source As Object,
    args As ServerValidateEventArgs) Handles CustomValidator1.ServerValidate
    If Not String.IsNullOrEmpty(PhoneHome.Text) OrElse
        Not String.IsNullOrEmpty(PhoneBusiness.Text) Then
        args.IsValid = True
    Else
        args.IsValid = False
    End If
End Sub
```

```csharp
protected void CustomValidator1_ServerValidate(object source,
    ServerValidateEventArgs args)
{
    if (!string.IsNullOrEmpty(PhoneHome.Text) ||
        !string.IsNullOrEmpty(PhoneBusiness.Text))
    {
        args.IsValid = true;
    }
    else
    {
        args.IsValid = false;
    }
}
```

6. 切换到用户控件的标记视图，在包含控件的表格之前添加以下 JavaScript 代码块：

```javascript
<script type="text/javascript">
function validatePhoneNumbers(source, args)
{
    var phoneHome = document.getElementById('<%= PhoneHome.ClientID %>');
    var phoneBusiness = document.getElementById('<%= PhoneBusiness.ClientID %>');
    if (phoneHome.value != '' || phoneBusiness.value != '')
    {
        args.IsValid = true;
    }
    else
    {
        args.IsValid = false;
    }
}
</script>
```

在 JavaScript 中，通常使用驼峰命名法来编写方法名，即方法名的第一个单词小写，后续单词的首字母大写。

如果你发现 VS 将左花括号（{}）放在行尾而不是单独成行，可以选择主菜单中的“工具 ⇨ 选项”，然后展开“文本编辑器 ⇨ JavaScript ⇨ 格式”路径，并勾选“新行”类别中的两个选项。这纯粹是格式偏好问题；无论左花括号是否单独成行，JavaScript 都能正常运行。请注意，JavaScript 区分大小写，因此请确保完全按照此处所示输入代码。

7. 按 Ctrl+Shift+S 保存所有更改，在浏览器中请求 Contact.aspx 页面，并单击“发送”按钮。同时请注意，ValidationSummary 控件会以列表形式显示表单中输入数据的所有问题。客户端 JavaScript 函数 validatePhoneNumbers 现在确保您在将页面提交回服务器之前至少输入一个电话号码。图 9-8 显示了该页面在 Google Chrome 中的显示效果。

![](img/eadab2ccd79b253c01a3fdff2321202d_374_0.png)

图 9-8

8. 返回 VS，在设计视图中单击 ValidationSummary 控件。在属性网格中，将 ShowMessageBox 更改为 True，将 ShowSummary 更改为 False。（快速提示：您可以轻松选择

在这里，您可以看到控件的服务器端 ClientID 属性如何被转换为对应的客户端 id。这比在最终 HTML 中硬编码文本框的 id 属性要好得多，因为 ASP.NET 运行时可以轻松更改这些 id。在前一章中，您已经了解了这种情况发生的方式和原因。

为了使浏览器中的最终 JavaScript 更简短、更易读，您可以使用前一章中介绍的 ClientIDMode 属性来“固定”电话号码控件的 ID。由于一个页面中不太可能出现两个 ContactForm 用户控件，因此可以安全地假设，如果固定客户端控件 ID，不会出现两个同名的客户端控件。为此，您需要将这两个控件的 ClientIDMode 设置为 Static，如下所示：

```html
<asp:TextBox ID="PhoneHome" runat="server" ClientIDMode="Static" />
<asp:TextBox ID="PhoneBusiness" runat="server" ClientIDMode="Static" />
```

由于控件 ID 现已固定，它们将原样出现在最终 HTML 中：

```javascript
var phoneHome = document.getElementById('PhoneHome');
var phoneBusiness = document.getElementById('PhoneBusiness');
```

最终，客户端 ID 会被传递给文档对象上的 JavaScript 函数 getElementById，以获取对 JavaScript 中相应文本框的引用。在第 11 章中讨论 jQuery 时，我会介绍一种比使用 getElementById 更简单的替代方法。然后代码会检查这两个 TextBox 控件的 value 属性。如果其中一个不是空字符串，验证就成功。但 validatePhoneNumbers 方法如何向验证机制报告验证是否成功呢？当 ASP.NET 验证机制调用 validatePhoneNumbers 方法时，它会传递两个参数：source（指向 HTML 中实际 CustomValidator 的引用）和 args。args 对象公开了一个 IsValid 属性，使您能够确定验证是否成功：

```javascript
if (phoneHome.value != '' || phoneBusiness.value != '')
{
    args.IsValid = true;
}
else
{
    args.IsValid = false;
}
```

使用此代码，如果两个文本框均为空，IsValid 将设置为 false，因此验证不会成功，从而阻止表单提交。如果至少有一个文本框包含值，IsValid 将设置为 true。在此示例中，未使用 source 参数，但您可以用它来突出显示或根据验证控件是否有效来更改验证控件。

在服务器端，CustomValidator 控件会调用服务器端验证方法，该方法执行相同的检查：

### VB.NET

```vbnet
If Not String.IsNullOrEmpty(PhoneHome.Text) OrElse
    Not String.IsNullOrEmpty(PhoneBusiness.Text) Then
    args.IsValid = True
Else
    args.IsValid = False
End If
```

```csharp
if (!string.IsNullOrEmpty(PhoneHome.Text) ||
    !string.IsNullOrEmpty(PhoneBusiness.Text)
)
{
    args.IsValid = true;
}
else
{
    args.IsValid = false;
}
```

通过在客户端和服务器端检查数据，您可以确保系统只接受有效数据。即使浏览器不支持 JavaScript（可能是因为用户故意将其关闭），您的数据仍然会在服务器端进行检查。然而，重要的是要认识到，在处理提交给页面的数据之前，您仍然需要检查页面是否有效。您可以通过检查页面的 IsValid 属性来实现这一点：

```vbnet
If Page.IsValid Then
    ' OK to proceed
End If
```

```csharp
if (Page.IsValid)
{
    // OK to proceed
}
```

当页面或活动 ValidationGroup 中的所有控件都有效时，IsValid 属性返回 True。在服务器端处理数据之前检查 IsValid 属性，可以确保根据验证控件数据是有效的，即使浏览器中关闭了 JavaScript 并且表单在没有客户端检查的情况下被发送到服务器。在本章后面讨论发送电子邮件时，您会再次看到 IsValid 属性的使用。

除了到目前为止您已经看到的验证控件之外，ASP.NET 还提供了另一种验证机制，接下来将对此进行讨论。

## 了解请求验证

按照设计，只要页面上的某个控件包含看起来像 HTML 标签的内容，ASP.NET 页面就会抛出异常。例如，当您在联系表单的注释文本框中输入 <h1>Hello World</h1> 或 <script type="text/javascript">alert('Hello World');</script> 时，您会看到图 9-10 中所示的错误。

如果您将站点托管在外部托管方，则需要使用其提供的 SMTP 服务器。如果您不确定自己的 SMTP 服务器，请联系网络管理员或 ISP。

当您获得 SMTP 服务器的地址后，可以在 Web.config 文件的 <system.net> 元素中对其进行全局配置。当您使用 ISP 的 SMTP 服务器时，配置设置如下所示：

```xml
<system.net>
  <mailSettings>
    <smtp deliveryMethod="Network" from="Your Name &lt;you@example.com &gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
...
</configuration>
```

您必须将 <system.net> 元素添加为 Web.config 文件根元素 <configuration> 的直接子元素。在 <system.net> 中，您需要添加 <mailSettings> 元素，该元素又包含一个 <smtp> 元素。最后，<network> 元素指向您的 SMTP 服务器。

<smtp> 元素接受一个可选的 from 属性，该属性允许您以“姓名 <电子邮件地址>”的格式设置发件人的姓名和电子邮件地址。由于 XML 中的尖括号（< >）具有特殊含义，您需要使用 &lt; 和 &gt; 进行转义。当您以编程方式发送电子邮件时，可以覆盖此 From 地址，您将在下一个 Try It Out 练习中看到。

如果您的 ISP 要求您在发送电子邮件之前进行身份验证，或者希望您使用不同的端口号，您可以将此信息添加到 <network /> 元素中：

```xml
<smtp deliveryMethod="Network" from="Your Name &lt;you@example.com &gt;">
  <network host="smtp.example.com" userName="UserName" password="Password"
    port="587" />
</smtp>
```

端口号因服务器而异。在某些情况下，您可以省略 port 属性，SmtpClient 将使用默认端口号（即 25）。其他常用端口号包括 465 和 587。

某些邮件服务器（如 Gmail 提供的服务器）要求您使用安全套接字层（SSL），这是一种加密发往邮件服务器的数据以提高安全性的技术。在 ASP.NET 4 之前的版本中，您必须在自己的代码中以编程方式启用 SSL。幸运的是，由于 <network /> 元素中包含了 enableSsl 属性，现在不再需要这样做了。要使用 Gmail 服务器或任何其他需要 SSL 的邮件服务器，您可以使用如下所示的 <network /> 元素：

```xml
<network enableSsl="true" host="smtp.gmail.com" password="Password"
  userName="YourAccountName@gmail.com" port="587" />
```

别忘了输入您的密码和用户名——对于 Gmail 来说，用户名就是您的完整 Gmail 电子邮件地址。根据您的设置，您可能需要生成一个应用专用密码，您可以在此处生成：http://bit.ly/N9Wv3S。

