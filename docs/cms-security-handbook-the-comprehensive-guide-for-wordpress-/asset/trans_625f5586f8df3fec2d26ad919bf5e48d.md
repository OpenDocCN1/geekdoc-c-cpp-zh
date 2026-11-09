

## 1xx 系列

此类状态码表示临时响应，仅由状态行和可选头组成，并以空行结束。

以下是该系列中的具体代码：

- 100 继续 — `HTTP_CONTINUE`
- 101 切换协议 — `HTTP_SWITCHING_PROTOCOLS`
- 102 处理中 — `HTTP_PROCESSING`

## 2xx 系列

此类状态码表示操作已被成功接收、理解和接受。

以下是该系列中的具体代码：

- 200 正常 — `HTTP_OK`
- 201 已创建 — `HTTP_CREATED`
- 202 已接受 — `HTTP_ACCEPTED`
- 203 非授权信息 — `HTTP_NON_AUTHORITATIVE`
- 204 无内容 — `HTTP_NO_CONTENT`
- 205 重置内容 — `HTTP_RESET_CONTENT`
- 206 部分内容 — `HTTP_PARTIAL_CONTENT`
- 207 多状态 — `HTTP_MULTI_STATUS`

## 3xx 系列

此系列中的代码表示用户代理需要采取进一步操作才能完成请求。如果（且仅当）第二个请求中使用的方法是 GET 或 HEAD，则所需操作可由用户代理在不与用户交互的情况下执行。用户代理不应自动重定向请求超过五次，因为此类重定向通常表示无限循环。

以下是该系列中的具体代码：

- 300 多种选择 — `HTTP_MULTIPLE_CHOICES`
- 301 永久移动 — `HTTP_MOVED_PERMANENTLY`
- 302 已找到 — `HTTP_MOVED_TEMPORARILY`
- 303 参见其他 — `HTTP_SEE_OTHER`
- 304 未修改 — `HTTP_NOT_MODIFIED`
- 305 使用代理 — `HTTP_USE_PROXY`
- 306 未使用 — `UNUSED`
- 307 临时重定向 — `HTTP_TEMPORARY_REDIRECT`

## 4xx 系列

此系列中的代码表示请求包含错误语法或无法完成。这些代码表示客户端似乎出错的情况。除响应 HEAD 请求外，服务器应包含一个实体，其中说明错误情况，以及该情况是临时还是永久。

以下是该系列中的具体代码：

- 400 错误请求 — `HTTP_BAD_REQUEST`
- 401 需要授权 — `HTTP_UNAUTHORIZED`
- 402 需要付款 — `HTTP_PAYMENT_REQUIRED`
- 403 禁止 — `HTTP_FORBIDDEN`
- 404 未找到 — `HTTP_NOT_FOUND`
- 405 方法不允许 — `HTTP_METHOD_NOT_ALLOWED`
- 406 不可接受 — `HTTP_NOT_ACCEPTABLE`
- 407 需要代理认证 — `HTTP_PROXY_AUTHENTICATION_REQUIRED`
- 408 请求超时 — `HTTP_REQUEST_TIME_OUT`
- 409 冲突 — `HTTP_CONFLICT`
- 410 已失效 — `HTTP_GONE`
- 411 需要长度 — `HTTP_LENGTH_REQUIRED`
- 412 前提条件失败 — `HTTP_PRECONDITION_FAILED`
- 413 请求实体过大 — `HTTP_REQUEST_ENTITY_TOO_LARGE`
- 414 请求 URI 过长 — `HTTP_REQUEST_URI_TOO_LARGE`
- 415 不支持的媒体类型 — `HTTP_UNSUPPORTED_MEDIA_TYPE`
- 416 请求范围无法满足 — `HTTP_RANGE_NOT_SATISFIABLE`
- 417 期望失败 — `HTTP_EXPECTATION_FAILED`
- 418 我是茶壶 — `UNUSED`
- 419 未使用 — `UNUSED`
- 420 未使用 — `UNUSED`
- 421 未使用 — `UNUSED`

WordPress 用户应访问 http://perishablepress.com/press/tag/security/ 查看各种 .htaccess 示例。Joomla! 用户应访问 http://snipt.net/nikosdion/the-master-htaccess/ 了解使用 .htaccess 更好地保护 Joomla! 站点的具体方法。

### 阻止 IP 地址

以下示例展示如何阻止 IP 地址访问您的站点：

```apache
<Limit GET POST PUT>
  Order Allow,Deny
  Allow from all
  Deny from xxx.xxx.xxx.xxx
  Deny from xxx.xxx.xxx.xxx
  Deny from xxx.xxx.xxx.xxx
  Deny from xxx.xxx.xxx.xxx
  Deny from xxx.xxx.xxx.xxx
</Limit>
```

