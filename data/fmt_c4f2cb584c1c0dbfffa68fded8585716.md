
在 Fedora 和 RHEL 中，基础 Apache 服务器的主配置文件位于`/etc/httpd/conf/httpd.conf`。除了此，`/etc/httpd/conf.d`目录下的任何文件也用于 Apache 配置。在 Ubuntu 中，Apache 配置存储在 Apache 服务器读取的文本文件中，从`/etc/apache2/apache2.conf`开始。

## 使用指令

许多配置指令的范围可以根据上下文进行更改。也就是说，某些参数可以在全局级别设置，并在特定文件或目录中更改。

或虚拟主机。其他指令本质是全局性的，例如指定服务器监听哪些 IP 地址的指令。另一些指令仅在应用于特定位置（location）时有效。

位置以这种形式进行配置：包含一个包含位置类型的起始标签，随后紧跟该位置的配置选项，并以结束标签结尾。这种形式通常被称为配置块（configuration block），看起来与 HTML 代码非常相似。一种特殊的配置块被称为位置块（location block），用于将指令的范围限制到特定的文件或目录。这些块包含以下内容：

```
<locationtag specifier>
(特定于此块内匹配指定符的对象的特定选项)
</locationtag>
```

存在不同类型的位置标签，并根据所指定的资源位置类型进行选择。起始标签中的指定符将根据位置标签的类型进行处理。你通常使用的位置标签有`Directory`（目录）、`Files`（文件）和`Location`（位置），它们将指令的范围限制到特定的目录、文件或位置。

- `Directory`标签用于根据文件系统上的位置指定路径。例如，`<Directory />`指向计算机上的根目录。目录继承其上级目录的设置，最具体的`Directory`块会覆盖不那么具体的块，无论它们在配置文件中的出现顺序如何。

- `Files`标签用于通过名称指定文件。`Files`标签可以包含在`Directory`块中，以将其限制为目录下的文件。`Files`块中的设置会覆盖`Directory`块中的设置。

- `Location`标签用于指定访问文件或目录的 URI。它与`Directory`的不同在于，它与请求包含的地址有关，而不是文件在驱动器上的实际位置。`Location`标签最后处理，并覆盖`Directory`和`Files`块中的设置。

这些标签的匹配版本——`DirectoryMatch`、`FilesMatch`和`LocationMatch`——具有相同的功能，但在资源规范中包含正则表达式。`FilesMatch`和`LocationMatch`块分别与`Files`和`Location`块同时处理。`DirectoryMatch`在`Directory`块之后处理。

Apache 还可以配置为处理包含在`AccessFileName`指令中指定的名称的文件中的配置选项（该指令通常设置为`.htaccess`）。访问配置文件中的指令将应用于其所包含的目录下的所有对象，包括子目录及其内容。访问配置文件与`Directory`块同时处理，并使用类似的“最具体匹配”原则。

# 第四部分：成为 Linux 服务器管理员

# 第 17 章：配置 Web 服务器

## 注意

访问控制文件对于允许用户在无法访问服务器文件的情况下更改特定设置非常有用。访问配置文件中允许的配置指令由其所在目录的`AllowOverride`设置决定。某些指令在这些层级上没有意义，并且在尝试访问 URI 时通常会导致产生“服务器内部错误”消息。`AllowOverride`选项在`http://httpd.apache.org/docs/mod/core.html#allowoverride`中有详细介绍。

位置块和访问控制文件中常见的三个指令是`DirectoryIndex`、`Options`和`ErrorDocument`：

- `DirectoryIndex`告诉 Apache 当 URI 包含目录但不包含文件名时，应加载哪个文件。该指令在`Files`块中不起作用。

- `Options`用于调整 Apache 处理目录内文件的方式。`ExecCGI`选项允许 Apache 识别可以被 CGI 脚本运行的文件，而`Includes`选项告诉 Apache 允许服务器端包含 (SSI)。另一个常用选项是`Indexes`选项，如果`DirectoryIndex`设置中的其中一个文件名缺失，它告诉 Apache 生成文件列表。可以指定选项的绝对列表，也可以通过在选项名称前添加或删除`-`来修改选项列表。更多信息请参阅`https://httpd.apache.org/docs/mod/core.html#options`。

- `ErrorDocument`指令用于指定在发生特定错误时发送包含消息的文件。该文件的位置相对于`/var/www`。该指令必须指定错误代码和错误文档的完整 URI。可能的错误代码包括`403`（拒绝访问）、`404`（未找到）和`500`（服务器内部错误）。你可以在`http://httpd.apache.org/docs/mod/core.html#errordocument`找到更多关于`ErrorDocument`的信息。例如，当客户端从服务器请求一个未找到的 URI 时，以下`ErrorDocument`行会使`404`错误代码向客户端发送一个在`/var/www/HTTP_NOT_FOUND.html`中列出的错误消息：

```
ErrorDocument 404 /error/HTTP_NOT_FOUND.html
```

