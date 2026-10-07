
# 单点登录 (SSO)

在涵盖了基础安全 API 之后，K2 blackpearl 安全框架中另一个值得提及的功能是单点登录 (SSO)。K2 blackpearl 提供了一个 API，允许从任何客户端（本地或通过网络远程）查询安全提供程序。添加 `SourceCode.Security.UserRoleManager.Client.dll` 程序集的引用将提供对 `UserRoleManagerServer` 对象的访问，该对象提供了访问 K2 blackpearl 服务器上所有安全提供程序的接口。

`UserRoleManagerServer` 对象包含的所有方法与 `IRoleProvider` 接口上的方法完全镜像。区别在于 `UserRoleManagerServer` 与所使用的安全提供程序无关，这意味着你可以通过提供安全标签来查询任何已安装的安全提供程序。凭据是王国之钥，它们是安全的。一旦缓存，所有后续请求 K2 blackpearl 都会使用加密来保护这些凭据并防止特定系统的缓存。为 K2 blackpearl 版本计划的额外功能将允许用户或管理员选择凭据。目前章节正在编写中，SSO 功能仅适用于 SmartObjects。未来，SSO 功能将适用于所有 K2 组件。

## 第四部分：K2 blackpearl 的管理

下表记录了 `UserRoleManagerServer` 的方法：

| 方法 | 说明 |
| --- | --- |
| FindGroups | 重载。在指定安全标签的安全提供程序上调用 `IRoleProvider.FindGroups()`。 |
| FindUsers | 重载。在指定安全标签的安全提供程序上调用 `IRoleProvider.FindUsers()`。 |
| FormatItemName | 在指定安全标签的安全提供程序上调用 `IRoleProvider.FormatItemName()`。 |
| GetDefaultLabelName | 通过查询 `[DefaultLabel]` 设置为 1 的 `[Labels]` 表来检索默认安全标签名称。 |
| GetGroup | 重载。在指定安全标签的安全提供程序上调用 `IRoleProvider.GetGroup()`。 |
| GetLabelProvider | 返回一个包含提供程序名称的字符串数组。 |
| GetLabels | 返回包含 Host Server 中所有注册安全标签的字符串数组。 |
| GetUser | 重载。在指定安全标签的安全提供程序上调用 `IRoleProvider.GetUser()`。 |
| QueryGroupProperties | 在指定安全标签的安全提供程序上调用 `IRoleProvider.QueryGroupProperties()`。 |
| QueryUserProperties | 在指定安全标签的安全提供程序上调用 `IRoleProvider.QueryUserProperties()`。 |
| ResolveQueue | 重载。这些方法主要用于支持使用目标队列的迁移或升级的 K2.net 2003 进程。 |

## 第 17 章：管理和创建安全提供程序

在新创建的自定义安全提供程序项目中添加四个类文件。命名如下如下：

- `CustomSecurityProvider.IAuthenticationProvider.cs`
- `CustomSecurityProvider.IostableSecurityProvider.cs`
- `CustomSecurityProvider.IostableType.cs`
- `CustomSecurityProvider.IRoleProvider.cs`

然后，打开每个文件并更改类声明：

```
class CustomSecurityProvider
```

更改为：

```
partial class CustomSecurityProvider
```

然后，对于每个文件，实现文件名中对应接口的骨架接口；例如，要向 `CustomSecurityProvider.IAuthenticationProvider.cs` 文件添加 `IAuthenticationProvider` 接口，请在 Visual Studio 中打开它并将其从：

```
partial class CustomSecurityProvider
```

更改为：

```
public partial class CustomSecurityProvider : IAuthenticationProvider
```

然后，点击 `IAuthenticationProvider` 接口上的智能标签（Smart Tag），并选择显式实现接口 'IAuthenticationProvider'（如图 17-7 所示）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_677_0.png)

这将自动补全所有所需的 `IAuthenticationProvider` 接口要求。对每个接口重复这些步骤。

为了简单起见，对于具有重叠方法名的接口，你可以选择“显式实现接口...”选项。实际上，只有两个方法需要显式实现：`IAuthenticationProvider.Init()` 和 `IRoleProvider.Init()`。最后，一旦创建了所有部分类并生成了骨架方法，只需要 `CustomSecurityProvider.IostableSecurityProvider.cs` 类，其他部分类上的接口可以删除。

### 安装自定义安全提供程序

一旦所有骨架方法就绪，就可以安装自定义提供程序并开始调试，尽管在没有实现所有方法的情况下，可能会看到来自 K2 Host 服务器的错误。不要在生产服务器上安装不可信任的提供程序，因为提供程序的任何问题都会影响 K2 Host 服务器的可用性。

以下是安装和配置新安全提供程序的流程概述：

1. 准备安全提供程序依赖项。
2. 准备主机服务器配置设置。
3. 安装安全提供程序库。
4. 配置安全提供程序。
5. 调试安全提供程序。
6. 测试安全提供程序。现在，让我们深入查看这六个阶段。

### 准备提供程序依赖项和配置

如果自定义安全提供程序有任何依赖项，必须在将安全提供程序库集成到主机服务器之前进行部署和配置。例如，如果自定义安全提供程序需要创建数据库并填充数据，请确保先执行此操作。

在设置并配置所有外部依赖后，停止 K2 blackpearl 服务。

### 准备主机服务器配置设置

