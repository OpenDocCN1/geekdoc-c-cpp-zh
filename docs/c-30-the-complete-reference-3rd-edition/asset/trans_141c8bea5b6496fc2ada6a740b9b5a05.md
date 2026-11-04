
## 创建通用迭代器

前面的迭代器示例都是非泛型的，但当然也可以创建泛型迭代器。操作起来相当容易：只需返回一个泛型 IEnumerator<T> 或 IEnumerable<T> 类型的对象。下面是一个创建泛型迭代器的示例：

// A simple example of a generic iterator.
using System;
using System.Collections.Generic;

class MyClass<T> {
    T[] array;

    public MyClass(T[] a) {
        array = a;
    }

    // This iterator returns the characters
    // in the chrs array.
    public IEnumerator<T> GetEnumerator() {
        foreach (T obj in array)
            yield return obj;
    }
}

class GenericItrDemo {
    static void Main() {
        int[] nums = { 4, 3, 6, 4, 7, 9 };
        MyClass<int> mc = new MyClass<int>(nums);

        foreach (int x in mc)
            Console.Write(x + " ");

        Console.WriteLine();

        bool[] bVals = { true, true, false, true };
        MyClass<bool> mc2 = new MyClass<bool>(bVals);

        foreach (bool b in mc2)
            Console.Write(b + " ");

        Console.WriteLine();
    }
}
```

输出如下所示：

```
4 3 6 4 7 9
True True False True
```

在此示例中，要迭代的对象数组通过其构造函数传递给 MyClass。数组的类型作为类型参数指定给 MyClass。

GetEnumerator() 方法对类型为 T 的数据进行操作并返回一个 IEnumerable<T> 枚举器。因此，由 MyClass 定义的迭代器可以枚举任何类型的数据。

## 集合初始化器

C# 3.0 包含一个名为集合初始化器的新功能，它使初始化某些集合变得更容易。无需显式调用 Add()，您可以在创建集合时指定一组初始化器。执行此操作时，编译器会使用这些值自动为您调用 Add()。语法与数组初始化类似。下面是一个示例。它创建了一个 List<char>，该列表由字符 C、A、E、B、D 和 F 初始化。

```
List<char> lst = new List<char>() { 'C', 'A', 'E', 'B', 'D', 'F' };
```

执行此语句后，lst.Count 将等于 6，因为有六个初始化器，并且此 foreach 循环

```
foreach(ch in lst)
Console.Write(ch + " ");
```

将显示

C A E B D F

当使用存储键/值对的集合（如 LinkedList<TK, TV>）时，您需要提供初始化器对，如下所示：

```
SortedList<int, string> lst =
    new SortedList<int, string>() { {1, "One"}, {2, "Two" }, {3, "Three"} };
