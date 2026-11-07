
应发送时，人们发现使用名称比使用数字地址要容易得多。

这些协议中的每一个对 Internet 通信的各个方面都至关重要，并且各自有特定的用途和通信规则。理解它们对网络编程至关重要，尤其是在与 Web 服务器、邮件服务器、文件服务器和 DNS 服务器交互时。

## HTTP 与 HTTPS 深入解析

HTTP（HyperText Transfer Protocol，超文本传输协议）是一种应用层协议，主要用于在万维网上传输文档。HTTP 遵循客户端-服务器模型，客户端打开连接并向已知服务器发送消息。然后服务器用自己的消息进行响应，并关闭连接。

HTTP 消息由客户端到服务器的请求和服务器到客户端的响应组成。请求由方法（如 GET 或 POST）、所请求的 URL 以及一系列标头组成。响应由响应代码（如 200 表示成功，404 表示未找到）、消息以及响应自身的一系列标头组成。

HTTPS（HTTP Secure）是 HTTP 的安全版本。它使用 TLS（传输层安全协议），或以前的 SSL（安全套接层），来加密客户端和服务器之间的连接。这意味着两者之间发送的所有数据都完全加密，使黑客难以拦截和理解数据。

## 使用 Boost Beast 发送 HTTP 请求

现在，让我们借助 Boost.Asio 中的 Boost Beast 库，深入探讨如何使用 C++ 发起 HTTP/HTTPS 请求。

下面是一个向 HTTP 服务器发送 HTTP GET 请求的简单程序：

```cpp
#include
#include
#include
#include
#include
#include

namespace http = boost::beast::http;
namespace net = boost::asio;
using tcp = net::ip::tcp;

int main()
{
    try
    {
        auto const host = "example.com";
        auto const port = "80";
        auto const target = "/index.html";
        int version = 11;

        net::io_context ioc;
        tcp::resolver resolver(ioc);
        auto const results = resolver.resolve(host, port);

        tcp::socket socket(ioc);
        net::connect(socket, results.begin(), results.end());

        http::request req{ http::verb::get, target, version };
        req.set(http::field::host, host);
        req.set(http::field::user_agent, BOOST_BEAST_VERSION_STRING);

        http::write(socket, req);

        boost::beast::flat_buffer buffer;
        http::response res;
        http::read(socket, buffer, res);

        std::cout << res << std::endl;

        socket.shutdown(tcp::socket::shutdown_both);
    }
    catch (std::exception const& e)
    {
        std::cerr << "Error: " << e.what() << std::endl;
        return EXIT_FAILURE;
    }

    return EXIT_SUCCESS;
}
```

该程序建立到 example.com 的 80 端口（HTTP 的标准端口）的连接，发送针对 /index.html 的 GET 请求，然后读取并打印响应。

要支持 HTTPS，需要使用 Boost Asio SSL 模块创建 SSL 套接字，这会稍微复杂一些。

### 使用 Boost Asio SSL 发起 HTTPS 请求

由于安全连接需要进行 SSL/TLS 握手，发起 HTTPS 请求比 HTTP 请求稍微复杂一些。不过，Boost Asio 提供了一个方便的 ssl::stream 类，它作为现有流（如 TCP 套接字）的包装器，并为其添加 SSL/TLS 功能。

在进入代码之前，请注意，Boost Asio SSL 模块依赖 OpenSSL 库。你需要在项目中安装 OpenSSL 并链接它。还要确保你的系统具有 OpenSSL 可用于验证证书的证书存储。

下面是一个使用 Boost Asio 和 Boost Beast 发起 HTTPS GET 请求的简化示例：

```cpp
#include

#include

#include

#include

namespace http = boost::beast::http;
namespace net = boost::asio;
namespace ssl = net::ssl;
using tcp = net::ip::tcp;

int main()
{
    try
    {
        auto const host = "example.com";
        auto const port = "443";
        auto const target = "/index.html";
        int version = 11;

        net::io_context ioc;
        ssl::context ctx{ssl::context::tlsv12_client};

        // This holds the root certificate used for verification
        ctx.set_default_verify_paths();

        tcp::resolver resolver{ioc};
        auto const results = resolver.resolve(host, port);

        ssl::stream stream{ioc, ctx};
        net::connect(stream.next_layer(), results.begin(), results.end());
        stream.handshake(ssl::stream_base::client);

        http::request req{http::verb::get, target, version};
        req.set(http::field::host, host);
        req.set(http::field::user_agent, BOOST_BEAST_VERSION_STRING);

        http::write(stream, req);

        boost::beast::flat_buffer buffer;
```