### 阻止恶意机器人

恶意机器人是一类攻击网站的恶意软件。这些恶意程序要么闯入系统，要么收集用于闯入的信息。阻止它们是常规且频繁的任务。幸运的是，.htaccess 提供了一种简单的方法来实现。有关在 .htaccess 中阻止恶意机器人的良好示例，请参见 http://perishablepress.com/press/2010/06/09/2010-user-agent-blacklist，并复制 2010 用户代理黑名单中的指令。

### 保护特定文件

以下示例保护特定文件免遭除您的 IP 之外的所有访问者访问：

```apache
# Block all visitors except your IP or IPs
<Limit GET POST>
  Order Deny,Allow
  Deny from all
  Allow from first ip address
  Allow from second ip address
</Limit>
ErrorDocument 403 path/custom-message.html
<Files path/custom-message.html>
  Order Allow,Deny
  Allow from all
</Files>
```

### 在您的站点上要求 SSL

以下示例展示如何在您的站点上要求 SSL：

```apache
SSLOptions +StrictRequire
SSLRequireSSL
SSLRequire %{HTTP_HOST} eq "domain.tld"
ErrorDocument 403 https://domain.tld

# require SSL without mod_ssl
RewriteCond %{HTTPS} !=on [NC]
RewriteRule ^.*$ https://%{SERVER_NAME}%{REQUEST_URI} [R,L]
```

### 在您的站点上部署自定义错误页面

复制以下模式以提供您自己的一组自定义错误页面。只需将 /errors/###.html 替换为正确的路径和文件名。还要更改路径前的 ###，以调用其他错误的页面。

> **注意** 您的自定义错误页面大小必须大于 512 字节，否则 Internet Explorer 将完全忽略它们。

使用以下内容提供自定义错误页面：

```apache
ErrorDocument 400 /errors/400.html
ErrorDocument 401 /errors/401.html
ErrorDocument 403 /errors/403.html
ErrorDocument 404 /errors/404.html
ErrorDocument 500 /errors/500.html
```

### 提供通用错误文档

使用以下内容提供通用错误文档：

```apache
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^.*$ /dir/error.php [L]
```

### 禁用服务器签名

使用以下内容禁用服务器签名：

```apache
ServerSignature Off
```

### 将服务器请求方法限制为 GET 和 PUT

使用以下内容将服务器请求方法限制为 GET 和 PUT：

```apache
Options -ExecCGI -Indexes -All
RewriteEngine on
RewriteCond %{REQUEST_METHOD} ^(TRACE|TRACK|OPTIONS|HEAD)
RewriteRule ^.* - [F]
```

## 缩略语和术语

表 B-1 提供了常见安全缩略语的列表。

| 缩略语 | 含义 |
|---|---|
| APF | 高级策略防火墙 |
| AES | 高级加密标准 |
| ACL | 访问控制列表 |
| ASP | 动态服务器页面 |
| BIOS | 基本输入/输出系统 |
| BSIG | 蓝牙技术联盟 |
| CGI | 通用网关接口 |
| CISSP | 认证信息系统安全专家 |
| CISO | 首席信息安全官 |
| CISP | 持卡人信息安全计划 |
| CLI | 命令行解释器 |
| CMS | 内容管理系统 |
| CoLo | 主机托管设施 |
| CSU/DSU | 通道服务单元/数据服务单元 |
| DCE | 数据通信设备 |
| DDoS | 分布式拒绝服务（攻击） |
| DES | 数据加密标准 |
| DHCP | 动态主机配置协议 |
| FDDI | 光纤分布式数据接口 |
| FTP | 文件传输协议（应用层） |
| GBIC | 千兆接口转换器 |
| Gbps | 千兆比特每秒 |
| HTML | 超文本标记语言 |
| IANA | 互联网号码分配机构组织 |
| ICMP | 互联网控制消息协议 |
| IMAP | 互联网消息访问协议 |
| IOS | 互联网络操作系统 |
| IP | 互联网协议（互联网层） |
| IP Address | 互联网协议地址 |
| IPS | 入侵防御系统 |
| IRC | 互联网中继聊天 |
| ISDN | 综合业务数字网络 |
| ISP | 互联网服务提供商 |
| JAXP | 用于 XML 解析的 Java API |
| JDBC | Java 数据库连接 |
| JDK | Java 开发工具包 |
| Kbps | 千比特每秒 |
| LAN | 局域网 |
| LDAP | 轻量级目录访问协议 |
| LLC | 逻辑链路控制 |
| MAC | 媒体访问控制 |
| MAN | 城域 |