```

编译器将每组值作为参数传递给 Add()。因此，编译器会将第一个初始化器对翻译为对 Add(1, "One") 的调用。由于编译器会自动调用 Add() 将初始化器添加到集合中，因此集合初始化器只能与支持 Add() 的公共实现的集合一起使用。因此，集合初始化器不能与 Stack、Stack<T>、Queue 或 Queue<T> 集合一起使用，因为它们不支持 Add()。您也不能对提供 Add() 作为显式接口实现的集合（如 LinkedList<T>）使用集合初始化器。

*本页特意留空*

System.Net 中定义的类如下所示：

| AuthenticationManager | Authorization |
|---|---|
| Cookie | CookieCollection |
| CookieContainer | CookieException |
| CredentialCache | Dns |
| DnsPermission | DnsPermissionAttribute |
| DownloadDataCompletedEventArgs | DownloadProgressChangedEventArgs |
| DownloadStringCompletedEventArgs | Endpoint |
| EndpointPermission | FileWebRequest |
| FileWebResponse | FtpWebRequest |
| FtpWebResponse | HttpListener |
| HttpListenerBasicIdentity | HttpListenerContext |
| HttpListenerException | HttpListenerPrefixCollection |
| HttpListenerRequest | HttpListenerResponse |
| HttpVersion | HttpWebRequest |
| HttpWebResponse | IPAddress |
| IPEndPoint | IPEndPointCollection |
| IPHostEntry | IrDAEndPoint |
| NetworkCredential | OpenReadCompletedEventArgs |
| OpenWriteCompletedEventArgs | ProtocolViolationException |
| ServicePoint | ServicePointManager |
| SocketAddress | SocketPermission |
| SocketPermissionAttribute | UploadDataCompletedEventArgs |
| UploadFileCompletedEventArgs | UploadProgressChangedEventArgs |
| UploadStringCompletedEventArgs | UploadValuesCompletedEventArgs |
| WebClient | WebException |
| WebHeaderCollection | WebPermission |
| WebPermissionAttribute | WebProxy |
| WebRequest | WebRequestMethods |
| WebRequestMethods.File | WebRequestMethods.Ftp |
| WebRequestMethods.Http | WebResponse |

System.Net 定义了以下接口：

| IAuthenticationModule | ICertificatePolicy | ICredentialPolicy |
|---|---|---|
| ICredentials | ICredentialsByHost | IWebProxy |
| IWebProxyScript | IWebRequestCreate |  |

它定义了这些枚举：

| AuthenticationSchemes | DecompressionMethods | FtpStatusCode |
|---|---|---|
| HttpRequestHeader | HttpResponseHeader | HttpStatusCode |
| NetworkAccess | SecurityProtocolType | TransportType |
| WebExceptionStatus |  |  |

System.Net 还定义了几个委托。

尽管 System.Net 定义了许多成员，但只有少数几个成员即可完成大多数常见的 Internet 编程任务。网络的核心是抽象类 WebRequest 和 WebResponse。这些类被支持特定网络协议的类继承。（协议定义了在网络上传输信息时使用的规则。）例如，支持标准 HTTP 协议的派生类是 HttpWebRequest 和 HttpWebResponse。

尽管 WebRequest 和 WebResponse 易于使用，但对于某些任务，您可以采用基于 WebClient 的更简单的方法。例如，如果您只需要上传或下载文件，那么 WebClient 通常是完成此操作的最佳方式。

## 统一资源标识符

Internet 编程的基础是统一资源标识符（URI）。URI 描述了网络上某个资源的位置。URI 也常被称为 URL，即统一资源定位符的缩写。由于 Microsoft 在描述 System.Net 的成员时使用术语 URI，本书也将如此。您无疑熟悉 URI，因为您每次在 Internet 浏览器中输入地址时都会使用一个 URI。

URI 的一般形式如下：

```
Protocol://ServerID/FilePath?Query
```

Protocol 指定所使用的协议，例如 HTTP。ServerID 标识特定的服务器，例如 mhpprofessional.com 或 HerbSchildt.com。FilePath 指定特定文件的路径。如果未指定 FilePath，则获取指定 ServerID 上的默认页面。最后，Query 指定将发送到服务器的信息。Query 是可选的。在 C# 中，URI 由 Uri 类封装，该类将在本章后面进行介绍。

## Internet 访问基础

System.Net 中包含的类支持 Internet 交互的请求/响应模型。在这种方法中，您的程序（即客户端）请求服务器信息，然后等待响应。例如，在请求时，您的程序可能会向服务器发送某个网站的 URI。您将收到的响应是与该 URI 关联的超文本。这种请求/响应方法既方便又简单易用，因为大多数细节都由系统处理。

以 WebRequest 和 WebResponse 为顶层的类层次结构实现了 Microsoft 所称的可插拔协议。如大多数读者所知，有几种不同类型的网络通信协议。Internet 使用中最常见的是超文本传输协议（HTTP）。另一种是文件传输协议（FTP）。构造 URI 时，URI 的前缀指定协议。例如，http://www.HerbSchildt.com 使用前缀 http，表示超文本传输协议。

如前所述，WebRequest 和 WebResponse 是抽象类，定义了所有协议共有的通用请求/响应操作。从它们派生出实现特定协议的具体类。派生类使用 WebRequest 中定义的静态方法 RegisterPrefix() 将自身注册。当您创建 WebRequest 对象时，如果可用，则 URI 前缀指定的协议将自动使用。这种“可插拔”方法的优点是，无论使用何种类型的协议，大部分代码保持不变。

.NET 运行时自动定义 HTTP、HTTPS、file 和 FTP 协议。因此，如果您指定使用 HTTP 前缀的 URI，您将自动获得支持它的 HTTP 兼容类。如果您指定使用 FTP 前缀的 URI，您将自动获得支持它的 FTP 兼容类。

由于 HTTP 是使用最广泛的协议，本章仅讨论它。（不过，相同的技术适用于所有受支持的协议。）支持 HTTP 的类是 HttpWebRequest 和 HttpWebResponse。这些类继承 WebRequest 和 WebResponse，并添加了若干适用于 HTTP 协议的自身成员。

System.Net 支持同步和异步通信。对于许多 Internet 用途，同步事务是最好的选择，因为它们易于使用。在同步通信中，您的程序发送请求然后等待接收响应。对于某些高性能应用程序，异步通信更好。使用异步方法，您的程序可以在等待信息传输的同时继续处理。然而，异步通信更难实现。此外，并非所有程序都能从异步方法中受益。例如，通常在需要从 Internet 获取信息时，在信息接收之前没有其他事情可做。在这种情况下，异步方法的潜在收益无法实现。由于同步 Internet 访问更易于使用且适用性更广，因此本章仅研究这种类型。

由于 WebRequest 和 WebResponse 是 System.Net 的核心，接下来将对它们进行研究。

## WebRequest

WebRequest 类管理网络请求。它是抽象的，因为它没有实现特定协议。它确实定义了所有请求共有的那些方法和属性。WebRequest 中支持同步通信的方法如表 25-1 所示。WebRequest 中定义的属性如表 25-2 所示。属性的默认值由派生类确定。

WebRequest 未定义公共构造函数。

要向 URL 发送请求，您必须首先创建一个派生自 WebRequest 且实现所需协议的类的对象。这是通过调用 Create() 完成的，Create() 是 WebRequest 中定义的静态方法。Create() 返回一个继承 WebRequest 并实现特定协议的类的对象。