位置块和访问控制文件的另一个常见用途是限制或扩展对资源的访问。`Allow`指令可用于允许匹配主机的访问，而`Deny`指令可用于禁止访问。这两个选项在块内都可能出现多次，并由`Order`设置处理。将`Order`设置为`Deny, Allow`允许访问一个范围，而设置为`Allow access`则允许访问该范围的子集。通过添加`Satisfy`选项一些额外的参数，你可以添加密码验证。

有关`Allow`或`Deny`、`Satisfy`或其他指令的更多信息，请参考 Apache 指令索引：`http://httpd.apache.org/docs/current/mod/directives.html`。

## 理解默认设置

为了帮助你理解默认`httpd.conf`文件中的设置，我在下方显示了其中一些设置及其描述。我删除了注释并重新排列了其中一些内容。

以下设置显示了`httpd`的位置：

```
ServerRoot "/etc/httpd"
Include *.conf
ErrorLog logs/error_log
CustomLog logs/access_log"
DocumentRoot "/var/www/html"
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

`ServerRoot`指明`/etc/httpd`为配置存储位置。`Include`指令显示包含哪些文件。`ErrorLog`和`CustomLog`指明活动记录的地方。`DocumentRoot`指明`/var/www/html`为首页。`ScriptAlias`指明`cgi-bin/`位于`/var/www/cgi-bin/`。

以下设置显示了：

`DocumentRoot`和`ScriptAlias`指令决定了内容的所在地。传统上，你会在`DocumentRoot`目录(`/var/www/html`)中放置`index.html`文件并根据需要添加其他内容。`ScriptAlias`告诉守护进程`cgi-bin`中的脚本。例如，客户端可以通过请求如`http://example.com/cgi-bin/`的 URL 来访问脚本。

除了文件位置，你可以在`httpd.conf`中找到其他信息。是一些示例：

- `Listen 80`

- `User apache`

- `Group apache`

- `ServerAdmin root@localhost`

- `DirectoryIndex index.html php`

- `AccessFileName .htaccess`

`Listen 80`告诉`httpd`在端口`80`（HTTP 默认端口）上监听请求。默认情况下，它监听所有网络接口，但你可以通过 IP 地址将其限制在选定的接口上（例如：`80`）。

`User`和`Group`指令告诉`httpd`以`apache`用户和组身份运行。`ServerAdmin`的值（默认是`root@localhost`）将发布在某些网页上，以告知用户服务器问题。

`DirectoryIndex`列出了请求目录时的文件。例如，如果网络浏览器请求`//whatever/`，`httpd`将检查`/var/www/html/whatever/index.html`是否存在，如果存在则提供服务。如果不存在，在本例中，`httpd`将查找`index.php`。如果找不到该文件，则将显示目录的内容。

`AccessFileName`指令允许你告诉`httpd`如果目录中存在`.htaccess`文件，使用其内容来读取允许访问该目录的设置。例如，该文件可以用于对目录进行密码保护，或者指示如何方式显示目录内容。为了使此文件生效，`Directory`容器（见下）需要开启`AllowOverride`。（默认情况下，`AllowOverride None`防止`.htaccess`文件用于任何指令）。

以下`Directory`容器定义了访问根目录(`/`)、`/var/www`和`/var/www/html`目录时的行为：

```
<Directory /> /
AllowOverride none
Require all denied
```

```apache
<Directory "/var/www">
  AllowOverride None
  # 允许开放访问：
  Require all granted
</Directory>
<Directory "/var/www/html">
  Options FollowSymLinks
  AllowOverride None
  Require all granted
</Directory>
```

`<Directory>`指令表示`httpd`尝试访问 Linux 文件系统中的任何文件，但会被拒绝。`AllowOverride none`指令防止`.htaccess`文件覆盖该目录的设置。这些设置适用于任何未在其他`Directory`（目录）容器中定义的子目录。

在`/var/www`目录下的内容访问限制被放宽。允许访问在该目录下添加的内容，但不允许覆盖设置。

`/var/www/html`目录包含符号链接且不允许进行覆盖。通过`Require all granted`，`httpd`阻止了对服务器的任何访问。

如果所有描述的设置对你有效，那么你就可以向`/var/www/html`和`/var/www/cgi-bin`目录中添加你想要的内容。你可能对默认设置不满意的一个可能是你可能想为多个域名提供内容（例如`example.com`、`example.org`和`example.net`）。要实现这一点，你需要配置虚拟主机（virtual hosts）。虚拟主机将在下一节中详细介绍，它们是一个方便（几乎是必需的）工具，可以根据请求指向的服务器地址或名称向客户端提供不同的内容。大多数配置选项都适用于虚拟主机，但可以被`<VirtualHost>`块内的指令所覆盖。

### 为 Apache 添加虚拟主机

Apache 支持在单个服务器内创建独立的网站，以保持内容分离。各个站点在同一台服务器上进行配置，被称为虚拟主机。

虚拟主机实际上只是一种方法，允许从同一个 Apache 服务器提供多个域名的内容。你不再需要为每个域名准备一个物理系统来提供内容，而是可以从同一个操作系统为多个域名提供内容。

