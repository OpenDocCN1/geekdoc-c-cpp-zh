
在第二章中仅讨论了 probing 元素的 privatePath 属性，本节我将讨论其他 XML 配置文件元素。下面是一个 XML 配置文件。

```xml
<?xml version="1.0"?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <probing privatePath="AuxFiles;bin\subdir" />

      <dependentAssembly>

        <assemblyIdentity name="SomeClassLibrary"
          publicKeyToken="32ab4ba45e0a69a1" culture="neutral"/>

        <bindingRedirect
          oldVersion="1.0.0.0" newVersion="2.0.0.0" />

        <codeBase version="2.0.0.0"
          href="http://www.Wintellect.com/SomeClassLibrary.dll" />

      </dependentAssembly>

      <dependentAssembly>

        <assemblyIdentity name="TypeLib"
          publicKeyToken="1f2e74e897abbcfe" culture="neutral"/>

        <bindingRedirect
          oldVersion="3.0.0.0-3.5.0.0" newVersion="4.0.0.0" />

        <publisherPolicy apply="no" />

      </dependentAssembly>

    </assemblyBinding>
  </runtime>
</configuration>
```

这个 XML 文件为 CLR 提供了大量信息。其含义如下：

- **probing 元素** 当试图查找弱命名程序集时，在应用程序基目录的 AuxFiles 和 bin\subdir 目录中查找。对于强命名程序集，CLR 会在 GAC 或 codeBase 元素指定的 URL 中查找。仅当未指定 codeBase 元素时，CLR 才会在应用程序的私有路径中查找强命名程序集。

- **第一个 dependentAssembly、assemblyIdentity 和 bindingRedirect 元素** 当试图定位由控制 32ab4ba45e0a69a1 公钥标记的组织发布的、区域性中立的 SomeClassLibrary 程序集的 1.0.0.0 版本时，改为定位同一程序集的 2.0.0.0 版本。

- **codeBase 元素** 当试图定位由控制 32ab4ba45e0a69a1 公钥标记的组织发布的、区域性中立的 SomeClassLibrary 程序集的 2.0.0.0 版本时。

## 发布者策略控制

在上一节描述的情形中，程序集的发布者只是将新版本的程序集发送给管理员，管理员安装该程序集并手动编辑应用程序或机器的 XML 配置文件。一般而言，当发布者修复程序集中的 bug 时，发布者希望有一种简单的方法来打包新程序集并将其分发给所有用户。但发布者还需要一种方法告诉每个用户的 CLR 使用新版本的程序集而不是旧版本的程序集。当然，每个用户都可以修改自己应用程序或机器的 XML 配置文件，但这极为不便且容易出错。发布者需要的是创建策略信息，并在新程序集安装时将该策略信息安装到用户的计算机上。在本节中，我将展示程序集的发布者如何创建这种策略信息。

假设你是程序集的发布者，并且刚刚创建了一个修复了一些 bug 的新版本程序集。当你打包新程序集准备分发给所有用户时，还应该创建一个 XML 配置文件。该配置文件与我们一直在讨论的配置文件非常相似。下面是针对 SomeClassLibrary.dll 程序集的一个示例文件（名为 SomeClassLibrary.config）。

```xml
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>

        <assemblyIdentity name="SomeClassLibrary"
          publicKeyToken="32ab4ba45e0a69a1" culture="neutral"/>

        <bindingRedirect
          oldVersion="1.0.0.0" newVersion="2.0.0.0" />

        <codeBase version="2.0.0.0"
          href="http://www.Wintellect.com/SomeClassLibrary.dll"/>

      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

当然，发布者只能为自己创建的程序集设置策略。此外，这里显示的元素是发布者策略配置文件中唯一可以指定的元素；例如，不能指定 probing 或 publisherPolicy 元素。

该配置文件告诉 CLR，只要引用程序集的 1.0.0.0 版本，就加载 SomeClassLibrary 程序集的 2.0.0.0 版本。现在，作为发布者的你可以创建一个包含此发布者策略配置文件的程序集。通过运行 AL.exe 来创建发布者策略程序集，如下所示。

```
AL.exe /out:Policy.1.0.SomeClassLibrary.dll
       /version:1.0.0.0
       /keyfile:MyCompany.snk
       /linkresource:SomeClassLibrary.config
