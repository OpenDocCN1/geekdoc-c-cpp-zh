
最后的路径参数指定了 cookie 应用于服务器的哪个部分。值 `'/'` 意味着从文档向上任何地方都可以访问该 cookie。然而，你可以通过限制范围，例如将路径更改为子文件夹如 `'/chat'` 来限制范围。你可以直接省略相同的范围，就好像它的值为 `'/'` 一样。如果你这样做，你还可以缩短读取和删除 cookie 时使用的代码，如下所示：

```
value = ProcessCookie('read', 'password')
ProcessCookie('erase', 'password')
```

记住，路径（或无路径）对于对 cookie 的所有访问必须是相同的，否则你将无法读取和写入它。你可能不需要使用 `domain` 和 `secure` 参数，这就是为什么我在前面的示例中省略了它们，但如果你需要，它们是可用的。

这里有一个示例，可以让你测试 cookie 是否正在被可靠地传输：

```javascript
<script>
window.onload = function() {
  value = ProcessCookie('read', 'username')
  if (value) alert('返回的 username 值为: ' + value + ')')
  else alert('username 没有值。')

  alert('点击 OK 存储值为 'fred' 的 cookie 'username'')
  ProcessCookie('save', 'username', 'fred', 60 * 24)

  alert('点击 OK 获取 cookie')
  value = ProcessCookie('read', 'username')

  if (confirm('返回的 :username 值为: ' + value + '\n\n现在，点击 [确定] 删除 cookie，然后' +
  '刷新页面以查看 cookie 是否已删除。\n或' +
  '点击 [取消] 不执行操作，然后刷新页面以' +
  '查看它是否保留了原来的值。\n')) {
    ProcessCookie('erase', 'username')
  }
}</script>
```

这段 JavaScript 获取 cookie `'username'`，如果它有值，就会显示出来。

当你第一次加载此页面时，它不存在，所以你会看到弹出一个警告框并告知你。

接下来，将创建 cookie 并赋值为 `'fred'`，在操作前后都有警告消息，以便你可以看到每个操作的结果。

最后，会弹出一个确认对话框，你可以在其中点击 OK 按钮删除 cookie，或者点击取消 按钮保持原样。我建议你点击 OK 然后刷新页面，查看 cookie 是否已被删除。然后再次按照警告提示操作，但这次点击取消按钮并刷新页面，查看 cookie 的值已被保留。

## 326 JavaScript 插件：100 种解决方案

### 插件

```javascript
function ProcessCookie(action, value, seconds, path,
domain, secure)
{
  if (action == 'save') {
    var date = new Date();
    date.setTime(date.getTime() + seconds * 1000);
    var expires = seconds ? '; expires=' + date.toUTCString() : '';
    path = path ? '; path=' + path : '';
    domain = domain ? '; domain=' + domain : '';
    secure = secure ? '; secure=' + secure : '';
    document.cookie = name + '=' + escape(value) + expires + path + domain + secure;
  } else if (action == 'read') {
    if (!document.cookie) return false;
    else {
      var start = document.cookie.indexOf(name + '=');
      if (start == -1) {
        start += name.length + 1;
        var end = document.cookie.indexOf(' start;', start);
        end = (end == -1) ? document.cookie.length : end;
        return unescape(document.cookie.substring(start, end));
      }
    }
  } else if (action == 'erase') {
    ProcessCookie('save', name, '', -60);
  }
}
```

## 85 CreateAjax()

`Ajax` 是 2.0 极大提升用户交互的动力。它代表异步 JavaScript 和 XML，但这实际上是服务器后台调用的缩写。使用此插件，你可以轻松地从服务器请求信息而用户无需感知。

图 11-2 显示了一个从服务器获取并插入到 `div` 中的简单 HTML 文件。

### 变量、数组和函数

| | 本地 Ajax 对象 |
| :--- | :--- |
| `readyState` | 包含状态的属性 |
| `status` | 包含状态的属性 |
| `responseText` | 包含 Ajax 调用返回文本的属性 |
| `XMLHttpRequest` | 非微软浏览器创建 Ajax 对象的函数 |
| `ActiveXObject()` | 微软浏览器创建 Ajax 对象的函数 |

### 工作原理

由于不同的浏览器需要以不同的方式创建 Ajax 对象，插件使用成对的 `try() ... catch()` 语句按顺序创建每个方法，直到某种方法有效或尝试了所有方法并返回 false，如下：