正在进行虚拟主机托管的 Apache 服务器可能有多个解析到服务器 IP 地址的域名。提供给 Web 客户端的内容取决于访问服务器时使用的名称。

例如，如果客户端通过请求名称`www.example.com`访问服务器，则客户端将被重定向到一个`ServerName`设置为响应`www.example.com`的虚拟主机容器。该容器将提供内容的位置，并可能提供与全局设置不同的错误日志或`Directory`指令。每个虚拟主机都可以像在单独机器上一样进行管理。

要使用基于名称的虚拟主机托管，请开启`NameVirtualHost`指令。然后根据需要添加多个`VirtualHost`容器。以下是配置虚拟主机的方法：

> 注意

> 启用`NameVirtualHost`后，如果通过 IP 地址或未在`VirtualHost`容器中设置的名称访问服务器，则默认的`DocumentRoot(/var/www/html)`将不再被使用。相反，`VirtualHost`容器将作为服务器的默认位置。

1. 在 Fedora 或 RHEL 中，使用此模板创建一个名为`/etc/httpd/conf.d/example.org`的文件：

```apache
NameVirtualHost *:80
<VirtualHost *:80>
ServerAdmin webmaster@example.org
ServerName www.example.org
ServerAlias web.example.org
DocumentRoot /var/www/html/example.org/
DirectoryIndex index.php index.htm
</VirtualHost>
```

此示例包含以下内容：

- `NameVirtualHost`行告诉 Apache 根据 HTTP 客户端提供的主机名来确定从哪个虚拟主机提供文档。

- 对任何 IP 地址的 80 端口的`*:80`请求将以此种方式处理。

- `VirtualHost`块中的`*:80`指定了该虚拟主机适用的地址和端口。如果你的 Linux 系统关联了多个 IP 地址，可以将`*`替换为特定的 IP 地址。对于`NameVirtualHost`和`VirtualHost`指定，端口是可选的，但应始终使用以防止与 SSL 虚拟主机（默认使用端口 443）发生干涉。

- `ServerName`和`ServerAlias`行告诉 Apache 该虚拟主机应该被识别为哪个名称，因此将它们替换为适用于你网站的名称。如果你没有备用名称，可以留着`ServerAlias`行；如果你有多个备用名称，可以在每个`ServerAlias`行指定多个名称，或使用多个`ServerAlias`行。

- `DocumentRoot`指定了 Web 文档（为此站点提供的内容）的存储位置。虽然显示为在默认`DocumentRoot`(`/var/www/html`）下创建的子目录，但通常网站会挂载到特定用户的家目录（例如`/home/chris/public_html`），以便每个目录都可以由不同的用户管理。

启用主机后，使用`apachectl`检查配置，然后进行平滑重启：

```bash
# apachectl configtest
Syntax OK
# apachectl graceful
```

只要你已经在 DNS 服务器上注册了网站，浏览器就应该能够使用`www.example.org`或`web.example.org`访问该网站。如果可行，你也可以开始向系统添加虚拟主机了。

扩展网站用途的另一种方法是允许多个用户在你的服务器上共享他们的内容。如下一节所述，你可以允许用户在其家目录的子目录下添加他们想要与你的 Web 服务器共享的内容。

> 注意

> 将虚拟主机保持在单独的文件中是虚拟主机的方便方法。但是，你应该小心地将它们分开。

### 允许用户发布自己的 HTML

在你的配置中没有这些块的情况下，你可能需要创建它们。如果启用了`mod_userdir`模块（默认未启用），家目录对 Web 可用。例如，`example.org`上名为`wtucker`的用户内容存储在`/home/wtucker/public_html`。

1. 创建`<IfModule userdir.c>`块。将`chris`更改为想要创建自己的`public_html`目录的用户名。

```apache
<IfModule userdir.c>
UserDir enabled chris
</IfModule>
```

2. 创建`<Directory>`指令并根据喜好设置。块看起来如下：

```apache
<IfModule userdir.c>
<Directory "/home/*/public_html">
Options Indexes FollowSymlinks
Require all granted
</Directory>
</IfModule>
```

3. 让用户在他们的家目录创建`public_html`目录：

```bash
$ mkdir $HOME/public_html
```

4. 设置执行权限（root 用户），允许`httpd`守护进程访问家目录：

```bash
# chmod +x /home/*
```

5. 如果 SELinux 强制模式（在 Fedora 和 RHEL 中默认如此），设置 SELinux 文件内容属性允许`httpd`守护进程访问内容：

```bash
# chcon -R --reference=/var/www/html /home/*/public_html
```

6. 设置 SELinux 布尔值允许用户从家目录共享 HTML 内容：

```bash
# setsebool -P httpd_enable_homedirs true
```

7. 重启或加载`httpd`。

此时，你应该能够通过浏览器指向`http://hostname/~user`来访问用户`public_html`目录中的内容。

## 使用 SSL/TLS 保护你的 Web 流量
