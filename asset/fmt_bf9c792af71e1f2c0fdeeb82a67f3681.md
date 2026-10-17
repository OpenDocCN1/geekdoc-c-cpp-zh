
使用标准 HTTP 协议的网站任何数据都是以明文发送。这意味着任何可以监控服务器和客户端之间网络上流量的人都可以嗅探网络并看到你的数据。

电子商务应用程序（如在线购物和银行）通常使用安全套接层 (SSL) 或传输层安全 (TLS) 进行加密。

# 第四部分：成为 Linux 服务器管理员

TLS 是基于 SSL 3.0 版本的，因此它们在本质上非常相似。由于这种相似性——加上 SSL 较老——SSL 缩写通常被用来泛指。对于 Web 连接，首先建立 SSL 连接，然后普通的 HTTP 通信通过它进行“隧道传输”。

注意

由于 SSL 协商发生在任何 HTTP 通信之前，基于名称的虚拟主机（发生在 HTTP 层）与 SSL 配合并不良好。因此，每个 SSL 虚拟主机都应该有一个唯一的 IP 地址。（参见 Apache 站点信息：http://apache.org/docs/hosts.html）

当你在 SSL 客户端和 SSL 服务器之间建立连接时，使用非对称（公共）加密来验证身份并建立会话参数。DES 或 RC4 等对称加密算法用于加密会话期间传输的数据。在使用非对称加密后，对称加密对于会话数据传输更快且更实用。

为了让客户端验证服务器的身份，服务器必须有一个预先生成的公密钥以及一个包含服务器信息的证书。证书必须使用客户端知的公密钥进行验证。

证书通常由第三方证书机构（CA）进行数字签名，CA 验证了请求者的身份和请求的有效性。在大多数情况下，CA 是一个与 Web 浏览器达成安排并默认信任其证书的公司。CA 更改了服务器。

