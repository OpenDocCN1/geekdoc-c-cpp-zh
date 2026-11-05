
## 10) 视图状态设置

可以使用术语“可自定义”来定制视图状态。可以将视图状态定制为在多个级别存储值，例如：

- 1) 在应用程序级别设置视图状态（当应用程序中的页面不允许使用视图状态时，可以在 web.config 文件中禁用或启用它。）
- 2) 在页面级别设置视图状态（如果特定页面不允许使用视图状态，则可以在 @ Page 指令中禁用或启用它，该指令是 aspx 页面的第一行。）
- 3) 在控件级别设置视图状态（当特定控件不允许使用视图状态时，可以在控件级别禁用它或启用它。）

## 2) 隐藏字段

1) ASP.NET 提供了一个名为“Hidden Field”的服务器控件。它可用于在页面级别存储值，这类似于视图状态。隐藏字段的值会连同其他控件的值一起在 HTTP 表单集合中发送。

## 2) 优点

使用简单，并且隐藏字段将值存储在页面本身中，因此不使用服务器资源。

## 3) 缺点

- 1) 当使用过多隐藏字段来存储数据时，隐藏字段会使页面变得沉重。
- 2) 隐藏字段不能用于存储敏感数据，因为所保存的值未经过哈希处理或未加密。

## 4) 存储和检索隐藏值

## 步骤 1：为隐藏字段设置值

```
/* (txtUsername.Text) value is assigned to the Hidden Field's Value property. */
protected void btnok_Click(Object sender, EventArgs e)
{
hiddenval.Value = txtUsername.Text;
}
```

## 步骤 2：从隐藏字段检索值

/* 从隐藏字段中检索值并将其分配给标签。隐藏字段的“Value”属性默认返回字符串。如果需要其他数据类型值，则需要进行显式转换。 */

```
protected void Page_Load(object sender, EventArgs e)
{
if(! String.IsNullOrEmpty(hdfValue.Value))
{
    lblLogin.Text = hiddenval.Value;
}
}
```

/* 隐藏字段值存储在页面本身中。当用户被重定向到其他页面时，该值会丢失。 */

```
<tr>
<td>
<span id="lblname"></span>
<input type="hidden" name="hdfValue" id="hdfValue" value="RaviW"/>
</td>
</tr>
```

/* 这里将“RaviW”作为来自文本框的值传递，并分配给隐藏字段 */

## 3) 查询字符串

- 1) 查询字符串追加到页面 URL 的末尾，用于保存附加信息。它是一种用于跨页面发送数据的简单技术。
- 2) 它以键-值对的形式存储信息。使用“?”符号将键和值追加到页面 URL。

## 3) 使用查询字符串传递值的方法

```
protected void btnOk_Click(Object sender, EventArgs e)
{
Response.Redirect(String.Format("Default.aspx?Username={0}",txtLogin.Text.Trim()));
}
/* here code sends the Login to another page and use that value on that page.*/
/* reading Query String value */
protected void Page_Load(object sender, EventArgs e)
{
if(!Page.IsPostBack)
{
    string Login = this.Request.QueryString["Login"];
    lblLogin.Text =Login;
}
}
```

/*查询字符串值使用 Request 对象读取。可以在查询字符串中发送多个参数及其各自的值。对于多个参数，各个参数使用“&”分隔符分隔。*/

### 4) Cookie

- 1. Cookie 是 ASP.Net 支持的另一种最佳状态管理方式，使用它来存储信息。它是一个存储在客户端计算机上的文本文件。
- 2. 当用户向服务器发送请求时，服务器创建 Cookie 并附加一个标头，然后将其随响应一起发送回用户。浏览器接受该 Cookie 并将其存储在客户端计算机上的特定位置。Gmail、Facebook、Yahoo 等流行且数据量大的网站都使用 Cookie。
- 3. 有两种在 Cookie 中分配/存储值的方法。

### 1. 使用 Request 对象

