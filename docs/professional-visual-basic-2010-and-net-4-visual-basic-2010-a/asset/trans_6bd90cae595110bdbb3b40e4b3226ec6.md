

配置文件的首要目的是为希望覆盖 CLR 默认策略处理的开发人员或管理员提供绑定相关信息。

具体来说，配置文件以 XML 编写，其根节点名为 <configuration>，并且必须存在结束节点 </configuration> 才能在语法上正确。配置文件分为代表不同控制区域的特定类型节点。这些区域如下：

- Startup
- Runtime
- Remoting
- Crypto
- Class API
- Security

尽管所有这些区域都很重要，本章仅涵盖前两个。所讨论的所有设置都可以添加到应用程序配置文件中。其中一些设置（已指出）也可以添加到机器配置文件中。如果应用程序配置文件中的设置与机器配置文件中的设置冲突，则使用机器配置文件中的设置。在下面关于配置设置的讨论中谈到程序集引用时，我们专门指的是共享程序集（这意味着程序集具有强名称，这是 GAC 中程序集所必需的）。

## Startup Settings

应用程序和机器配置文件的 <startup> 节点具有 <requiredRuntime> 节点，用于指定应用程序所需的运行时版本。这是因为不同版本的 CLR 可以并排运行在同一台机器上。以下示例展示了如何在配置文件中指定 .NET 运行时版本：

```
<configuration>
  <startup>
    <requiredRuntime version ="4.0.xxxx" safemode ="true"/>
  </startup>
</configuration>
```

## Runtime Settings

运行时节点，写作 <runtime>（不要与 <requiredRuntime> 混淆），指定用于管理 CLR 如何处理垃圾回收和程序集版本的设置。通过这些设置，你可以指定应用程序所需的程序集版本，或将其重定向到完全不同的版本。

### Loading a Particular Version of an Assembly

应用程序和机器配置文件可用于确保加载特定版本的程序集。你可以指示此版本是否应始终加载，或仅替换程序集的特定版本。此功能通过在配置文件中使用 <assemblyIdentity> 和 <bindingRedirect> 元素来实现，如以下示例所示：

```
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="AssemblyName"
                          publickeytoken="b77a5c561934e089"
                          culture="en-us"/>
        <bindingRedirect oldVersion="*"
                         newVersion="2.0.50.0"/>
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

```
</dependentAssembly>
</assemblyBinding>
</runtime>
</configuration>
```

Code snippet from CodeSnippetsChapter31

<assemblyBinding> 节点用于通过 <dependentAssembly> 节点和 <probing> 节点（你将很快看到）声明程序集位置的设置以及重定向。

在上一个示例中，当 CLR 解析对名为 AssemblyName 的程序集的引用时，它会加载版本 2.0.50.0 而不是清单中出现的版本。如果你只想在引用特定版本时加载程序集的 2.0.50.0 版本，则可以将 oldVersion 属性的值替换为你想要替换的版本号（例如，1.5.0.0）。publickeytoken 属性用于存储要替换的程序集强名称的哈希值。这确保了正确识别程序集。culture 属性也是如此。

### Defining the Location of an Assembly

程序集的位置也可以在应用程序和机器配置文件中定义。你可以使用 <codeBase> 元素通知 CLR 程序集的位置。这使你能够分发应用程序，并在首次使用时按需下载外部引用的程序集：

```
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="AssemblyName"
                    publickeytoken="b77a5c561934e089"
                    culture="en-us"/>
                <codeBase version="2.0.50.0"
                    href="http://www.wrox.com/AssemblyName.dll"/>
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
</configuration>
```

Code snippet from CodeSnippetsChapter31

从此示例可以看出，每当解析对程序集 AssemblyName 的版本 2.0.50.0 的引用时（并且程序集尚未在用户计算机上），CLR 将尝试从 href 属性中定义的位置加载程序集。href 属性中定义的位置是标准 URL，可用于在 Internet 上或本地定位文件。

如果找不到程序集或 href 属性中定义的程序集清单中的详细信息与配置文件中定义的信息不匹配，则程序集的加载将失败，并且你会收到 TypeLoadException。如果前一个示例中程序集的版本实际上是 2.0.60.0，则程序集仍会加载，因为版本号仅在内部版本号和修订号上不同。

### Providing the Search Path

需要考虑的配置文件的最后用途是提供在应用程序目录中定位程序集时使用的搜索路径。此设置仅适用于应用程序配置文件（例如 AppName.exe.config）。默认情况下，CLR 仅在应用程序基本目录中搜索程序集——它不会查看任何子目录。你可以通过在应用程序配置文件中使用 <probing> 元素来修改此行为，如以下示例所示：

```
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <probing privatePath="regional"/>
        </assemblyBinding>
    </runtime>
</configuration>
```

Code snippet from CodeSnippetsChapter31

privatePath 属性可以包含相对于应用程序目录的目录列表（以分号分隔），你希望 CLR 在尝试定位程序集时搜索这些目录。privatePath 属性不能包含绝对路径名。

作为解析程序集引用的部分，CLR 首先在应用程序的基本目录中检查它。如果找不到它，然后它会按顺序查找 privatePath 变量中指定的所有子目录，以及查找与程序集同名的子目录。如果要解析的程序集名为 AssemblyName，则 CLR 还会检查名为 AssemblyName 的子目录是否存在。

但故事还未结束。如果要解析的引用程序集包含 culture 设置，则 CLR 还会在其搜索的每个目录中检查特定于文化的子目录。例如，如果 CLR 正在尝试解析对名为 AssemblyName 且文化为 en 的程序集的引用，并且 privatePath 等于上一个示例中的值，并且正在运行的应用程序的主目录为 C:\ExampleApp，则 CLR 将按以下顺序查找以下目录：

- C:\ExampleApp
- C:\ExampleApp\en
- C:\ExampleApp\en\AssemblyName
- C:\ExampleApp\regional\en
- C:\ExampleApp\regional\en\AssemblyName

正如你所见，CLR 可以探测相当多的目录来定位程序集。当 CLR 解析外部程序集时，它首先咨询配置文件，以确定是否需要修改解析程序集的过程。如前所述，你可以修改解析过程以满足你的需求。

## BASICS OF REFLECTION

如第 4 章所述，你可以使用称为反射的过程探索给定程序集的内部结构。你可以找出当前应用程序域中加载了哪些程序集。你可以发现每个程序集中驻留的类型，以及对于任何给定类型，该类型公开的方法和属性。你甚至可以通过反射执行方法或更改属性值，即使在编译时你可能不知道方法或属性的名称。

在本节中，你将看到执行每项操作所需的基本代码。代码使用 System.Reflection 命名空间中的类，最值得注意的是 Assembly 类，并且每个示例都假定代码模块具有导入 System.Reflection 的 Imports 语句。

使用反射功能所需的主要类包括以下内容：

- Assembly — 包含检查程序集元数据甚至操作程序集的成员
- AppDomain — 包含有关当前正在运行的应用程序域的信息
- Type — 提供对 .NET 类型信息的访问

