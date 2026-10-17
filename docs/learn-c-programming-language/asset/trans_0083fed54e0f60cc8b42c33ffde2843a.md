

![](img/7976f323fd1a5c8774f95fbf029a106f_294_0.png)

## HTTP 协议

### Web 服务器配置

在进行 CGI 编程之前，请确保你的 Web 服务器支持 CGI 并且已配置为处理 CGI 程序。所有由 HTTP 服务器执行的 CGI 程序都保存在一个预先配置好的目录中。该目录称为 CGI 目录，按惯例命名为 /var/www/cgi-bin。按惯例 CGI 文件的扩展名为 .cgi，尽管它们是 C++ 可执行文件。

默认情况下，Apache Web 服务器配置为在 /var/www/cgi-bin 中运行 CGI 程序。如果你想指定其他目录来运行你的 CGI 脚本，可以修改 httpd.conf 文件中的以下部分：

```apache
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options ExecCGI
    Order allow,deny
    Allow from all
</Directory>
```

```apache
<Directory "/var/www/cgi-bin">
Options All

</Directory>
```

这里，我假设你已经成功启动并运行了 Web 服务器，并且能够运行其他 CGI 程序，如 Perl 或 Shell 等。

### 第一个 CGI 程序

考虑以下 C++ 程序内容：

```cpp
#include <iostream>

using namespace std;

int main ()
{
    cout << "Content-type:text/html\r\n\r\n";
    cout << "<html>\n";
    cout << "<head>\n";
    cout << "<title>Hello World - First CGI Program</title>\n";
    cout << "</head>\n";
    cout << "<body>\n";
    cout << "<h2>Hello World! This is my first CGI program</h2>\n";
    cout << "</body>\n";
    cout << "</html>\n";

    return 0;
}
```

编译以上代码并将可执行文件命名为 cplusplus.cgi。该文件保存在 /var/www/cgi-bin 目录中，其内容如下。在运行你的 CGI 程序之前，请确保使用 **chmod 755 cplusplus.cgi** UNIX 命令更改文件模式以使其可执行。现在如果点击 cplusplus.cgi，则会产生以下输出：

My First CGI program

上面的 C++ 程序是一个简单的程序，它将输出写入 STDOUT 文件，即屏幕。有一个重要且额外的功能可用，即第一行打印 **Content-type:text/html\r\n\r\n**。该行发送回浏览器并指定在浏览器屏幕上显示的内容类型。

现在你应该已经理解了 CGI 的基本概念，并且可以使用 Python 编写许多复杂的 CGI 程序。C++ CGI 程序可以与任何其他外部系统，如 RDBMS，以交换信息。

### HTTP 头部

行 **Content-type:text/html\r\n\r\n** 是 HTTP 头部的一部分，发送到浏览器以理解内容。所有 HTTP 头部都将具有以下形式：

```
HTTP Field Name: Field Content

For Example
Content-type: text/html\r\n\r\n
```

以下是你在 CGI 编程中会经常使用的其他重要 HTTP 头部。

| 头部 | 描述 |
|---|---|
| Content-type: | 定义返回文件的格式的 MIME 字符串。示例为 Content-type:text/html。 |
| Expires: Date | 信息失效的日期。浏览器应使用此信息来决定何时需要刷新页面。有效日期字符串的格式应为 01 Jan 1998 12:00:00 GMT。 |
| Location: URL | 应返回的 URL 而非请求的 URL。你可以使用此字段将请求重定向到任何文件。 |
| Last-modified: Date | 资源最后修改的日期。 |
| Content-length: N | 返回数据的长度，以字节为单位。浏览器使用此值来报告文件的估计下载时间。 |
| Set-Cookie: String | 设置通过 *string* 传递的 cookie。 |

### CGI 环境变量

所有 CGI 程序都将访问以下环境变量。这些变量在编写任何 CGI 程序时发挥重要作用。

| 变量名 | 描述 |
|---|---|
| CONTENT_TYPE | 内容的数据类型，当客户端向服务器发送附加内容时使用。例如文件上传等。 |
| CONTENT_LENGTH | 查询信息的长度，仅对 POST 请求可用。 |
| HTTP_COOKIE | 以键值对形式返回设置的 cookie。 |
| HTTP_USER_AGENT | User-Agent 请求头字段包含发起请求的客户端信息。它是 Web 浏览器的名称。 |
| PATH_INFO | CGI 脚本的路径。 |
| QUERY_STRING | 使用 GET 方法请求发送的 URL 编码信息。 |
| REMOTE_ADDR | 发出请求的远程主机的 IP 地址。这对于日志记录或身份验证目的很有用。 |
| REMOTE_HOST | 发出请求的完全限定主机名。如果此信息不可用，则可以使用 REMOTE_ADDR 获取 IP 地址。 |
| REQUEST_METHOD | 用于发出请求的 method。最常见的 method 是 GET 和 POST。 |
| SCRIPT_FILENAME | CGI 脚本的完整路径。 |
| SCRIPT_NAME | CGI 脚本的名称。 |
| SERVER_NAME | 服务器的主机名或 IP 地址。 |
| SERVER_SOFTWARE | 服务器正在运行的软件的名称和版本。 |