```javascript
try {
  var ajax = new XMLHttpRequest()
}
catch(el) {
  try {
    var ajax = new ActiveXObject("XMLHTTP")
  }
  catch(el) {
    return false;
  }
}
```

## 328 插件版 JavaScript: 100 个解决方案

```javascript
{
  ajax = new ActiveX("Msxml2.XMLHTTP")
  catch(e2) {
    try {
      ajax = new ActiveX("Microsoft.XMLHttpRequest")
    } catch(e3) {
      ajax = false
    }
  }
}
```

第一个 `try()` 适用于除 Internet Explorer 6 或低版本以外的所有浏览器，第二个适用于 Internet Explorer 6，第三个适用于 Internet Explorer 5。因此，测试大致按照流行浏览器的使用顺序进行。

假设其中一个 `try()` 函数成功，`ajax` 就是一个新的 Ajax 对象；否则，它包含该值。如果它不是一个对象，插件将返回 `false`；否则，代码将在 `ajax` 的 `onreadystatechange` 事件上附加一个内联匿名函数，如下：

```javascript
if (ajax) ajax.onreadystatechange = {
  if (this.readyState == 4 &&
      this.status == 200 &&
      this.responseText != null)
    callback.call(this.responseText)
}
```

这个子函数每当 `ajax` 的 `readyState` 属性变化时就会调用一次，并检查其值是否为 4、`status` 属性是否为 200 以及 `responseText` 属性是否为空。如果满足了所有这些条件，意味着 Ajax 请求成功，因此调用 `callback` 参数中的函数，并传递 `this.responseText` 返回的数据。

实际调用并不由此插件执行。它只是捕获事件并用 Ajax 返回的值填充它。Ajax 调用本身在接下来两个插件 `GetAjaxRequest()` 和 `PostAjaxRequest()` 中完成。

### 如何使用

通常，你不会使用此函数，除非你调用 `GetAjaxRequest()` 或 `PostAjaxRequest()` 来处理你的 Ajax 调用，因为它们会为你调用它；在下面的代码中，我们将一些数据加载到 `div` 中：

```html
<div id='a'></div>

<script>
window.onload = function()
```

## 第 11 章：Cookies、Ajax 与安全 329

```javascript
{
  url = 'ajaxxtest.htm'
  GetAjaxRequest('a', todiv, url)
}
function todiv() {
  Html('a', this)
}
</script>
```

函数 `todiv()` 被传递给插件（注意函数省略了括号，否则只会传递 div 返回的值），并在返回的数据准备就绪后由插件进行回调。在那个时刻，它将使用 `this` 关键字检索数据，并使用 `Html()` 插件将其赋值给 div 的 `innerHTML` 属性。

你需要知道，Ajax 是一个被严格控制的过程，以防止黑客从其他服务器注入恶意代码。因此，只能访问与包含 Ajax 的同一服务器上的文件或程序。例如，如果你想将 Google 首页副本抓取到你网站的 `div` 中，这是是不可能的，Ajax 调用将失败。

因此，如果你在另一个服务器上测试前面的示例，它将无法工作，除非你把 `ajaxxtest.htm` 文件也复制过去。不过，你可以通过从插件版 JavaScript 网站调用以下 URL 来验证它的有效性：

http://pluginjavascript.com/plug-ins/example85.htm

### 插件

```javascript
function CreateAjaxObject(id, callback)
{
  try
    var ajax = new XMLHttpRequest()
    catch(el) {
      try
        ajax = new ActiveX("Msxml2.XMLHTTP")
      catch(e2) {
        try
          ajax = new ActiveX("Microsoft.XMLHTTP")
        catch(e3) {
          ajax = false
        }
      }
    }
  }
}
```

## 330 插件版 JavaScript: 100 个强大的解决方案

```javascript
if (ajax) ajax.onreadystatechange = function() {
  if (this.readyState == 4 &&
      this.status == 200 &&
      this.responseText != null) {
    callback.call(this.responseText);
  }
}
return ajax;
```

## 86 GetAjaxRequest()

此插件使用之前的 `CreateAjaxObject()` 将 Wikipedia 首页加载到 `div` 中。当然，Ajax 的用途远比抓取网页要多，例如在注册网站注册时检查用户名是否被占用，或者更新新闻动态、读者评论或聊天等。为了简单起见，我决定抓取一个网页，以便你可以快速验证这些插件是否正常工作，如图 11-3 所示。

### 关于插件

此插件在后台从网站获取数据。它需要以下内容：

