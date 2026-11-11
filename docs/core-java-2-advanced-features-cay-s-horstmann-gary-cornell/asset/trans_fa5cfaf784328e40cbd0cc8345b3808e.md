
## 清单 4.6 *（续）*

```java
/**
 * This program connects to an URL and displays the response header data and the first 10 lines of
 * the requested data.
 *
 * Supply the URL and optional username and password (for HTTP basic authentication) on the
 * command line.
 * @version 1.21 2007-06-26
 * @author Cay Horstmann
 */
public class URLConnectionTest
{
   public static void main(String[] args)
   {
      try
      {
         String urlName;
         if (args.length > 0) urlName = args[0];
         else urlName = "http://hostname.com";

         URL url = new URL(urlName);
         URLConnection connection = url.openConnection();

         // set username, password if specified on command line

         if (args.length > 2)
         {
            String username = args[1];
            String password = args[2];
            String input = username + ":" + password;
            Base64.Encoder encoder = Base64.getEncoder();
            String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
            connection.setRequestProperty("Authorization", "Basic " + encoding);
         }

         connection.connect();

         // print header fields

         Map<String, List<String>> headers = connection.getHeaderFields();
         for (Map.Entry<String, List<String>> entry : headers.entrySet())
         {
            String key = entry.getKey();
            for (String value : entry.getValue())
               System.out.println(key + ": " + value);
         }

         // print convenience functions
         System.out.println("----------");
         System.out.println("getContentType: " + connection.getContentType());
         System.out.println("getContentLength: " + connection.getContentLength());
         System.out.println("getContentEncoding: " + connection.getContentEncoding());
         System.out.println("getDate: " + connection.getDate());
         System.out.println("getExpiration: " + connection.getExpiration());
         System.out.println("getLastModified: " + connection.getLastModified());
         System.out.println("----------");

         String encoding = connection.getContentEncoding();
         if (encoding == null) encoding = "UTF-8";
         try (Scanner in = new Scanner(connection.getInputStream(), encoding))
         {
            // print first ten lines of contents

            for (int n = 1; in.hasNextLine() && n <= 10; n++)
               System.out.println(in.nextLine());
            if (in.hasNextLine()) System.out.println("... ");
         }
         catch (IOException e)
         {
            e.printStackTrace();
         }
      }
   }
}
```

| `java.net.URL` | 1.0 |
|---|---|
| • `InputStream openStream()` | 打开一个输入流，用于读取资源数据。 |
| • `URLConnection openConnection()` | 返回一个 `URLConnection` 对象，该对象管理与资源的连接。 |

| `java.net.URLConnection` | 1.0 |
|---|---|
| • `void setDoInput(boolean doInput)`<br>• `boolean getDoInput()` | 如果 `doInput` 为 true，则用户可以从该 `URLConnection` 接收输入。 |
| • `void setDoOutput(boolean doOutput)`<br>• `boolean getDoOutput()` | 如果 `doOutput` 为 true，则用户可以向该 `URLConnection` 发送输出。 |

## java.net.URLConnection 1.0（续）

- `void setIfModifiedSince(long time)`
- `long getIfModifiedSince()`

`ifModifiedSince` 属性配置此 `URLConnection`，使其仅获取自给定时间以来被修改的数据。该时间以自 1970 年 1 月 1 日格林尼治标准时间午夜以来的秒数表示。

- `void setUseCaches(boolean useCaches)`
- `boolean getUseCaches()`

如果 `useCaches` 为 true，则可以从本地缓存中检索数据。请注意，`URLConnection` 本身并不维护此类缓存；缓存必须由外部程序（如浏览器）提供。

- `void setAllowUserInteraction(boolean allowUserInteraction)`
- `boolean getAllowUserInteraction()`

如果 `allowUserInteraction` 为 true，则可以向用户查询密码。请注意，`URLConnection` 本身没有执行此类查询的功能；查询必须由外部程序（如浏览器或浏览器插件）执行。

- `void setConnectTimeout(int timeout)` 5.0
- `int getConnectTimeout()` 5.0

