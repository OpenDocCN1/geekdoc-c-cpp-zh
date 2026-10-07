
```sql
SELECT

SecurityLabelID,

SecurityLabelName,

AuthSecurityProviderID,

AuthInit,

RoleSecurityProviderID,

RoleInit,

DefaultLabel

FROM

SecurityLabels

WHERE

SecurityLabelName = 'K2'
```

## 第 17 章：管理和创建安全提供程序

存储在 `RoleInit` 列中的 XML 数据摘要如下：

```xml
<roleprovider>
<init>ADCache=10;LDAPPath=//:LDAP://DC=DENALLIX;DC=COM;ResolveNestedGroups=False;IgnoreForeignPrincipals=False;IgnoreUserGroups=False;MultiDomainPath=False;DataSources&lt;DataSources&gt;DataSourcePath=LDAP://DC=DENALLIX;DC=COM* NetBiosName="DENALLIX*" &gt;&lt;DataSources&gt;</init>
...
</roleprovider>
```

ADUM 初始化设置列在 XML 文档的 `<init>` 节点中。这些设置在下表所示：

| 设置 | 定义 | 默认值 |
|---|---|---|
| ADCache | ADUM 维护一个从 AD 获取的用户和组数据缓存。此值控制值缓存的分钟数。 | 10 min |
| LDAPPath | 域的 LDAP 区分名称 (DN)，例如：LDAP=//DC=DENALLIX;DC=COM | 安装期间检测到的域 DN。 |
| ResolveNestedGroups | 此设置控制组在另一个组中引用的行为。如果此值为 false，则嵌套组内的用户将不会被解析。如果设置为 true，K2 将尝试解析所有嵌套组中的所有用户。如果启用此选项，K2 将跟踪循环组引用，以防陷入无限循环。 | False |
| IgnoreForeignPrincip | 外部主实体是对森林外部外部域中用户或组的引用，该域在森林内已建立信任关系。 | False |
| IgnoreUserGroups | 此设置引导 ADUM 解析用户可能所属的任何组。如果为 true，则不会对任何用户进行组解析。如果为 false，ADUM 将解析用户所属的组。 | False |

## 第四部分：K2 blackpearl 的管理（续接）

| 设置 | 定义 | 默认值 |
|---|---|---|
| MultiDomain | 此设置提醒 ADUM 此时它应该处理来自森林内多个域的用户和组。更多信息请参阅下一节。 | False |
| DataSources | 此 XML 文档包含 ADUM 用于解析用户和组的每个域的数据源。例如： 
```xml
<DataSources>
  <DataSource
    Path="LDAP://DC=DENALLIX,DC=COM"
    NetBiosName="DENALLIX*"
</DataSources>
``` | Path 和 NetBiosName 均设置为 K2 blackpearl 安装期间检测到的域值。 |

> 如果错误地修改 HostServer 数据库，可能会导致 K2 blackpearl 出现严重问题。在应用配置更改之前，请反复检查，并确保已备份数据库以及配置文件。在部署到生产系统之前，请务必在开发环境中测试新的配置设置。

修改 ADUM 配置设置的最常见场景是为其他域添加额外的支持。下一节将引导您完成添加额外域的过程，这将允许该域内的用户能够与 K2 工作流进行交互并参与其中。

## 配置对多个域的支持

根据上述的 ADUM 配置设置，可以配置 K2 blackpearl 使用森林内的多个域来解析用户和组。此外，还可以配置 ADUM 解析来自具有单向或双向信任的森林外部的用户和角色。

除了更改 K2 Workspace 配置外，`Rolelet` 列中 `init` 节点get两个配置设置也需要修改。

应当记录良好的 `MultiDomain` 属性应设置为 True。此外，应在 `DataSources` XML 文档中添加一个新的 `DataSources` 节点，定义要添加域的 `Path` 和 `NetBiosName`。

HostServer 数据库中还有一列需要更新；`AuthAuth` 列包含 K2 用于身份验证用户的域列表。

## 第 17 章：管理和创建提供程序

以下是一个 SQL 脚本示例，该脚本将更新所有相关字段，为 DENALLIX 域作为 CENTRAL-DLX 域添加多域支持。请确保从您的环境中提取当前设置，然后合并后续示例中用**粗体/斜体**标记的更改。