我们使用 ssl::stream 而不是 tcp::socket。这在 TCP 套接字之上提供了 SSL/TLS 功能。

我们调用 stream.handshake(ssl::stream_base::client) 在发送 HTTP 请求之前执行 SSL/TLS 握手。

完成后，我们调用 stream.shutdown() 干净地关闭 SSL/TLS 连接。我想告诉你的一点是，这个程序默认不会验证服务器证书。要进行正确的证书验证，你需要调用 ctx.set_verify_mode(ssl::verify_peer)，并使用 ssl::rfc2818_verification 对象来验证服务器身份。

```cpp
CURL *curl;
CURLcode res;
std::string ftpUrl = "ftp://example.com/myfile.txt";
std::string username = "myusername";
std::string password = "mypassword";
std::string ftpCommand = "RNFR myfile.txt";
std::string renameCommand = "RNTO newfile.txt";

curl_global_init(CURL_GLOBAL_DEFAULT);
curl = curl_easy_init();

if(curl) {
    struct curl_slist *headerlist=NULL;
    headerlist = curl_slist_append(headerlist, ftpCommand.c_str());
    headerlist = curl_slist_append(headerlist, renameCommand.c_str());
    curl_easy_setopt(curl, CURLOPT_URL, ftpUrl.c_str());
    curl_easy_setopt(curl, CURLOPT_USERNAME, username.c_str());
    curl_easy_setopt(curl, CURLOPT_PASSWORD, password.c_str());
    curl_easy_setopt(curl, CURLOPT_POSTQUOTE, headerlist);

    res = curl_easy_perform(curl);
    if(res != CURLE_OK)
        fprintf(stderr, "curl_easy_perform() failed: %s\n",
                curl_easy_strerror(res));

    curl_slist_free_all(headerlist);
    curl_easy_cleanup(curl);
}

curl_global_cleanup();
return 0;
}
```

这演示了如何使用 C++ 和 libcurl 在 FTP 服务器上重命名文件（将 myfile.txt 重命名为 newfile.txt）。在这段代码中，我们使用 CURLOPT_POSTQUOTE 选项将 FTP 命令传递给 libcurl。命令 RNFR 用于指定文件的旧名称，RNTO 用于指定新名称。

在使用这段代码之前，你需要安装 libcurl，并将 ftp://example.com/myfile.txt、myusername 和 mypassword 替换为实际的 FTP 服务器 URL、用户名和密码。

## SMTP 与 IMAP 深入解析

SMTP（Simple Mail Transfer Protocol，简单邮件传输协议）是一种用于电子邮件传输的通信协议。它是邮件服务器用来发送和接收电子邮件消息的机制。当你发送电子邮件时，它会使用 SMTP 通过 Internet 从一台服务器传输到另一台服务器。

另一方面，IMAP（Internet Message Access Protocol，Internet 消息访问协议）是电子邮件客户端用来从邮件服务器检索消息的协议。当你检查收件箱时，电子邮件客户端会使用 IMAP 联系服务器以获取你的电子邮件。

在 C++ 中，你可以使用 VMime 库发送（SMTP）和接收（IMAP）电子邮件。VMime 是一个强大的 C++ 类库，用于解析、生成或编辑 Internet RFC 2822 和 MIME 消息。VMime 旨在提供一种快速简便的方式来操作 Internet 邮件消息。

### 使用 VMime 库发送电子邮件

下面是一个如何使用 VMime 发送电子邮件的简单示例：

```cpp
#include

#include

int main() {
    vmime::platform::setHandler();

    // Constructs a new message
    vmime::shared_ptr msg = vmime::make_shared();

    // Fill in the basic fields
    msg->getHeader()->getSubject()->setValue("Test mail");
    msg->getHeader()->getFrom()->appendAddress(vmime::make_shared("me@example.com"));
    msg->getHeader()->getTo()->appendAddress(vmime::make_shared("you@example.com"));

    // Message body
    vmime::shared_ptr txt = vmime::make_shared("Hello, world!");
    msg->getBody()->setContents(txt);

    // Now, let's create the SMTP transport service
    vmime::shared_ptr sess = vmime::net::session::create();
```
