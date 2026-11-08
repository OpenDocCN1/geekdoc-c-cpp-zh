

## 认证、授权与计费框架

认证、授权与计费（AAA）是一种基于标准的框架，您可以实施该框架来控制允许谁访问网络（认证）、他们在网络上可以执行哪些操作（授权），以及审计他们在访问网络期间执行了哪些操作（计费）。

### 本地 AAA 认证

以下是配置 Cisco 路由器以支持本地 AAA 认证的一般步骤：

- 1. 在本地路由器数据库中添加用户名和密码。
- 2. 使用 `aaa new-model` 命令在路由器上全局启用 AAA。
- 3. 使用 `aaa authentication` 命令和指定的方法列表配置认证策略。
- 4.（可选）使用 `aaa authorization` 命令和指定的方法列表配置授权策略。
- 5.（可选）使用 `aaa accounting` 命令和指定的方法列表配置计费策略。
- 6. 确认并排查 AAA 配置问题。

> **注意** `aaa authentication` 命令的其他变体包括 `aaa authentication ppp`、`aaa authentication enable` 和 `aaa authentication dot1x`。

> **注意** 其他可配置参数包括 `aaa authentication banner`、`aaa authentication username-prompt`、`aaa authentication password-prompt` 和 `aaa authentication fail-message`。

```text
Router(config)#username                  | Add a username and password to the local
 username privilege level              | security database.
 secret password
Router(config)#aaa new-model             | Enable AAA.
```

![](img/0d9540c65a85f4cb1c32cee46038d8ab_101_0.png)

图 7-1  AAA 摘要界面

单击“启用 AAA”。

“启用 AAA”对话框出现，如图 7-2 所示。

单击“是”将启用 AAA，并自动在 console 线路上配置本地认证。它还会为 vty 线路配置本地认证、使用 EXEC shell 的授权，并接受用户的特权级别（如果已配置）。

> **注意** 单击**否**不会启用 AAA。

![](img/0d9540c65a85f4cb1c32cee46038d8ab_101_1.png)

图 7-2  “启用 AAA”对话框

### 基于服务器的 AAA 认证

在大型网络中为每台 Cisco 设备维护本地认证数据库并不可行。大型网络需要基于 AAA 服务器的解决方案。路由器与 AAA 服务器通信，这些服务器可以安装在 Windows 服务器或专用设备上，例如 Cisco 1121 安全访问控制系统（ACS）或 Cisco 身份服务引擎（ISE）。

当用户连接到路由器时，系统会提示他们输入用户名和密码。路由器将凭据传递给 Cisco Secure ACS（服务器或引擎）。Cisco Secure ACS 对用户进行认证。

### TACACS+ 与 RADIUS 对比

路由器使用 TACACS+ 或 RADIUS 协议与 AAA 服务器通信，以实现 AAA 功能：

|  | TACACS+ | RADIUS |
|---|---|---|
| **标准** | Cisco 专有 | RFC 2865、2866、2867 和 2868 |
| **传输协议** | TCP 端口 49 | UDP 端口 1645 或 1812 用于认证，UDP 端口 1646 或 1813 用于计费 |
| **机密性** | 加密整个数据包主体，但保留标准 TCP 报头 | 仅加密从客户端到服务器的 Access-Request 数据包中的密码 |
| **功能** | 使用 AAA 架构，将认证、授权和计费分离 | 将认证和授权合并 |
| **定制性** | 基于用户/组提供路由器命令的授权 | 可以将特权级别传递到路由器，供路由器本地用于命令授权 |
| **计费** | 捕获的信息有限 | 捕获更详细的信息 |
| **部署** | 常见于 Cisco 部署以及需要多协议支持的环境 | 在 VoIP 安装和支持 802.1x 的环境中很受欢迎 |

**注意：** 根据所选解决方案的不同，配置命令会略有差异。

**注意：** RADIUS 最终将被 DIAMETER 取代。

以下是配置 Cisco 路由器以支持基于服务器的认证的一般步骤：

- 1. 配置 AAA 服务器和服务器组。
- 2. 在路由器上全局启用 AAA。
- 3. 使用 `aaa authentication` 命令和指定的方法列表配置认证策略。
- 4.（可选）使用 `aaa authorization` 命令和指定的方法列表配置授权策略。
- 5.（可选）使用 `aaa accounting` 命令和指定的方法列表配置计费策略。
- 6. 确认并排查 AAA 配置问题。

### 配置基于服务器的 AAA 认证

配置基于服务器的认证的第一步是配置 AAA 服务器对象：

| 命令 | 描述 |
|---|---|
| `R1(config)#tacacs-server host`<br>`{host-name \| host-ip-address}`<br>`[key string] [port [integer]]`<br>`[single-connection] [timeout [seconds]]` | 指定 TACACS+ 主机。密钥、端口号、single-connection 和超时均为可选。<br><br>**注意：** 加密密钥可以使用 `tacacs-server key` 命令单独配置。<br><br>**提示：** 连接到 Cisco Secure ACS 时，请使用 single-connection 关键字。这更高效，因为它允许服务器处理更多数量的 TACACS 操作。超时指定了路由器在重新传输前等待服务器回复的时间。默认值为 5 秒。 |
| `R1(config)#radius-server host`<br>`{host-name \| host-ip-address}`<br>`[auth-port port-number] [acct-port port-number] [key password]` | 指定 RADIUS 主机。端口号和密钥是可选的。<br><br>**注意：** 如果未指定 auth-port 和 acct-port，则 auth-port 的默认值为 1645，acct-port 的默认值为 1646。<br><br>**注意：** 您可以使用 `radius-server key` 命令单独配置加密密钥。 |

可选地，可以将服务器分组。此功能允许您选择已配置服务器主机的一个子集，并将其用于特定服务：

| 命令 | 描述 |
|---|---|
| `Router(config)#aaa group server radius group-name` | 将现有 RADIUS 服务器主机分组，并将它们用于特定服务。 |
| `Router(config-sg-radius)#server ip-address {auth-port port-number} {acct-port port-number}` | 为组服务器配置 RADIUS 服务器的 IP 地址。 |
| `Router(config)#aaa group server tacacs+ group-name` | 将现有 TACACS+ 服务器主机分组，并将它们用于特定服务。 |
| `Router(config-sg-tacacs+)#server server-ip` | 为组服务器配置 TACACS+ 服务器的 IP 地址。**注意：** 您可以重复使用此命令将多台服务器添加到组中。 |

最后，配置登录认证方法列表以使用已标识的服务器：

| 命令 | 描述 |
|---|---|
| `Router(config)#aaa authentication login [default \| list-name] {method1 method2 ...}` | 定义访问线路时要使用的默认登录认证方法。基于服务器的可选方法包括：<br><br>- `group radius`<br>- `group tacacs+`<br>- `group group-name`<br><br>**注意：** 建议将本地路由器数据库添加为备用方法，以防与 AAA 服务器的通信失败。 |

### 配置基于服务器的 AAA 认证示例

配置 AAA 服务器的第一步是配置 AAA 服务器对象：

| 命令 | 描述 |
|---|---|
| `R1(config)#username ADMIN`<br>`privilege 15 secret cisco123` | 在本地数据库中创建一个条目。 |
| `R1(config)#aaa new-model` | 启用 AAA。 |
| `R1(config)#radius-server host 192.168.1.101 auth-port 1812 acct-port 1813 key cisco123` | 指定一台 RADIUS 服务器，并使用 UDP 端口号 1812 和 1813 以及密钥 cisco123。 |