```sql
USE [HostServer]
UPDATE
[SecurityLabels]
SET
AuthInit =
<AuthInit>
<Domain>DENALLIX</Domain>
<Domain>CENTRAL-DLX</Domain>
</AuthInit>
RoleInit =
<roleprovider>
<addACacheSize=10;LDAPPath=LDAP://DC=DENALLIX,DC=COM;ResolvedNextGroups TrueBaseSearch=False;UserPrincipals=False;UserGroups=MultiDomain TrueAttributes=alt;DataSource Path=LDAP://DC=DENALLIX,DC=COM BaseName=DENALLIX&amp;gt;DataSource Path=LDAP://DC=CENTRAL-DLX BaseName=DENALLIX,DC=COM&amp;gt;DataSources&amp;gt;&lt;/provider>
<login />
<implementation assembly="ADUM, Version=4.0.0.0, Culture=neutral, PublicKeyToken=16a2c5aaaalib130d" type="ADUM.K2UserManager" />
<properties>
<user>
<property name="Name" type="String" />
<property name="Description" type="String" />
<property name="Email" type="String" />
<property name="Manager" type="String" />
<property name="Sip" type="String" />
<property name="ObjectID" type="String" />
</user>
<group>
<property name="Name" type="String" />
<property name="Description" type="String" />
</group>
</properties>
</roleprovider>
WHERE SecurityLabel = 'K2'
```

在更新了 SecurityLabels 表后，最后一个需要配置的区域是 K2 Workspace。该文件位于 `K2 Install\Workspace`。

在 `web.config` 的连接设置中，添加以下内容：

```xml
<add name="CNTRLDX" connectionString="LDAP://DC=DENALLIX,DC=COM" />
```

## 第四部分：K2 blackpearl 的管理（续）

最后，在成员部分使用上一步连接的新提供程序，请注意示例中的**粗体/斜体**文本。

```xml
<add name="CNTRX-AD"
  connectionProtection="Secure"
  enablePasswordReset="false"
  enableSearchMethods="true"
  requireQuestionOnAnswer="false"
  description="Central DLX connection"
  requiresEmail="false"
  clientSearchTimeout="30"
  attributeMapName="sAMAccountName"
  name="AspNetDirectoryMembershipProvider,CentralDLX"
  type="System.Web.Security.ActiveDirectoryMembershipProvider,System.Web,Version=2.0.0.0,Culture=neutral,PublicKeyToken=b0f5f7f5d0a3a" />
```

此过程可以根据需要重复 K2 中的任何域。

## 安全提供程序 API

并不是每个组织都使用 Active Directory，也不是每个组织都使用 SQL Server，因此强制其中之一可能是限制性的。这留下了第三种选择——开发自己的安全提供程序，以使用企业现有的身份验证和授权机制。K2 blackpearl 提供了插件架构，可以添加或替换当前的身份验证和授权提供程序。可能您的组织使用 Active Directory 并依赖 ADUM，但某些业务需求要求您允许合作伙伴访问 K2 ——在这种情况下，添加额外的安全提供程序非常有意义。K2 工作流允许混合使用来自多个安全提供程序的用户，从而充分利用工作流引擎。

本节将介绍构建这些插件化安全提供程序所需的 K2 blackpearl API。

## 第 17 章：管理和创建安全提供者

## 安全提供者对象模型

K2 blackpearl Host Server 是托管所有 K2 服务的核心服务器，它具有可扩展的架构，允许插件式组件。为了让对象被 Host Server 加载并识别作为安全提供者使用，它必须实现 `IHostableSecurityProvider` 接口。该接口基于其他三个接口构建：`IHostableType` 接口、`IAuthenticationProvider` 和 `IRoleProvider` 接口。

所有由 Host Server 加载的插件组件都必须实现 `IHostableType` 接口。Host Server 将动态加载、初始化和卸载实现 `IHostableType` 接口的对象。

此外，所有 K2 安全提供者都需要两个接口才能运行：一个通过 `IAuthenticationProvider` 进行认证，另一个通过 `IRoleProvider` 接口处理用户和角色功能。在实现这些时，还需要实现表示自定义安全提供者的用户和组的额外接口——稍后会详细介绍。

这三个接口（`IHostableType`、`IAuthenticationProvider` 和 `IRoleProvider`）都被 `IHostableSecurityProvider` 接口继承。为了创建自定义安全提供者，必须实现这个主接口 `IHostableSecurityProvider`，因此理解每个接口的功能及其关系至关重要。请花一点时间研究图 17-1 所示，以理解这些关系。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_651_0.png)

