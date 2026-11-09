
XML 配置文件虽然可以，但这非常不方便且容易出错。发布者需要的是在安装新程序集时，将策略信息安装到用户计算机上的方式。在本节中，我将演示程序集的发布者如何创建这些策略信息。

假设你是某个程序集的发布者，并且刚刚创建了一个修复了一些 bug 的新版本程序集。当你打包新程序集以分发给所有用户时，还应该创建一个 XML 配置文件。这个配置文件与我们一直在讨论的配置文件看起来一模一样。下面是一个用于 SomeClassLibrary.dll 程序集的示例文件（名为 SomeClassLibrary.config）：

```xml
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>

                <assemblyIdentity name="SomeClassLibrary"
                    publicKeyToken="32ab4b45e0a69a1" culture="neutral"/>

                <bindingRedirect
                    oldVersion="1.0.0.0" newVersion="2.0.0.0" />

                <codeBase version="2.0.0.0"
                    href="http://www.intellect.com/SomeClassLibrary.dll"/>

            </dependentAssembly>
        </assemblyBinding>
    </runtime>
</configuration>
```

当然，发布者只能为自己创建的程序集设置策略。此外，此处显示的元素是可以在发布者策略配置文件中指定的唯一元素；例如，你不能指定 probing 或 publisherPolicy 元素。

这个配置文件告诉 CLR，只要引用了 SomeClassLibrary 程序集的 1.0.0.0 版本，就加载该程序集的 2.0.0.0 版本。现在，你作为发布者，可以创建一个包含此发布者策略配置文件的程序集。你可以通过如下方式运行 AL.exe 来创建发布者策略程序集：

```text
AL.exe /out:Policy.1.0.SomeClassLibrary.dll
      /version:1.0.0.0
      /keyfile:MyCompany.snk
      /linkresource:SomeClassLibrary.config
```

让我解释一下 AL.exe 的命令行开关的含义：

-   `/out` 这个开关告诉 AL.exe 创建一个名为 Policy.1.0.SomeClassLibrary.dll 的新 PE 文件，该文件仅包含一个清单。这个程序集的名称非常重要。名称的第一部分 Policy 告诉 CLR 这个程序集包含发布者策略信息。名称的第二和第三部分 1.0 告诉 CLR 这个发布者策略程序集适用于主版本号和次版本号为 1.0 的 SomeClassLibrary 的任何版本。发布者策略仅适用于程序集的主版本号和次版本号；你不能创建针对程序集特定构建或修订版本的发布者策略。名称的第四部分 **SomeClassLibrary** 表示此发布者策略对应的程序集的名称。名称的第五部分也是最后一部分 *dll* 只是生成程序集文件的扩展名。
-   `/version` 此开关标识发布者策略程序集的版本；这个版本号与 SomeClassLibrary 程序集本身无关。你知道，发布者策略程序集也可以有版本。今天，发布者可能会创建一个发布者策略，将 SomeClassLibrary 的 1.0.0.0 版本重定向到 2.0.0.0 版本。将来，发布者可能希望将 SomeClassLibrary 的 1.0.0.0 版本定向到 2.5.0.0 版本。CLR 使用此版本号，以便知道要选择最新版本的发布者策略程序集。
-   `/keyfile` 此开关使 AL.exe 使用发布者的公钥/私钥对来对发布者策略程序集进行签名。这个密钥对也必须与用于 SomeClassLibrary 程序集所有版本的密钥对匹配。毕竟，CLR 正是通过这种方式知道同一个发布者同时创建了 SomeClassLibrary 程序集和此发布者策略文件。
-   `/linkresource` 此开关告诉 AL.exe，XML 配置文件将被视为程序集的一个单独文件。生成的程序集由两个文件组成，这两个文件都必须随新版本的 SomeClassLibrary 程序集一起打包并部署给用户。顺便说一下，你不能使用 AL.exe 的 `/embedresource` 开关将 XML 配置文件嵌入到程序集文件中，从而生成单文件程序集，因为 CLR 要求 XML 文件必须包含在它自己的单独文件中。

一旦构建了这个发布者策略程序集，它就可以与新 SomeClassLibrary.dll 程序集文件一起打包并部署给用户。发布者策略程序集必须安装到 GAC 中。虽然 SomeClassLibrary 程序集也可以安装到 GAC 中，但它不是必须的。它可以部署到应用程序的基目录或由 codeBase URL 标识的其他目录中。

**重要说明** 发布者只应在部署程序集的更新版本或服务包版本时创建发布者策略程序集。在全新安装应用程序时，不应安装任何发布者策略程序集。

关于发布者策略，我想最后说明一点。假设某个发布者发布了发布者策略程序集，但出于某种原因，新程序集引入的 bug 比修复的 bug 还多。如果出现这种情况，管理员可能想让 CLR 忽略该发布者策略程序集。要让运行时这样做，管理员可以编辑应用程序的配置文件，并添加以下 `publisherPolicy` 元素：

```xml
<publisherPolicy apply="no"/>
```

该元素可以作为 `<assemblyBinding>` 元素的子元素放在应用程序的配置文件中，以便它适用于所有程序集；或者作为 `<dependentAssembly>` 元素的子元素放在应用程序的配置文件中，以使其适用于特定程序集。当 CLR 处理应用程序的配置文件时，它会看到不应在 GAC 中查找发布者策略程序集。因此，CLR 将继续使用旧版本的程序集运行。但请注意，CLR 仍将检查并应用 Machine.config 文件中指定的任何策略。

**重要说明** 发布者策略程序集是发布者就程序集不同版本之间的兼容性做出声明的一种方式。如果程序集的新版本不打算与早期版本兼容，则发布者不应创建发布者策略程序集。通常，当你构建修复 bug 的程序集新版本时，应使用发布者策略程序集。你应该测试程序集新版本的向后兼容性。另一方面，如果你要向程序集添加新功能，则应将此程序集视为与先前版本没有关系，并且不应发布发布者策略程序集。此外，对此类程序集无需进行任何向后兼容性测试。

## 第 4 章：类型基础

**本章内容：**

-   所有类型都派生自 `System.Object` — 91
-   类型之间的转换 — 93
-   命名空间和程序集 — 97
-   运行时如何关联 — 102

在本章中，我将介绍使用类型和公共语言运行时（CLR）所需的基础信息。具体来说，我将讨论你可以期望每个类型都具有的最小行为集。我还将描述类型安全、命名空间、程序集以及将对象从一种类型转换为另一种类型的各种方式。最后，我将通过解释类型、对象、线程栈和托管堆在运行时如何相互关联来结束本章。

### 所有类型都派生自 `System.Object`

运行时要求每个类型最终都必须派生自 `System.Object` 类型。这意味着以下两种类型定义是相同的：

```csharp
// Implicitly derived from Object              // Explicitly derived from Object
class Employee {                              class Employee : System.Object {
    ...                                           ...
}                                             }
```

因为所有类型最终都派生自 `System.Object`，所以你可以保证每种类型的每个对象都具有一组最小的方法。具体来说，`System.Object` 类提供了表 4-1 中列出的公共实例方法。

**表 4-1** `System.Object` 的公共方法

| 公共方法 | 说明 |
|---|---|