设置或获取连接超时时间（以毫秒为单位）。如果在建立连接之前超时时间已到，则关联输入流的 `connect` 方法会抛出 `SocketTimeoutException`。

- `void setReadTimeout(int timeout)` 5.0
- `int getReadTimeout()` 5.0

设置或获取读取数据的超时时间（以毫秒为单位）。如果在读操作成功之前超时时间已到，则 `read` 方法会抛出 `SocketTimeoutException`。

- `void setRequestProperty(String key, String value)`

设置一个请求头字段。

- `Map<String,List<String>> getRequestProperties()` 1.4

返回请求属性的映射。同一键的所有值都放在一个列表中。

- `void connect()`

连接到远程资源并获取响应头信息。

- `Map<String,List<String>> getHeaderFields()` 1.4

返回响应头的映射。同一键的所有值都放在一个列表中。

- `String getHeaderFieldKey(int n)`

获取第 n 个响应头字段的键；如果 n ≤ 0 或大于响应头字段数，则返回 null。

- `String getHeaderField(int n)`

获取第 n 个响应头字段的值；如果 n ≤ 0 或大于响应头字段数，则返回 null。

- `int getContentLength()`

获取内容长度（如果可用），否则返回 -1。

- `String getContentType()`

获取内容类型，例如 `text/plain` 或 `image/gif`。

- `String getContentEncoding()`

获取内容编码，例如 `gzip`。这个值通常不常用，因为默认的身份编码不应该用 Content-Encoding 头来指定。

- `long getDate()`
- `long getExpiration()`
- `long getLastModified()`

获取资源的创建日期、过期日期和最后修改日期。这些日期以自 1970 年 1 月 1 日格林尼治标准时间午夜以来的秒数表示。

- `InputStream getInputStream()`
- `OutputStream getOutputStream()`

返回用于从资源读取或向资源写入的流。

- `Object getContent()`

选择合适的 content handler 来读取资源数据并将其转换为对象。除非你安装了自己的 content handler，否则此方法对于读取标准类型（如 `text/plain` 或 `image/gif`）并没有用处。

### 4.4.3 提交表单数据

在上一节中，你了解了如何从 Web 服务器读取数据。现在我们将展示你的程序如何将数据发送回 Web 服务器以及由 Web 服务器调用的程序。

为了将信息从 Web 浏览器发送到 Web 服务器，用户需要填写一个*表单*，如图 4.8 所示。

![](img/7dd923a566750151a3aab0dacd0cdaa5_288_0.png)

图 4.8 一个 HTML 表单

当用户单击“提交”按钮时，文本字段中的文字以及所有复选框、单选按钮和其他输入元素的设置都会被发送回 Web 服务器。Web 服务器调用一个处理用户输入的程序。

许多技术使 Web 服务器能够调用程序。其中最知名的是 Java servlet、JavaServer Faces、Microsoft Active Server Pages (ASP) 和公共网关接口 (CGI) 脚本。

服务器端程序处理表单数据并生成另一个 HTML 页面，Web 服务器将其发送回浏览器。此过程如图 4.9 所示。响应页面可以包含新信息（例如，在信息搜索程序中），也可以只是一个确认信息。然后 Web 浏览器显示响应页面。

![](img/7dd923a566750151a3aab0dacd0cdaa5_289_0.png)

我们不讨论本书中服务器端程序的实现。我们只对编写与现有服务器端程序交互的客户端程序感兴趣。

当表单数据发送到 Web 服务器时，数据是由 servlet、CGI 脚本还是其他服务器端技术解释并不重要。客户端以标准格式将数据发送到 Web 服务器，Web 服务器负责将其传递给生成响应的程序。

通常使用两种命令（称为 GET 和 POST）向 Web 服务器发送信息。

在 GET 命令中，你只需将查询参数附加到 URL 的末尾。URL 的形式为

```
http://host/path?query
```

每个参数的形式为 *name=value*。参数用 & 字符分隔。参数值使用 *URL 编码*方案进行编码，遵循以下规则：