- 一个对象或对象 ID——这不能是数组
- `callback` 在获取数据后将返回的数据传递给它的函数
- `url` 用于通信的 URL
- `args` 传递给 URL 的任何参数

图 11-3

Wikipedia 首页已插入到 `div` 中。

![](img/95e4c43b430487125c342550cc090977_347_0.png)

## 第 11 章：Cookies、Ajax 与安全 331

### 变量、数组与函数

| `nocache` | 赋值的局部变量 |
| :--- | :--- |
| `ajax` | 赋值的局部变量 |
| `CreateAjaxObject()` | 插件返回 |
| `open()` | `ajax` 的方法 |
| `send()` | `ajax` 的方法 |
| `Math.random()` | 返回的函数 |

### 工作原理

此插件使用之前的 `CreateAjaxObject()` 将 Wikipedia 首页加载到 `div` 中。当然，Ajax 的用途远比抓取网页要多，例如在注册网站注册时检查用户名是否被占用，或者更新新闻动态、读者评论或聊天等。为了简单起见，我决定抓取一个网页，以便你可以快速验证这些插件是否正常工作，如图 11-3 所示。（等待，文本重复了）安克雷奇机场的天气是从 weather.gov 的 RSS 馈中提取的。这里以原始形式显示，但你可以轻松编写一些 JavaScript 来使用你需要的数据并按照你的要求进行格式化。

实际上：

```javascript
ajax.open('GET', url + '?' + args + nocache, true)
```

最后，变量 `true` 表示成功：

```javascript
ajax.send(null)
return true
```

### 如何使用

通常，你不会使用此函数，除非你调用 `GetAjaxRequest()` 或 `PostAjaxRequest()` 来处理你的 Ajax 调用，因为它们会为你调用它；在下面的代码中，我们将一些数据加载到 `div` 中：

```html
<div id='a'></div>

<script>
window.onload = function()
{
{
  url = 'ajaxxtest.htm'
  GetAjaxRequest('a', todiv, url)
}
function todiv() {
  Html('a', this)
}
</script>
```

# 第 11 章：Cookies、Ajax 与安全 333

图 11-4
使用此插件，你可以将 RSS 馈提取数据提取并填充到代码标签中。

![](img/95e4c43b430487125c342550cc090977_350_0.png)

### 关于插件

此插件在后台从网站获取数据。它返回以下参数：

- *id* 一个对象或对象 ID——这不能是一个数组
- *callback* 在检索数据后将返回的数据传递给它的函数
- *url* 用于通信的 URL
- *args* 要传递给 URL 的任何参数

### 变量、数组和函数

| | |
|---|---|
| `content` | 包含用于 URL 编码表单的类型类型的局部变量 |
| `ajax` | 赋值为 Ajax 对象的局部变量 |
| `CreateAjaxObject()` | 返回新 Ajax 对象的插件 |
| `open()` | `ajax` 用于开启请求的方法 |
| `setRequestHeader()` | `ajax` 用于设置各种头部的方法 |
| `send()` | `ajax` 用于发送请求的方法 |
| `Math.random()` | 返回随机数的函数 |

### 工作原理

此插件从 `AjaxRequest()` 开始。它首先将请求中数据的 content type 设置为 URL 编码格式。它通过调用 `CreateAjaxObject()` 返回 Ajax 对象，如果结果不是 true，则返回值 false，因为在没有这些的情况下无法继续：

```
var content = 'application/x-www-form-encoded'

var ajax = new CreateAjaxObject(id, callback)

if (ajax) return false
```

# 334 插件 JavaScript：100 种强大的解决方案

如果对象创建成功，它将继续开启请求，在 POST 中传递 'POST' 类型，在 URL 中传递 URL，并传递值 true 以进行异步请求：

```
ajax.open('POST', url, true)
```

接下来，将发送内容类型和连接头部：

```
ajax.setRequestHeader('Content-type', contenttype)

ajax.setRequestHeader('Content-length', args.length)

ajax.setRequestHeader('Connection', 'close')
```

最后，发送请求并返回值 true 以表示成功：

```
ajax.send(args)

return true
```

### 如何使用

你调用插件的方式与 `GetAjaxRequest()` 完全相同——只是插件执行 Ajax 时使用的过程是 POST，而不是 GET 请求。因此，请求目标也需要响应 POST 请求，如下例所示所示，该示例获取了阿拉斯加安克雷奇（Anchorage）机场的详情：

```
<div id=''></div>
```

```
<script>

window.onload = function() {

  url = 'ajaxpost.php'
