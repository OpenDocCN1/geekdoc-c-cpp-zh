
System.Console 类型）。从 TypeRef 条目开始，CLR 被引导到 AssemblyRef 条目：“mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”。此时，CLR 知道它需要哪个程序集。现在，CLR 必须定位该程序集以便加载它。

当解析被引用的类型时，CLR 可以在以下三个位置之一找到该类型：

- **同一文件** 对同一文件中类型的访问在编译时确定（有时称为早期绑定）。该类型直接从文件中加载，然后继续执行。

- **不同文件，同一程序集** 运行时确保被引用的文件确实位于当前程序集清单的 ModuleRef 表中。然后，运行时在加载程序集清单文件的目录中查找。该文件被加载，检查其哈希值以确保文件完整性，找到该类型的成员，然后继续执行。

- **不同文件，不同程序集** 当被引用的类型位于另一个程序集的文件中时，运行时加载包含被引用程序集清单的文件。如果此文件不包含该类型，则加载相应的文件。找到该类型的成员，然后继续执行。

**注意** ModuleDef、ModuleRef 和 FileDef 元数据表使用文件名及其扩展名来引用文件。然而，AssemblyRef 元数据表通过不带扩展名的文件名来引用程序集。当绑定到程序集时，系统会在尝试通过探测目录来定位文件时自动追加 .dll 和 .exe 文件扩展名，如第 2 章“简单管理控制（配置）”一节所述。

如果在解析类型引用时发生任何错误——找不到文件、无法加载文件、哈希不匹配等——则会抛出相应的异常。

**注意** 如果需要，你的代码可以向 System.AppDomain 的 AssemblyResolve、ReflectionOnlyAssemblyResolve 和 TypeResolve 事件注册回调方法。在回调方法中，你可以执行解决绑定问题的代码，使应用程序能够继续运行而不抛出异常。

在前面的示例中，CLR 确定 System.Console 是在与调用方不同的程序集中实现的。CLR 必须搜索该程序集，并加载包含该程序集清单的 PE 文件。然后扫描清单，以确定实现该类型的 PE 文件。如果清单文件包含被引用的类型，则一切正常。如果该类型位于该程序集的另一个文件中，则 CLR 加载另一个文件并扫描其元数据以定位该类型。然后，CLR 创建其内部数据结构来表示该类型，JIT 编译器完成 Main 方法的编译。最后，Main 方法可以开始执行。

图 3-2 说明了类型绑定是如何发生的。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_86_0.png)

注意：如果任何操作失败，则会抛出相应的异常。

**图 3-2** 流程图展示了在给定引用某个方法或类型的 IL 代码时，CLR 如何使用元数据来定位定义该类型的正确程序集。

**重要** 严格来说，刚才描述的示例并非 100% 正确。对于引用未随 .NET Framework 一起发布的程序集中定义的方法和类型，上述讨论是正确的。然而，.NET Framework 程序集（包括 MSCorLib.dll）与正在运行的 CLR 版本紧密相关。任何引用 .NET Framework 程序集的程序集始终绑定到与 CLR 版本匹配的版本。这称为*统一*，Microsoft 这样做是因为他们使用特定版本的 CLR 测试所有 .NET Framework 程序集；因此，统一代码栈有助于确保应用程序正常工作。

因此，在前面的示例中，对 `System.Console` 的 `WriteLine` 方法的引用会绑定到与 CLR 版本匹配的任意版本的 MSCorLib.dll，而不管程序集的 AssemblyRef 元数据表中引用的是哪个版本的 MSCorLib.dll。

这个故事还有一个转折：对 CLR 而言，所有程序集都通过名称、版本、区域性和公钥来标识。然而，GAC 使用名称、版本、区域性、公钥和 CPU 架构来标识程序集。当在 GAC 中搜索程序集时，CLR 会确定应用程序当前运行在哪种类型的进程中：32 位 x86（可能使用 WoW64 技术），