```
    protected void btnOk_Click(Object sender, EventArgs e)
    {
        this.Response.Cookies["Login"].Value = txtLoginname.Text.Trim();
    }

    /*The Cookies property of the HTTPResponse Object and the HTTPRequest Object can be
    used to assign values to the Cookies Collection and get values back from the Collection.
    Multiple values can be stored in a cookie.*/
```

### 2. 使用 HTTPCookies 对象

```
    protected void btnOk_Click(Object sender, EventArgs e)
    {
    HttpCookie logCookie = new HttpCookie("Login", txtLogin.Text.Trim());
    logCookie["Lid"] = "78";
    logCookie.Expires = DateTime.Now.AddHours(3);
    Response.Cookies.Add(logCookie);
    }

    /* HTTPCookie class is used to send cookie with cookie expiration time set for that cookie.
    Response.Cookies.Add(logCookie) adds cookie to the Cookies Collection. */
```

### 4) Cookie 的优点

Cookie 使用起来非常方便，并且由于存储在客户端计算机上，因此不使用服务器资源。

### 5) Cookie 的缺点

- 1. 用户可能会使用浏览器设置禁用 Cookie。
- 2) 由于 Cookie 位于客户端计算机上，黑客有机会入侵 Cookie 中的数据，因此 Cookie 完全不是保存敏感数据的好选择。

## 5) **控件状态**

- 1) 控件状态在 ASP.NET 2.0 中引入，它解决了视图状态的一些缺点。
- 2) 控件状态可用于在回发之间存储敏感信息。
- 3) 控件状态是一个状态容器，控件在其中维护其核心行为功能，而视图状态仅包含用于维护控件内容（UI）的状态。
- 4) 控件状态与视图状态共享相同的内存数据结构。
- 5) 如果控件的视图状态被禁用，控件状态仍然可以传播。例如，ASP.NET 2.0 中的新控件 Grid View 有效利用控件状态来维护其核心行为在回发之间所需的状态。

## 21.15.3.2 服务器端状态管理

- 1) 它是 ASP.NET 在服务器计算机上存储用户特定信息或应用程序状态的一种方式。它完全利用服务器资源（服务器内存）来存储信息，这与将数据保存在客户端计算机上的客户端状态管理技术形成对比。
- 2) 应用程序、会话、缓存、数据库可用于服务器端状态管理。
- 3) 在服务器端进行状态管理时，必须注意节省服务器资源。对于并发用户数量众多的高流量网站，使用会话对象进行状态管理可能会给服务器造成负载，导致性能下降。
- 4) 服务器端状态管理使用以下技术
  - 1) 应用程序状态
  - 2) 会话状态

## 1. **应用程序状态**

- 1) 它将信息作为字典集合以键-值对的形式存储在特定 URL 中。该值可在应用程序/网站的各个页面中访问。

## 2) 应用程序状态数据通过以下所述事件进行维护。

- 1. Application_Start，表示应用程序启动。
- 2. Application_End，确定应用程序结束。
- 3. Application_Error，指出应用程序中存在的错误。
- 4. Session_Start，指定会话开始。
- 5. Session_End，指定会话结束。

## 3) HttpApplication 类

1) 它用于提供应用程序状态信息。应用程序特定的值可以保存在应用程序状态中，并由服务器管理。

2) 该状态是全局存储，可通过应用程序中的页面访问。

## HttpApplication 状态的属性

- 1. Count，给出 HttpApplication 类中的对象数
- 2. AllKeys，是访问键的集合。
- 3. StaticObjects，访问 <object> 标签中存在的对象
- 4. Item[Int32]，通过索引检索的单个 HttpApplicationState 对象。
- 5. Contents，是 HttpApplicationState 对象的引用。

## HttpApplication 状态的方法

- 1. Clear，从集合中移除所有对象
- 2. Add，向集合中添加新对象
- 3. GetType，访问当前实例的 Type
- 4. Remove，从集合中移除命名对象
- 5. Set，更新对象的值
- 6. Lock，访问变量以管理同步
- 7. GetHashCode，访问默认哈希函数

## 4) 应用程序状态的优点

- 1. 应用程序状态可通过所有网页访问，因此可以使用单个副本存储信息
- 2. 它对用户来说很容易，并提供一致的框架类。