商业证书机构在价格、功能和浏览器支持方面各异，但请记住价格并不代表质量。流行的 CA 包括 InstantSSL (http://www.instantssl.com)、Thawte (http://thate.com) 和 Symantec (http://www.symantec.com/ssl-certificates)。

最后一个选项是运行自己的证书机构。这可能适用于预期用户较少且你有向他们分发 CA 证书（包括帮助他们在浏览器中安装）。创建 CA 的过程在书中过于详尽，但生成自签名证书是一个不错的替代。

# 第 17 章：配置 Web 服务器

后续章节描述了在安装 `mod_ssl` 包时，Fedora 和 RHEL 中如何配置 HTTPS 通信。之后，我将描述如何生成自己的 SSL 密钥和证书，以改进在本章配置的 Fedora 或 RHEL 系统上的 SSL 通信。

## 理解 SSL 如何配置

如果你在 Fedora 或 RHEL 中安装了 `mod_ssl` 包（在安装 Web 服务器时默认完成的），当包安装时会创建一个自签名证书和私钥。这允许你立即使用 HTTPS 协议与 Web 服务器通信。

虽然 `mod_ssl` 的默认配置允许 Web 服务器与客户端之间进行加密通信，但由于证书是自签名的，访问你站点的客户端是不安全的。通过探索 Apache Web 服务器的 SSL 配置，确保运行 Apache (`httpd`) 服务的服务器已安装 `mod_ssl` 包：

```
# yum install mod_ssl
```

`mod_ssl` 包包含了在 Web 服务器上实现 SSL 的模块（`mod_ssl.so`）以及用于 SSL 主机的配置文件：`/etc/httpd/conf.d/ssl.conf`。该文件中有很多注释可以帮助你修改。那些未注释的内容定义了一些初始设置和一个默认虚拟主机。以下是其中一些：

- VirtualHost 443 https

```apache
<VirtualHost _default_:443>
ErrorLog logs/ssl_error_log
TransferLog logs/ssl_access_log
LogLevel warn
...
LCificateFile /etc/pki/tls/certs/localhost.crt
SSLCertKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

SSL 服务设置为在系统所有接口的标准 SSL 端口 `443` 上监听。

创建了一个 VirtualHost 块，导致错误消息和访问消息记录到与服务器使用的标准日志（`/var/log/httpd/` 目录下的 `ssl_error_log` 和 `ssl_access_log`）分离的文件中。消息级别设置为 `warn` 并开启了 SSL 引擎。

## 第四部分：成为 Linux 服务器管理员

在之前的示例代码中，VirtualHost 块中与 SSL 证书相关的两个条目标识了密钥和证书信息。安装 `mod_ssl` 时会生成密钥并将其放在 `/etc/pki/tls/private/localhost.key` 文件。使用该密钥创建一个自签名证书 `/etc/pki/tls/certs/localhost.crt`。当你创建自己的证书时，需要替换此文件中的 `SSLCertificateFile` 和 `SSLCertificateKeyFile` 的值。

在安装 `mod_ssl` 包并重新加载配置后，可以通过以下步骤测试自签名证书是否正常：

- 1. **通过浏览器使用 HTTPS 访问网站。** 例如，在运行服务器的系统上的地址框中输入 `https://localhost` 并按回车。图 17.2 显示了出现的页面。

img 17.2: 使用默认证书访问 SSL 网站 (3886a4c1a68ab63e25e8e0a2d63de95.png)

 因为你是通过浏览器访问站点，点击“添加例外”。Firefox 会警告你将接受此证书。

- 3. 选择“查看”查看生成的证书。它包含了主机名、颁发和过期时间以及其他组织信息。

- 4. 关闭该窗口，然后选择“确认”接受连接。你现在可以看到使用 HTTPS 的默认页面。从现在起，你的浏览器将接受该证书并加密所有通信。

## 生成 SSL 密钥和自签名证书

要开始设置 SSL，使用 `openssl` 命令（属于 `openssl` 包）生成你的公钥和私钥。之后，你可以生成自己的自签名证书用于测试或内部使用。

- 1. 如果尚未安装 `openssl` 包，请按以下方式安装：

```
# yum install openssl
```

- 2. 生成 1024 位的 RSA 私钥并将其保存到文件：

```
# cd /etc/pki/tls/private
# openssl gensrsa -out server.key 1024
# chmod 600 server.key
```

- 3. 如果你不打算让你的证书签名，或者想测试你的配置，生成一个自签名证书并将其保存到 `/etc/pki/tls/certs` 目录下名为 `server.crt` 的文件中：

## 第四部分：成为 Linux 服务器管理员

```bash
# cd /etc/pki/tls/certs
# openssl req -new -x509 -nodes -days 365 \
  -key /etc/pki/tls/private/server.key \
  -out server.crt
Country Name (2 letter code) [AU]: US
State or Province Name (full name) [Some-State]: NJ
Locality Name (eg, city) [Default City]: Princeton
Organization Name (eg, company) [Default Company Ltd Ltd]:TEST USE ONLY
Organizational Unit Name (eg, section) [:TEST USE ONLY
Common Name (eg, YOUR name) [:secure.example.org
Email Address [:dom@example.org
```

4. 编辑 `/etc/httpd/conf.d/ssl.conf` 以更改密钥和证书的位置，以使用你刚刚创建的文件。例如：

```apache
SSLCertificate /etc/pki/tls/certs/server.crt
SSLCertificateFile /etc/pki/tls/private/server.key
```

5. 重启 `httpd` 服务。

6. 从本地浏览器中打开 `https://localhost`，重复此过程进行检查并接受新证书。

对于内部使用或测试，自签名证书可能适用于你。但是，对于公共网站，你应该使用由证书颁发机构（CA）验证的证书。接下来将介绍该操作步骤。

### 生成证书签名请求 (CSR)

如果你计划让 CA 签名你的证书（包括你自己运行的 CA），可以使用你的私钥生成证书签名请求 (CSR)：

- 1. 创建一个用于存储 CSR 的目录。

```
# mkdir /etc/pki/tls/ssl.csr
# cd /etc/pki/tls/ssl.csr/
```

- 2. 使用 `openssl` 命令生成 CSR。在输入信息后，当前目录下会生成一个 CSR 文件，通用名称（Common Name）应与客户端访问你的服务器时使用的名称匹配。确保其他细节正确，以便其通过第三方 CA 的验证。此外，如果你为密钥设置了密码，系统会提示在此处输入密码以使用该密钥。

```bash
# openssl req -new -key ../private/server.key -out server.csr
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Washington
```

## 第 17 章：配置 Web 服务器

Locality Name (eg, city) []:Bellingham

Organization Name (eg, company) [Internet Widgets Pty Ltd]:Example Company, LTD.

Organizational Unit Name (eg, section) []:Network Operations

Common Name (eg, YOUR name) [:secure.example.org

Email Address [:dom@example.org

请输入以下随证书请求一同发送的“额外”属性：

挑战密码 (challenge password) []

可选的公司名称 []:

- 3. 访问你选择的证书颁发机构的网站，并请求经过签名的证书。在某个时刻，CA 可能会要求你将 CSR 内容（在此处的 `server.csr` 文件）复制并粘贴到请求所需的表单中。

- 4. 当 CA 向你发送证书时（可能通过电子邮件），将其保存到 `/etc/pki/tls/certs/` 目录，并根据你托管的站点命名——例如 `example.org`。

- 5. 修改 `/etc/httpd/conf.d/ssl.conf` 中的 `SSLCertificateFile` 值指向你的新 CRT 文件。或者，如果你有多个 SSL 主机，可能想要创建一个独立的（可能是 `.conf` 文件），其内容如下：

```apache
Listen 192.168.0.56:443
<VirtualHost *:443>
ServerName secure.example.org
ServerAlias web.example.org
DocumentRoot /home/username/public_html/
DirectoryIndex index.php index.htm
SSngine On
SSLCificateKeyFile /etc/pki/tls/private/server.key
SSLCificateFile /etc/pki/tls/certs/example.org.crt
</VirtualHost>
```

`Listen` 指令中的 IP 地址应该替换为代表你所服务的 SSL 主机的公网 IP。记住，每个 SSL 主机都应该有自己的 IP 地址。

## 故障你的 Web 服务器

在任何复杂的环境中，你偶尔都会遇到问题。本节包含了隔离和解决你可能遇到的最常见错误的信息。

### 检查配置错误

你可能会偶尔遇到配置错误或脚本问题，导致 Apache 无法启动或特定文件无法访问。这些问题中的大多数可以使用两个 Apache 提供的工具进行隔离和解决：`apachectl` 程序和系统错误日志。

当遇到问题时，首先使用 `apachectl` 程序配合 `configtest` 参数来测试配置。事实上，养成每次更改配置都运行该命令的习惯是好的：

```bash
# apachectl configtest
Syntax OK
/usr/bin/apachectl graceful: httpd gracefully restarted
```

如果发生语法错误，Apache 会指示错误发生的位置，并且最好能提供关于问题性质的提示。你可以使用 `graceful` 重启选项（`apachectl graceful`）来指示 Apache 在不断开任何客户端连接的情况下重新加载配置。

> 注意

> `graceful` 重启选项允许 Apache 在不断开任何客户端连接的情况下重新加载配置。

# 第四部分：成为 Linux 服务器管理员

任何重要性至少等于你选择的 `LogLevel` 的消息都会存储在 `ErrorLog` 中。在典型的服务器上，`LogLevel` 被设置为 `warn`。你不应该将其设置为任何低于 `crit` 的值，并应避免将其留为 `debug`，因为这会减慢服务器速度并导致 `ErrorLog` 非常大。

作为最后的手段，你可以尝试手动运行 `httpd -X` 来检查崩溃或其他错误信息。`-X` 参数会运行 `httpd`，因此它会在屏幕上显示 `debug` 及更高级别的消息。

### 访问被禁止和服务器内部错误

当你尝试查看服务器上的特定页面时，可能会遇到两种常见的错误类型：权限错误和服务器内部错误。这两种错误通常可以使用错误日志中的信息进行定位。在对下列表描述的任何更改以尝试解决这些问题之后，请尝试重新请求并检查错误日志，查看消息是否发生了变化（例如，显示操作成功完成）。

> 注意

> “File not found”（找不到文件）错误可以按照检查“access forbidden”（拒绝访问）和“server internal errors”（服务器内部错误）相同的方式进行检查。你有时会发现 Apache 并没有在你认为它尝试查找特定文件的地方。通常，文件路径会出现在错误日志中。确保你使用的是正确的虚拟主机，并检查可能的 `Alias` 设置，这些设置可能会将你的位置引导到意想不到的地方。

- 文件权限——“File permissions prevent access”（权限阻止访问）错误表示 `apache` 进程由无法打开请求文件的用户运行。默认情况下，它由 `apache` 用户和组运行。确保该账户对目录及其上方的每个目录具有执行权限，并对文件本身具有读取权限。如果你想让 Apache 生成文件索引，也需要目录的读取权限。参阅 `chmod` 的手册页获取有关如何查看和更改权限的更多信息。

> 注意

> 编译后的二进制文件不需要读取权限，因为这些用 C 或 C++ 编写的程序可以安全地执行，除非需要保持程序内容的秘密。

- 拒绝访问——“Client denied by server configuration”（服务器配置拒绝客户端）错误表示 Apache 已配置为拒绝访问该对象。检查配置文件中的 `Location` 和 `Directory` 部分，这些部分可能会影响你正尝试访问的文件。记住，应用于路径的设置也会应用于该路径下方的任何路径。你可以通过仅更改你允许访问的更具体的路径的权限来覆盖此设置。

## 第 17 章：配置 Web 服务器

- **找不到索引**——“Directory index forbidden by rule”（规则禁止目录索引）错误表示 Apache 无法找到 `DirectoryIndex` 指令中指定的索引文件，并且被配置为不创建目录文件列表的索引。如果你有索引页面，请确保它具有相关 `DirectoryIndex` 指令指定的名称之一，或者在对应对象的适当 `Directory` 或 `Location` 部分中添加 `Options` 行。

- **脚本崩溃**——“Premature end of script headers”（脚本头过早结束）错误表示脚本在完成之前崩溃了。有时，导致此现象的错误也会出现在日志中。在使用 `suexec` 或 `PHP` 时，此错误也可能由文件所有权或权限错误引起。这些错误出现在 `/var/log/httpd/` 的日志文件中。

- **SELinux 错误**——如果文件权限是开启的，但日志中出现了拒绝权限的消息，则可能是 SELinux 导致了问题。临时将 SELinux 设置为 `Permissive` 模式（`setenforce 0`），然后再次尝试访问文件。如果文件现在可以访问，则将 SELinux 设置为 `Enforcing` 模式（`setenforce 1`）并检查文件上下文和布尔值（Boolean）。`httpd` 访问文件时，文件上下文必须正确。布尔值可能会防止从远程监控的目录提供文件，或防止页面发送电子邮件或上传文件。输入 `man httpd_selinux` 可获取与 `httpd` 服务相关的 SELinux 配置设置的详情。（安装 `selinux-policy-dev` 包可以将该页面添加到你的系统中。）

## 总结

开源 Apache 项目是世界上最流行的 Web 服务器。尽管 Apache 提供了极大的活性、安全性和复杂，但在 Fedora、RHEL 和大多数 Linux 发行版中，只需几分钟即可配置一个基础的 Apache Web 服务器。

本章介绍了安装、配置、安全和故障排除基础 Apache Web 服务器的步骤。你学习了如何配置虚拟主机和安全 SSL 主机。你还学习了如何配置 Apache 允许系统上的任何用户账户从其 `public_html` 目录发布内容。