```

让我解释一下 AL.exe 命令行开关的含义：

- **/out** 该开关告诉 AL.exe 创建一个新的 PE 文件，名为 Policy.1.0.SomeClassLibrary.dll，该文件仅包含一个清单。此程序集的名称非常重要。名称的第一部分 Policy 告诉 CLR 该程序集包含发布者策略信息。名称的第二和第三部分 1.0 告诉 CLR，此发布者策略程序集适用于 SomeClassLibrary 程序集中主版本和次版本为 1.0 的任何版本。发布者策略仅适用于程序集的主版本号和次版本号；不能创建针对程序集特定生成或修订版本的发布者策略。名称的第四部分 SomeClassLibrary 指示该发布者策略所对应的程序集的名称。名称的第五部分也是最后一部分 dll 只是生成程序集文件的扩展名。

- **/version** 该开关标识发布者策略程序集的版本；此版本号与 SomeClassLibrary 程序集本身无关。你知道，发布者策略程序集也可以有版本。今天，发布者可能创建一条发布者策略，将 SomeClassLibrary 的 1.0.0.0 版本重定向到 2.0.0.0 版本。将来，发布者可能希望将 SomeClassLibrary 的 1.0.0.0 版本指向 2.5.0.0 版本。CLR 使用此版本号，以便它知道要选择最新版本的发布者策略程序集。

- **/keyfile** 该开关使 AL.exe 使用发布者的公钥/私钥对为发布者策略程序集签名。此密钥对还必须与用于 SomeClassLibrary 程序集所有版本的密钥对匹配。毕竟，CLR 正是通过这种方式知道同一发布者同时创建了 SomeClassLibrary 程序集和此发布者策略文件。

- **/linkresource** 该开关告诉 AL.exe，XML 配置文件应被视为程序集的一个单独文件。生成的程序集由两个文件组成，这两个文件都必须与新版 SomeClassLibrary 程序集一起打包并部署给用户。顺便说一下，不能使用 AL.exe 的 /embedresource 开关将 XML 配置文件嵌入程序集文件以构成单文件程序集，因为 CLR 要求 XML 文件包含在它自己单独的文件中。

构建完此发布者策略程序集后，可以将其与新的 SomeClassLibrary.dll 程序集文件打包在一起并部署给用户。发布者策略程序集必须安装到 GAC 中。尽管 SomeClassLibrary 程序集也可以安装到 GAC，但不一定非要这样。它可以部署到应用程序的基目录或由 codeBase URL 标识的其他目录中。

> **重要** 发布者只应在部署程序集的更新或服务包版本时创建发布者策略程序集。在全新安装应用程序时，不应安装任何发布者策略程序集。

关于发布者策略，我还想说明最后一点。假设发布者分发了发布者策略程序集，但由于某种原因，新程序集引入的 bug 比修复的 bug 还多。如果发生这种情况，管理员希望告诉 CLR 忽略发布者策略程序集。要让运行时这样做，管理员可以编辑应用程序的配置文件并添加以下 publisherPolicy 元素。

```xml
    <publisherPolicy apply="no"/>
```

此元素可以作为 `<assemblyBinding>` 元素的子元素放在应用程序的配置文件中，以便应用于所有程序集；或者作为 `<dependentAssembly>` 元素的子元素放在应用程序的配置文件中，以便应用于特定程序集。当 CLR 处理应用程序的配置文件时，它将看到不应在 GAC 中查找发布者策略程序集。因此，CLR 将继续使用程序集的旧版本来运行。但请注意，CLR 仍会检查并应用 Machine.config 文件中指定的任何策略。

> **重要** 发布者策略程序集是发布者就程序集不同版本之间的兼容性做出声明的一种方式。如果程序集的新版本不打算与早期版本兼容，则发布者不应创建发布者策略程序集。通常，当你构建修复 bug 的新版本程序集时，应使用发布者策略程序集。你应当测试新版本程序集的向后兼容性。另一方面，如果你正在为程序集添加新功能，则应认为该程序集与先前版本没有关系，并且不应随附发布者策略程序集。此外，对这种程序集无需进行任何向后兼容性测试。
