
```
}
catch (Exception ex)
{
    Response.Write(ex.Message);
}
}
```

这是一个不错的功能。在过去，你需要亲自处理字节本身。双向爬坡，还在雪地里。

要构建一个全面的文件上传功能，你需要更严格一些的编程实践。（比如我的错误处理？）不过这里的想法是，有一个 FileUpload 控件可以让你获得显著的后端控制。

在此顺便看看 HttpFileCollection，它是 System.Web 类，为 FileUpload 控件提供其功能。FileUpload 控件的所有属性，如文件的位、名称等，都在 HttpFileCollection 中。如果你需要比 FileUpload 控件提供的更精细的控制，请查看它。

## 烘焙 Cookie

Cookie 是网站可以在客户端机器上直接保存而无需客户端直接许可的唯一东西。它仍然需要间接许可，因为用户可以禁用 Cookie，但被动地，Cookie 可以在不真正询问用户“可以保存吗？”的情况下保存。

Cookie 对于状态管理很有用。例如，如果你知道客户端购物车的 ID，你可以将该 ID 保存到 Cookie 中，即使客户端离开一周后回来，你仍然可以回到业务层查找信息。

Cookie 存储在键值集合中——实际上是一个字典。如果你知道自己在找什么，可以查询集合获取想要的值；如果不知道，可以遍历集合直到找到它。

Cookie 集合使用 Request 和 Response 对象进行管理——基于我在前面章节“浏览 Web 流”中介绍的 HttpRequest 和 HttpResponse 类。

## 为客户端存储编码

要获取 Cookie，你必须先设置一个 Cookie。在对客户端的响应的一部分中——比如他在登录后——你希望告诉平台将信息保存到 Cookies 集合中。

![](img/80ff26f06fc9ab951e1cd4257b867366_743_0.png)

请记住 Cookie 是纯文本——任何人都可以读取它们。切勿存储可能被所谓的“黑帽”人士利用的东西。我几乎总是创建一个 System.Guid（全局唯一标识符）并用它来跟踪我随后在后端数据存储中持久化信息。

更好的做法是存储有关会话本身的信息，并了解该信息将在一段时间后从数据库中删除。这可以防止拦截 Cookie 的人冒充用户。选项很多，但在设置 Cookie 策略之前，请查看 Microsoft 和其他组织提供的最佳实践。

如果我想将会话信息存储在 Cookie 中并告诉数据库我的客户正在使用该会话，我会生成一个 Guid 并将其保存在两个地方。然后我可以在下一次请求时检索 Cookie，将其与用户集合中可用的 Guid 进行比较，并找到相关用户。

以下是基于会话信息设置 Cookie 的示例：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class Cookies : System.Web.UI.Page
    {
        WebUser currentUser = new WebUser();
        List<WebUser> usersInDatabase = new List<WebUser>();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!Page.IsPostBack)
            {
                //This is a first request, so we need to set the cookie
                Guid sessionGuid = new Guid();
                currentUser.SessionId = sessionGuid;
                //Tell the database about the new user
                usersInDatabase.Add(currentUser);
                //Get the cookies
                Response.Cookies.Add(new HttpCookie("SessionId",
                sessionGuid.ToString()));
            }
        }
        //This class would be in the library somewhere,
        //not actually in this file.
        public class WebUser
        {
            public Guid SessionId { get; set; }
        }
    }
```

## 在服务器上处理 Cookie

现在用户有了 Cookie，下一个请求来了。我需要从集合中获取 Cookie 并搜索我已知的用户库以获取所需的信息。以下代码中的粗体表示添加的代码：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class Cookies : System.Web.UI.Page
    {
        WebUser currentUser = new WebUser();
        List<WebUser> usersInDatabase = new List<WebUser>();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!Page.IsPostBack)
            {
                //This is a first request, so we need to set the cookie
                Guid sessionGuid = new Guid();
                currentUser.SessionId = sessionGuid;
                //Tell the database about the new user
                usersInDatabase.Add(currentUser);
                //Set the cookie
                Response.Cookies.Add(new HttpCookie("SessionId", sessionGuid.ToString()));
            }
            else
            {
                //The is a postback so we need to get the cookie
                string cookieSession = Request.Cookies.Get("SessionId").Value.ToString();
                Guid sessionGuid = new Guid(cookieSession);
                var returningUser = from u in usersInDatabase
                                    where u.SessionId.ToString() == sessionGuid.ToString()
                                    select u;
                foreach (var user in returningUser)
                {
                    //Better only be one
                    currentUser = user;
                }
            }
        }
        //This class would be in the library somewhere,
        //not actually in this file.
        public class WebUser
        {
            public Guid SessionId { get; set; }
        }
    }
}
```

按照以下步骤修改 Web.config 文件以进行跟踪：

- 1. 在项目中为跟踪创建一个新页面。
- 2. 在新 Tracing.aspx 页面的 @page 指令中添加 Trace 语句。
- 3. 在代码隐藏中，向 Page_Load 事件处理程序添加代码以模拟异常并捕获它，然后写入 Trace。
- 4. 按 <F5> 运行应用程序。

我把它命名为 Tracing.aspx。

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Tracing.aspx.cs" Inherits="Chapter_4.Tracing" Trace="true" %>
```

这只是为了看看 Trace 如何工作。Book I 更详细地介绍了异常处理。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class Tracing : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            try
            {
                throw new ApplicationException("This is the fake exception.");
            }
            catch (ApplicationException ex)
            {
                Trace.Warn(ex.Message);
            }
        }
    }
}
```

页面看起来不会像你期望的那样。大量信息以 Response.Write 样式转储到页面上，包括 Trace 消息（请查看图 4-4）。

Figure 4-4:
ASP.NET 跟踪示例。

![](img/80ff26f06fc9ab951e1cd4257b867366_747_0.png)

当然，你不想向用户展示所有这些，但如果应用程序出现问题，你是否希望能够为相关页面打开跟踪？你可以给它一些输入，然后使用跟踪查看服务器处理细节如何响应。