```cpp
if ( value != 0 ){
   cout << value;
}else{
   cout << "Environment variable does not exist.";
}
cout << "</td></tr>\n";
}
cout << "</table>\n";
cout << "</body>\n";
cout << "</html>\n";

return 0;
}
```

输出如下：

| 环境变量 | 值 |
|---|---|
| COMSPEC | Environment variable does not exist. |
| DOCUMENT_ROOT | /var/www/tutorialspoint |
| GATEWAY_INTERFACE | CGI/1.1 |
| HTTP_ACCEPT | text/html, application/xhtml+xml, */* |
| HTTP_ACCEPT_ENCODING | gzip, deflate |
| HTTP_ACCEPT_LANGUAGE | en-US |
| HTTP_CONNECTION | Keep-Alive |
| HTTP_HOST | www.tutorialspoint.com |
| HTTP_USER_AGENT | Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; rv:11.0) like Gecko |
| PATH | /sbin:/usr/sbin:/bin:/usr/bin |
| QUERY_STRING |  |
| REMOTE_ADDR | 183.82.104.71 |
| REMOTE_PORT | 50902 |
| REQUEST_METHOD | GET |
| REQUEST_URI | /cgi-bin/cpp_env.cgi |
| SCRIPT_FILENAME | /var/www/cgi-bin/cpp_env.cgi |
| SCRIPT_NAME | /cgi-bin/cpp_env.cgi |
| SERVER_ADDR | 66.135.33.172 |
| SERVER_ADMIN | webmaster@tutorialspoint.com |
| SERVER_NAME | www.tutorialspoint.com |
| SERVER_PORT | 80 |
| SERVER_PROTOCOL | HTTP/1.1 |
| SERVER_SIGNATURE |  |
| SERVER_SOFTWARE | Apache |
| < |  |

### C++ CGI 库

对于实际示例，你的 CGI 程序需要执行许多操作。有为 C++ 程序编写的 CGI 库，你可以从 ftp://ftp.gnu.org/gnu/cgicc/ 下载并按照步骤安装该库：

```bash
$tar xzf cgicc-X.X.X.tar.gz

$cd cgicc-X.X.X/

$./configure --prefix=/usr

$make

$make install
```

你可以在‘C++ CGI Lib Documentation’查看相关文档。

### GET 和 POST 方法

你一定遇到过许多需要将信息从浏览器传递到 Web 服务器并最终传递到你的 CGI 程序的情况。浏览器最频繁使用两种方法将此信息传递给 Web 服务器。这些方法为 GET 方法和 POST 方法。

#### 使用 GET 方法传递信息

GET 方法将编码的用户信息附加到页面请求中。页面和编码信息由 ‘?’ 字符分隔，如下所示：

```text
http://www.test.com/cgi-bin/cpp.cgi?key1=value1&key2=value2
```

GET 方法是将信息从浏览器传递到 Web 服务器的默认方法，并且会产生一个长字符串出现在你的浏览器位置框中。切勿使用 GET 方法传递密码或其他敏感信息到服务器。GET 方法有大小限制，你可以在请求字符串中传递最多 1024 个字符。

使用 GET 方法时，信息通过 QUERY_STRING http 头部传递，并且可在你的 CGI 程序中通过 QUERY_STRING 环境变量访问。

你可以通过简单地将键值对与任何 URL 拼接在一起传递信息，也可以使用 HTML <FORM> 标签使用 GET 方法传递信息。

#### 简单 URL 示例：Get 方法

这里有一个简单的 URL，它将使用 GET 方法向 hello_get.py 程序传递两个值。

`/cgi-bin/cpp_get.cgi?first_name=ZARA&last_name=ALI`

下面是一个生成 **cpp_get.cgi** CGI 程序以处理 Web 浏览器输入的程序。我们将使用 C++ CGI 库，这使得访问传递的信息变得非常容易：

```cpp
#include <iostream>

#include <vector>

#include <string>

#include <stdio.h>

#include <stdlib.h>

#include <cgicc/CgiDefs.h>

#include <cgicc/Cgicc.h>

#include <cgicc/HTTPHTMLHeader.h>

#include <cgicc/HTMLClasses.h>

using namespace std;
using namespace cgicc;

int main ()
{
    Cgicc formData;

    cout << "Content-type:text/html\r\n\r\n";
    cout << "<html>\n";
    cout << "<head>\n";
    cout << "<title>Using GET and POST Methods</title>\n";
    cout << "</head>\n";
    cout << "<body>\n";
```

