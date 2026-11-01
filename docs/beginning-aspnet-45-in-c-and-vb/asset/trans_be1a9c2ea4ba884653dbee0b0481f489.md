
2. 在浏览器中查看页面的 HTML，方法是右键单击页面并选择“查看源代码”或“查看页面源代码”。

3. 找到用户名的输入字段，然后查看其正下方的验证器代码。你应该会看到类似这样的内容：

```
<span id="cpMainContent_ContactForm_RequiredFieldValidator1" class="ErrorMessage" style="visibility:hidden;"></span>
```

4. 向下滚动到代码末尾，直到看到负责验证的大段 JavaScript 代码。对于 Name 字段，你会看到类似下面的内容：

```
var cpMainContent_ContactForm_RequiredFieldValidator1 = document.all ?
    document.all["cpMainContent_ContactForm_RequiredFieldValidator1"] :
    document.getElementById("cpMainContent_ContactForm_RequiredFieldValidator1");
cpMainContent_ContactForm_RequiredFieldValidator1.controltovalidate
    = "cpMainContent_ContactForm_Name";
cpMainContent_ContactForm_RequiredFieldValidator1.errormessage
    = "Enter your name";
cpMainContent_ContactForm_RequiredFieldValidator1.evaluationfunction
    = "RequiredFieldValidatorEvaluateIsValid";
cpMainContent_ContactForm_RequiredFieldValidator1.initialvalue = "";
```

对于每个验证控件，你都会看到类似的代码，这些代码都会增大页面的体积。

5. 返回 VS，在“解决方案资源管理器”中右键单击网站，然后选择“添加 ▸ 新建项”。找到“全局应用程序类”项。你不必输入名称，因为 Global.asax 的默认名称是该文件唯一允许的名称。

6. 将以下代码添加到 Global.asax 文件代码模板中已有的 Application_Start 方法中：

```
VB
Sub Application_Start(ByVal sender As Object, ByVal e As EventArgs)
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        New ScriptResourceDefinition With
        {
            .Path = "~/Scripts/jquery-1.7.2.min.js"
        })
End Sub
```

```
C#
void Application_Start(object sender, EventArgs e)
{
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        new ScriptResourceDefinition
        {
            Path = "~/Scripts/jquery-1.7.2.min.js"
        });
}
```

单词 jquery（全小写）的拼写区分大小写，所以请确保完全按照此处所示输入。如果你使用的是较新版本的 jQuery 库，请不要忘记更新版本号。

7. 保存更改并关闭文件。

8. 接下来，打开 Web.config 文件并修改 <appSettings> 元素中的下面这行代码。你在第9章中添加了该行。如果没有这行代码，请将其添加到 <appSettings> 标签之间。无论哪种方式，最终都应该得到如下代码：

```
<appSettings>
...
    <add key="ValidationSettings:UnobtrusiveValidationMode" value="WebForms" />
</appSettings>
```

9. 打开母版页，并更改对 jQuery 库的引用，使其指向你在 Global.asax 文件中创建的 ScriptResourceDefinition，如下所示：

```
<asp:ScriptManager ID="ScriptManager1" runat="server" EnablePageMethods="true">
    <Scripts>
        <asp:ScriptReference Name="jquery" />
    </Scripts>
</asp:ScriptManager>
```

如果不进行此更改，jQuery 会在使用验证控件的页面中被包含两次；一次来自 Global.asax 中的代码，另一次来自 ScriptManager 控件中的引用。通过让 ScriptReference 指向 Global.asax 中定义的 ScriptResourceDefinition，ASP.NET 会识别出它指向同一个 JavaScript 库，并且只包含一次该引用。

10. 保存更改，然后在浏览器中请求 Contact.aspx。单击“发送”按钮，并注意验证仍然有效。打开页面的 HTML，再次找到 name 输入字段。在该字段下方，你应该看到如下验证器代码：