服务停止后，需要安装自定义安全提供程序使用的任何 K2 blackpearl 特定配置设置，如果安全提供程序依赖于 `K2HostServer.config` 中 `configsettings` 部分的应用程序配置设置，或者它可能在 `connectionStrings` 部分中存储了数据库连接字符串。

### 安装安全提供程序库

在 K2 blackpearl 主机服务器中，有一个名为 `securityproviders` 的子文件夹。这是实现 `IHostableSecurityProvider` 接口的程序集存放的地方。停止 K2 blackpearl 后，将新的安全提供程序程序集复制到 `[K2 安装文件夹]\K2 blackpearl\Host Server\securityproviders` 文件夹中。确保复制自定义安全提供程序引用的未安装在 GAC 中的任何非 K2 程序集。

> 截至 K2 blackpearl 0807，所有程序集必须在主机服务器数据库中注册。更多信息请参见标题为“K2 blackpearl 0807 功能更改”的 KB00351。

以下是 0807 及更高版本在主机服务器数据库中注册程序集的步骤：

1. 使用 .NET Framework SDK 的强名称工具（Strong Name Utility）提取安全提供程序的公钥，例如：

```
sn.exe -Tp MySecurityProvider.dll
```

输出将类似于：

```
Microsoft (R) .NET Framework Strong Name Utility Version 3.5.30729.1

Copyright (c) Microsoft Corporation. All rights reserved.

Public key is
02400004800009400000060200000240000253141000040000100fb82d9369241be803
1262893716eaefb53661147a2ac2d2c4225956c7b398a715fd3903f680cd88e244460429caff1
54ae53922b9920498da6e1231b10c2d38915ecb0d14a812fc4ec78ec5c3ac916880382a4dce3a4126
0d28742515b5d967c2f96f5b11bc0bd116bcdf397bf22302dab49d373841f2381f484

Public key token is 9460afc2dd1b7
```

2. 使用 SQL 命令将安全提供程序添加到 HostServer 数据库，将 `SecurityProvider.dll` 替换为你的安全提供程序 dll 的实际程序集名称和公钥令牌

```
INSERT INTO [HostServer].[dbo].[AssemblyRegistration]
[AssemblyID],
[AssemblyName],
[PublicKeyToken],
[Enabled]
```

```
VALUES
(
newid(),
'SecurityProvider.dll',
'9460afc2dd1b7',
1
)
```

3. 确保在 `[K2 安装]\HostServer\bin\K2Server.config` 文件中按如下设置 `assemblyregistration` appSetting：

```
<appSettings>
...
<add key="useassemblyregistration" value="true" />
...
</appSettings>
```

4. 重启 K2 Server 服务。

### 配置安全提供程序

一旦复制了安全提供程序库并设置了配置设置，重启 K2 blackpearl 服务。在启动时，K2 服务器会轮询安全提供程序文件夹。如果服务器发现实现 `IHostableSecurityProvider` 接口对象的程序集，主机将在 `SecurityProviders` 表中插入新记录。

要将安全提供程序集成到 K2，需要更新 HostServer 数据库中的标签名称以及初始化数据（`AuthInit` `RoleInit`）。在运行脚本之前，确保给服务器留一点时间记录新的安全提供程序；如果由于某些原因 K2 服务器未检测到新提供程序，或者它没有足够的时间添加记录，脚本将失败。

### 第四部分：K2 blackpearl 管理

可以修改以下示例 SQL 脚本向 HostServer 数据库添加新的安全标签：

```sql
declare @securityProviderName varchar(255)
declare @securityLabel varchar(255)
declare @authProviderID uniqueidentifier
declare @securityProviderID uniqueidentifier
declare @securityLabelID uniqueidentifier
declare @authInit xml
declare @roleInit xml
declare @defaultLabel bit
```

```sql
USE [HostServer]
-- 这是将在 K2 工作区看到的安全标签
SET @securityLabel = '自定义标签'
-- 这是提供程序的类名
SET @securityProviderName = 'Custom.Auth.Provider'
-- 生成一个新的 GUID
SET @securityLabelID = newid()
-- 初始化身份验证程序的 AuthInit XML 文
SET @authInit = '<authInit />'
-- 初始化角色程序的 RoleInit XML 文
SET @roleInit = '<roleProvider></roleProvider>'
-- 这不是系统默认标签
SET @defaultLabel = 0
-- 提取新添加的身份验证安全提供程序的 ID
SELECT
@authProviderID = [SecurityProviderID]
FROM
[SecurityProviders]
WHERE
[ProviderClassName] = @securityProviderName
-- 提取新添加的角色安全提供程序的 ID
SELECT
@securityProviderID = [SecurityProviderID]
FROM
[SecurityProviders]
WHERE
[ProviderClassName] = @securityProviderName
```

#### 第17 章：管理和创建安全提供者

##### 将 SecurityProvider 链接到新的 Security Label
```sql
INSERT INTO [SecurityLabels]
(
  [SecurityLabelID,
  [SecurityLabelName,
  [AuthSecurityProviderID,
  [AuthInit,
  [RoleProviderID,
  [RoleInit,
  [DefaultLabel
)
(
  @securityLabelID,
  @securityLabel,
  @providerID,
  @authInit,
  @roleProviderID,
  @roleInit,
  @defaultLabel
)
VALUES
```