图 17-1

注意方法接口名称之间存在重叠，例如 `Init()` 和 `Login()` 方法。这可能会导致最初的困惑，但在这些多个接口上重复功能是有充分理由的。例如，需要三个不同的 `Init()` 方法——每个接口一个。这是因为 `IAuthenticationProvider` 和 `IRoleProvider` 是分别实例化的。

## 第四部分：K2 pearl 的管理

`IAuthenticationProvider` 和 `IRoleProvider` 由 Host Server 分别实例化，这意味着它们共享相同的类定义，并在内存中作为单独的对象实例进行初始化。这就是为什么每个接口都有一个 `Init()` 方法。如果 `IAuthenticationProvider` 和 `IRoleProvider` 之间有类似的初始化需求，则必须在每个 `Init()` 方法中重复代码。`IHostableType.Init()` 方法为 `IRoleProvider` 或 `IAuthenticationProvider` 可用。

尽管 `IAuthenticationProvider` 和 `IRoleProvider` 被合并到最终的 `IHostSecurityProvider` 中，但最终这两个接口并不需要都实现。额外的提供者可以混合使用。根据安全提供者配置的处理方式以及每个提供者单独实例化的方式，它们具有了一定的灵活性，允许它们完全解耦。例如，如果构建一个 `IIdentityProvider`，则不需要实现任何接口；它们可以抛出 `NotImplementedException`。这也是为什么 `Login()` 方法同时在 `IRoleProvider` 和 `IIdentityProvider` 接口上定义的原因。每个提供者都可以解耦，它们可以使用完全不同的机制进行登录以检索组或身份验证用户。也可能只需要一个提供者；例如，在某些情况下，可能只需要 `IAuthenticationProvider` 而不需要 `IRoleProvider`。

## 插件式架构

定义了对象模型后，Host Server 必须有一种动态加载和初始化安全提供者的方法。它在对象模型定义的接口上采用了插件架构，并结合 HostServer 数据库中的配置设置。安全提供者的实际安装将在本章后部分详细介绍；本节将尝试勾勒其架构。

有一个初始事件会触发 Host Server 加载安全提供者。通过将包含特定对象类型的程序集放入 K2 服务器的 `securityproviders` 文件夹，当 K2 服务启动时，它会轮询包含 `IHostSecurityProvider` 类型的程序集。一旦文件被 Host Server 加载，它将通过向数据库插入新行来记录新的安全提供者。下一步也是最后一步是手动的——需要更新数据库数据，为安全提供者提供一个友好的名称（称为安全标签 label），并为 `IAuthenticationProvider` 和 `IRoleProvider` 提供配置数据。

HostServer 数据库中用于构建安全提供者的两个表是图 17-2 所示的 `SecurityLabels` 和 `SecurityProvider` 表。`SecurityLabels` 表存储了每个安全提供者的记录。

## 第 17 章：管理和创建安全提供者

| PK SecurityLabelID | SecurityProvider |
| :--- | :--- |
| FK1 SecurityLabelName | SecurityProviderID |
| AuthSecurityProviderID | ProviderClassName |
| RoleSecurityProviderID | |
| DefaultLabel | | |
| FK2 SecurityProviderID | |

图 17-2

根据图 17-2 中定义的表关系，安全提供者被定义为唯一的安全标签，具有一个认证提供者类和一个角色安全提供者类，以及每个相应的初始化数据。

第一个字段是 `SecurityLabelName`，它是 K2 pearl 用于识别安全提供者的友好名称。例如，`K2` 是 Active Directory 提供者的标签，而 `K2SQL` 用于 K2 SQL 角色。因此，为了让 K2 识别用户，它会将安全标签与用户名组合，并用逗号分隔。例如，为了让 K2 识别名为 DENALLIX AD 的 Active Directory 域中的 Administrator，用户名将表示为 `K2:DENALLIX\Administrator`。

接下来是 `AuthSecurityProviderID` 列。它是 `SecurityProvider` 表中 `SecurityProviderID` 的外键。

`AuthInit` 字段结合 `SecurityProviderID` 为 Host Server 提供了启动时初始化 `IAuthenticationProvider` 所的信息。同样，`RoleInit` 字段结合 `SecurityProviderID` 为 Host Server 提供了初始化 `IRoleProvider` 所的信息。

```xml
<AuthInit>
  <Domain>DENALLIX</Domain>
</AuthInit>
```