```
<span data-val-controltovalidate="cpMainContent_ContactForm_Name"
      data-val-errormessage="Enter your name"
      id="cpMainContent_ContactForm_RequiredFieldValidator1"
      class="ErrorMessage" data-val="true"
      data-val-evaluationfunction="RequiredFieldValidatorEvaluateIsValid"
      data-val-initialvalue="" style="visibility:hidden;">*</span>
```

11. 向下滚动到代码末尾。请注意，之前看到的所有 JavaScript 现在已经消失。相反，在文件顶部，你现在会找到一个 <script> 元素，它指向一个 JavaScript 文件（即那些以 /ScriptResource.axd 开头的链接之一），其中包含使用 jQuery 库的验证代码。

## 工作原理

通过启用非侵入式 JavaScript 验证，验证控件会生成不同的代码。控件不再发出执行验证的 JavaScript 代码，而是在验证 <span> 上输出 HTML5 data- 属性。HTML5 规范允许你为元素自定义属性，只要以 data- 前缀开头即可。非侵入式验证框架利用了这一特性，为错误消息（在 data-val-error-message 中）以及验证输入控件时需要执行的 JavaScript 函数（在 data-val-evaluationfunction 中）等添加属性。当你单击提交按钮时，验证框架会启动，找到所有需要验证的控件，然后使用 data- 属性来确定需要验证的内容和方式。请注意，除了验证控件以及它们之前生成的 JavaScript 之外，变化不大。你的页面仍然包含相同的输入控件和提交按钮。但验证的执行方式已发生根本性变化，现在使用 jQuery 库以及添加到 HTML 元素上的 data- 属性。

要启用非侵入式验证，你必须在 Web.config 中启用之前禁用的键。该键会指示验证框架切换模式并发出非侵入式 JavaScript 代码。由于验证依赖 jQuery，你还需要向 ScriptManager 注册 jQuery 库。遗憾的是，你不能通过 ScriptManager 控件注册该库；你必须使用以下代码在 Global.asax 中完成：

```
VB
Sub Application_Start(ByVal sender As Object, ByVal e As EventArgs)
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        New ScriptResourceDefinition With
        {
            .Path = "~/scripts/jquery-1.7.2.min.js"
        })
End Sub
```

```
C#
void Application_Start(object sender, EventArgs e)
{
    ScriptManager.ScriptResourceMapping.AddDefinition("jquery",
        new ScriptResourceDefinition
        {
            Path = "~/scripts/jquery-1.7.2.min.js"
        });
}
```

这段代码使用对象初始化器创建 ScriptResourceDefinition 类的新实例，并将其 Path 属性设置为 jQuery 库的路径。然后，通过 AddDefinition 方法将此实例添加到 ScriptManager 的 ScriptResourceMapping 中。最后，通过将母版页中的 ScriptManager 控件指向此 ScriptResourceDefinition，jQuery 会被包含在站点的所有页面中。虽然这看起来有点不寻常，但结果非常直接：一个指向所引用 jQuery 库的链接被添加到页面输出中，供验证框架使用。

一旦你完成此设置，就再也不必为此操心了；你可以像以前一样向页面添加验证控件，jQuery 和 ASP.NET 的验证框架将为你处理所有验证。请注意，此更改完全不会影响服务器端验证；服务器端验证将继续像以前一样运行。

如果到现在你觉得 jQuery 真的很棒，我完全同意。虽然一开始可能有点难以适应 jQuery，但一旦你掌握了它，你会想知道没有它的时候你是怎么过来的。更酷的是，你并不局限于 jQuery 库开箱即用的功能。jQuery 具有可插拔的架构，这意味着你可以为它编写插件来扩展或增强 jQuery 的功能。在撰写本文时，官方 jQuery 插件网站因正在开发新网站而暂时下线。不过，在网上搜索“jQuery plug-ins”应该会找到许多有用的插件，用于各种目的，从图片画廊、验证框架、可视化工具提示、对话框等等。我们也鼓励你