```xml
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

这个 XML 文件向 CLR 提供了大量信息。它说明了以下内容：

- **probing 元素** 当尝试查找弱命名程序集时，请在应用程序基目录的 AuxFiles 和 bin\subdir 子目录中查找。对于强命名程序集，CLR 会在 GAC 中或 codeBase 元素指定的 URL 中查找。只有在未指定 codeBase 元素时，CLR 才会在应用程序的私有路径中查找强命名程序集。

- **第一个 dependentAssembly、assemblyIdentity 和 bindingRedirect 元素** 当尝试定位由控制 32ab4ba45e0a69a1 公钥标记的组织发布的、区域性中立的 SomeClassLibrary 程序集的 1.0.0.0 版本时，改为定位同一程序集的 2.0.0.0 版本。

- **codeBase 元素** 当尝试定位由控制 32ab4ba45e0a69a1 公钥标记的组织发布的、区域性中立的 SomeClassLibrary 程序集的 2.0.0.0 版本时，请尝试在以下 URL 找到它：*www.Wintellect.com/SomeClassLibrary.dll*。尽管我在第 2 章没有提到，codeBase 元素也可以用于弱命名程序集。在这种情况下，程序集的版本号会被忽略，并且应从 XML 的 codeBase 元素中省略。此外，codeBase URL 必须指向应用程序基目录下的某个目录。

- **第二个 dependentAssembly、assemblyIdentity 和 bindingRedirect 元素** 当尝试定位由控制 1f2e74e897abbcfe 公钥标记的组织发布的、区域性中立的 TypeLib 程序集的 3.0.0.0 版本到 3.5.0.0 版本（含）时，改为定位同一程序集的 4.0.0.0 版本。

- **publisherPolicy 元素** 如果生成 TypeLib 程序集的组织已部署发布者策略文件（将在下一节描述），则 CLR 应忽略此文件。

在编译方法时，CLR 确定被引用的类型和成员。运行时利用此信息，通过查看引用程序集的 AssemblyRef 表，确定在生成调用程序集时最初引用的程序集。然后，CLR 在应用程序的配置文件中查找该程序集/版本，并应用任何版本号重定向；此时 CLR 正在查找这个程序集/版本。

如果 publisherPolicy 元素的 apply 属性设置为 yes——或者该元素被省略——CLR 会检查 GAC 中是否有新的程序集/版本，并应用程序集发布者认为必要的任何版本号重定向；此时 CLR 正在查找这个程序集/版本。我将在下一节更详细地讨论发布者策略。最后，CLR 在计算机的 Machine.config 文件中查找新的程序集/版本，并在那里应用任何版本号重定向。

此时，CLR 知道它应加载的程序集版本，并尝试从 GAC 加载该程序集。如果该程序集不在 GAC 中，并且没有 codeBase 元素，则 CLR 会像我在第 2 章中描述的那样探测该程序集。如果执行最后一次重定向的配置文件还包含 codeBase 元素，则 CLR 会尝试从 codeBase 元素指定的 URL 加载该程序集。

使用这些配置文件，管理员可以真正控制 CLR 决定加载哪个程序集。如果应用程序遇到 bug，管理员可以联系出问题的程序集的发布者。发布者可以向管理员发送一个可安装的新程序集。默认情况下，CLR 不会加载这个新程序集，因为已经生成的程序集不引用新版本。然而，管理员可以修改应用程序的 XML 配置文件，指示 CLR 加载新程序集。

如果管理员希望计算机上的所有应用程序都采用新程序集，则可以改为修改计算机的 Machine.config 文件，这样每当应用程序引用旧程序集时，CLR 都会加载新程序集。

如果新程序集未能修复原始 bug，管理员可以从配置文件中删除绑定重定向行，应用程序将恢复为之前的行为。需要注意的是，系统允许使用与元数据中记录的程序集版本不完全匹配的程序集。这种额外的灵活性非常方便。

### 发布者策略控制

在上一节描述的场景中，程序集的发布者只是将程序集的新版本发送给管理员，管理员安装该程序集并手动编辑应用程序或计算机的 XML 配置文件。一般来说，当发布者修复程序集中的 bug 时，发布者希望有一种简便的方法来打包新程序集并将其分发给所有用户。但发布者还需要一种方法，告诉每个用户的 CLR 使用新的程序集版本而不是旧程序集版本。当然，每个用户可以修改其应用程序或计算机的
