
如果已加载，*Web 服务器配置显示*（`mod_info`）模块会使所有配置文件都可用，甚至精细到目录级别（想想 `.htaccess`）。这对你的站点造成的安全威胁是：该模块会向 Apache 的其他部分“泄露”有关配置指令的信息。这可能包括系统路径、用户名和密码、已安装的数据库等。强烈建议不要在面向 Internet 的服务器等生产环境中运行此模块。

如果在配置文件中发现以下行，请将其注释掉：

```
LoadModule info_module modules/mod_info.so
```

专职黑客的部分工作将是 *枚举* 你的网站。本质上，这意味着黑客会尝试找出并命名所有内容，以绘制网络和服务器的结构。如果已安装，`speling_module` 模块会尝试查找一个 *文档*（即诸如文件之类的资源），方法是将所请求目录中的每个文档名称与请求的文档名称进行比较，比较时不区分大小写，并允许最多一个拼写错误。

这种情况非常适合持续向站点发送请求进行探测，并查看会出现哪些文件。建议禁用此模块（如果已安装）。如果在配置文件中发现以下行，请将其注释掉：

```
LoadModule speling_module modules/mod_speling.so
```

利用目录转换模块的能力，攻击者可以轻易枚举 Web 服务器的用户。如果在配置文件中发现以下内容，除非绝对需要，否则请禁用：

```
LoadModule userdir_module modules/mod_userdir.so
```

如果你没有将 Apache 服务器用作通往其他服务器的 *代理服务器*（网关），那么请确保以下行（如果存在）已被注释掉：

```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule proxy_connect_module modules/mod_proxy_connect.so
```

如果你不知道代理服务器有什么用途，那你很可能不需要它。如果服务器没有完全加固，保持其启用是非常危险的。

> **注意** 有关 Apache 配置文件中指令的更多信息，请参见 http://httpd.apache.org/docs/2.2/mod/quickreference.html。

## 禁用或设置适当的服务

尽管每个 Apache 配置都大不相同，但了解启动时会启动哪些程序很重要。这些知识可以让你很好地了解应该启用或禁用哪些程序。你可能会拥有类似于图 5-9 所示的服务，该图显示了此特定服务器上启动的服务。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_166_0.png)

花些时间使用以下命令检查你的服务器：

```bash
# chkconfig --list | grep :on
```

调查这些服务，如果你确定不需要其中一个或多个，请使用以下命令禁用该服务：

```bash
# chkconfig service off
```

将该命令中的 service 一词替换为服务名称，如下所示：

```bash
# chkconfig pure-ftpd off
```

该命令会在下次重启时禁止 FTP 服务器运行。

### 那是什么服务？

有时，你可能会看到一个不确定的服务正在运行。这不必惊慌，但你可能想进一步调查。要了解该服务来自哪个 RPM 包（安装包），请运行以下命令：

```bash
$ rpm -qf /etc/init.d/servicename
```

这会显示是哪个包安装了它。它很可能只是另一个服务的依赖项。

你还可以通过输入以下命令来简要了解该 RPM 包的作用：

```bash
$ rpm -qi rpmname
```

请注意，此命令可能不适用于所有 Linux 发行版。

你应当开启的一项服务是 ModSecurity。让我们更仔细地了解这个非常重要的模块。

### ModSecurity

ModSecurity（可从 www.modsecurity.org 获取）是一个开源 Web 应用防火墙（WAF）。它的职责是保护 Web 应用层，抵御各种针对 CMS 和其他 Web 应用弱点的攻击。它通过多种防御手段来实现这一点，包括监控 HTTP（Web）流量、灵活的策略引擎以及对流量的实时分析。

ModSecurity（或 mod_security）作为反向代理工作，并提供针对攻击的虚拟补丁。强烈建议使用此 WAF 或其他类型的 WAF。

使用 yum 安装 mod_security 非常简单：

```bash
# yum install mod_security
```

默认配置很可能就适合你，但鉴于其灵活的策略引擎，你也可以选择在其上部署高度自定义的配置。更深入的细节超出了本书的范围。以下来源可以提供更多信息：

- *ModSecurity 手册*（伦敦，Feisty Duck, Ltd.，2010），由 ModSecurity 首席开发者 Ivan Ristic 编写。更多信息请参见 www.feistyduck.com/books/modsecurity-handbook/index.html。
- 另一个参考资料是一份相当完善的指南，介绍如何在 Ubuntu 上安装 ModSecurity，位于：www.thebitsource.com/infrastructure-operations/web-application/securing-apache-web-servers-modsecurity。

它是一个工具，强制 PHP 脚本（如你的 CMS）以脚本所有者的权限执行。

suPHP 是一个很好的工具，可确保你以非常安全的方式运行 PHP。如果你使用的是托管公司提供的受管理虚拟专用服务器（VPS）或专用服务器，快速致电支持人员可以帮助你确认是否正在运行它。

下一种方法是尝试将文件夹权限设置为 777。如果你正在运行 suPHP，浏览时会收到 500 Internal Error。

### phpinfo

PHP 有一种很好的方法来检查全部设置。使用 phpinfo 函数可在你的工具包中提供一个有用的工具。

这里列出的执行 phpinfo 函数的步骤非常容易遵循，而且最终结果非常有价值：

1. 在根目录中创建一个文本文件，并将其命名为 `phpinfo.php`。在该文件中插入以下内容：

    ```
    <?php phpinfo(); ?>
    ```

2. 保存该文件，并确保权限设置为 644。

3. 在浏览器中输入以下内容：

    ```
    http://www.yourdomain.com/phpinfo.php
    ```

大量关于服务器及其环境设置的信息会出现。在屏幕顶部附近，你应该会看到一个类似于图 5-10 的条目。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_170_0.png)

**图 5-10：** 已安装 suPHP

如果你看到的是 apache 而不是 CGI/FastCGI 字样，那么你很可能没有安装 suPHP。

PHP 有许多可能难以发现的设置。幸运的是，有一个免费的开源工具可以很好地评估你的设置，如下一节所述。

### PhpSecInfo

PhpSecInfo 工具由 PHP 安全领域的国际专家团体 PHP 安全联盟（PHPSC）打造，用于评估服务器的设置并确保关闭所有 PHP 漏洞。你可以通过访问以下地址获取该工具：

```
http://phpsec.org/projects/phpsecinfo/
```

在你的服务器上运行时，此工具会测试若干可能影响安全性的问题。图 5-11 显示了其中一种警告的示例。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_171_0.png)

**图 5-11：** PhpSecInfo 工具生成的警告

此警告以红色显示。各种警告和错误都进行了颜色编码。这个特定的错误告诉你 `force_redirect` 指令已被禁用。注意右下角的“更多信息”链接，它提供了有关此警告的详细说明。

报告底部是测试结果摘要，如图 5-12 所示。其中显示运行了 18 项测试，并给出 10 条提示，意味着需要关注。还产生了 2 个标记为严重的问题。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_171_1.png)

**图 5-12：** 测试结果摘要

无论你的服务器投入生产多久，都应该运行此工具。你可能会发现存在许多漏洞。务必在任何升级之后，或发生任何事件之后运行它。

### php.ini

使用 suPHP 时，你可以在大多数网站的根目录中找到一个名为 `php.ini` 的文件。此文件允许你向 PHP 解释器发出命令。如前所述，你可以使用此文件代替 `/etc/php.ini` 文件。请向你的主机商确认服务器正在运行 suPHP。

使用 WinSCP 找到 `/etc/php.ini` 文件。如果该文件不存在于此目录中，它也可能存在于你的 `public_html` 网站目录中。

