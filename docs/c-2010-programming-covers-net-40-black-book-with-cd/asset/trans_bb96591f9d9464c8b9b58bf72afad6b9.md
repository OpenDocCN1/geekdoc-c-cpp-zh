

## 程序集信息文件

你已经了解了程序集的清单，它是任何程序集最重要的组件。现在让我们看看清单从哪里获取大部分信息。每个使用 Visual C# 创建的项目都有一个 AssemblyInfo.cs 文件，其中包含大量配置属性和其他信息，例如公司名称、版本、商标信息和程序集名称。程序集信息文件使用这些配置属性为程序集分配强名称密钥并指定其他信息，例如公司名称、版本和程序集名称。

清单 33.1 显示了应用程序的 AssemblyInfo.cs 文件的代码：

### Listing 33.1: Showing the Code of the Assembly Information File

```
```csharp
...
[assembly: AssemblyKeyFile("Akey.snk")]
[assembly: AssemblyTitle("SharedObject")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("Kogent Solutions Inc")]
[assembly: AssemblyProduct("SharedObject")]
[assembly: AssemblyCopyright("Copyright © Kogent Solutions Inc 2010")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]

// Major Version
// Minor Version
// Build Number
// Revision
...
[assembly: AssemblyVersion("1.0.0.0")]
...
```
```

## Version Format

AssemblyInfo.cs 文件包含一个注释，指定了程序集版本的格式。以下语法显示了程序集版本的格式：

```
```text
<Major Version>.<Minor Version>.<Build Number>.<Revision>
```
```

在前面的语法中，如果对程序集所做的更改不是重大的，则版本号和修订号会发生变化。重大更改，例如删除或更改功能导致程序集与旧版本不兼容，可以通过更改主版本号来体现。版本信息由 AssemblyVersion 属性指定，如清单 33.1 所示。

## Configuration Files for Assemblies

你可以在不重新构建客户端的情况下将客户端重定向到程序集的新版本。但是，你必须首先在 .NET Framework 2.0 配置工具中配置客户端。.NET Framework 2.0 配置工具在我们通过它配置客户端时创建一个扩展名为 .exe.config 的配置文件。此配置文件包含代码，指示客户端被重定向到当前程序集的新版本，如清单 33.2 所示：

### Listing 33.2: Showing the Code of the Configuration Files for Assemblies

```
```xml
<?xml version="1.0"?>
<configuration>
    ......
        <bindingRedirect oldVersion="1.0.0.0" newVersion="1.1.0.0" />
    ......
```
```

```
</runtime>
</configuration>
```

清单 33.2 中突出显示的部分显示了你在配置客户端使用程序集新版本时输入的值。

除了使用 .NET Framework 2.0 配置工具创建的配置文件外，我们还有另外两种类型的配置文件；机器配置和发布者策略。机器配置文件用于设置对所有应用程序通用的系统范围信息。这些文件位于 <WinDrive>:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG\，名称为 machine.config。

另一种类型的配置文件是发布者策略文件。要理解其用途，请考虑这样一种情况：你希望将使用特定版本共享程序集的客户端重定向到共享程序集的新版本。我们可以使用 .NET Framework 2.0 配置工具并将客户端重定向到共享程序集的新版本。但是，想象一下当有太多客户端需要配置的情况；或者更糟的是，你根本不知道有多少客户端在使用旧版本。在这种情况下，你需要使用发布者策略文件。发布者策略文件包含系统范围的策略，确保请求特定版本程序集的所有应用程序都被重定向到指定的程序集新版本。但是，你需要在中央位置存储此类策略，以便每个客户端都能够使用它。我们知道所有客户端都会在 GAC 中查找共享程序集；因此，发布者策略文件可以放置在 GAC 中。

在程序集的新版本创建并在配置文件中提及后，CLR 会尝试借助以下两个属性找到程序集：

- codebase
- probing

让我们详细讨论这些属性。

### codebase

codebase 属性用于在特定网络上定位程序集，而不是在本地 GAC 中定位它。你可以在应用程序配置文件中设置 <codeBase> 属性，如清单 33.3 所示：

### Listing 33.3: Showing the Code for Setting the Codebase Attribute

```
...
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
  <dependentAssembly>
    <assemblyIdentity name="Sharedobject" publicKeyToken="deeb33795f7d292a"/>
    <codeBase version="2.0" href="file:///C:/NewGAC" />
  </dependentAssembly>
</assemblyBinding>
...
```

如果你的程序集已签名，你可以指定 Internet 上的任何位置（以 URL 形式，例如 http://localhost/shared.dll）或本地网络。但是，对于未签名的程序集，指定的路径必须相对于应用程序目录。

> NOTE
> 如果在应用程序配置文件中找到 codebase 属性，则程序集将在运行时从其中指定的位置加载。如果应用程序无法从 codebase 属性中指定的位置加载程序集，则加载过程被视为失败。

### probing

私有程序集始终位于应用程序目录中（有一些例外，即支持不同程序集文化的程序集）。如果需要将程序集放置在应用程序文件夹的子文件夹中，可以使用 probing 属性设置应用程序在这些子文件夹中查找程序集。清单 33.4 显示了在应用程序配置文件中设置 probing 属性的简单任务：

### Listing 33.4: Showing the Code for Setting the Probing Attribute

```
...
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
  <publisherPolicy apply="yes" />
  <probing privatePath="SubDir" />
</assemblyBinding>
...
```

在清单 33.4 中，应用程序被配置为在 bin\Debug 文件夹中的名为 SubDir 的子文件夹中查找引用的程序集。

现在让我们在 Immediate Solutions 部分学习如何使用程序集。

## Immediate Solutions

### Creating a Shared Assembly

要创建共享程序集，首先需要创建一个名为 SharedObject 的类库，以及一个名为 ASimpleClient 的 Windows 应用程序（也可在 CD-ROM 上获得）。尽管应用程序 ASimpleClient 本身就是一个程序集，但本节主要关注 SharedObject 类库，以了解与程序集相关的概念。

执行以下步骤创建 SharedObject 类库：

- 1. 打开 Microsoft Visual Studio 2010 并从主菜单中选择 New→Project。这将打开一个 New Project 对话框。
- 2. 从模板列表中选择 Class Library 模板（图 33.4）。
- 3. 在 Name 文本框中输入应用程序的名称 SharedObject，并在 Location 下拉框中输入应用程序的位置（图 33.4）。
- 4. 将应用程序的目标框架选择为 .NET Framework 2.0，如图 33.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1590_0.png)

Figure 33.4: Creating the SharedObject Class Library

- 5. 单击 OK 按钮关闭 New Project 对话框。这将创建 SharedObject 类库。
- 6. 打开 SharedObject 类库的 Class1.cs 文件并用清单 33.5 所示的代码替换现有代码：

### Listing 33.5: Showing the Code for Creating a Shared Assembly

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace SharedObject
{
    public class SharedObject
    {
        public string Greeting(string name)
        {
```

