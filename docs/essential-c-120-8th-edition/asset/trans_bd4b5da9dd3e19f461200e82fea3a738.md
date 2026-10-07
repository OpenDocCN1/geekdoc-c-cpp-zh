

请注意，并非只有控制程序可以引用库和包。事实上，任何程序集都可以引用任何其他程序集。通常，一个库会引用另一个库，从而形成依赖链。

## 使用 Dotnet CLI 引用项目或库

在第 1 章中，我们讨论了如何创建一个控制台程序。这样做创建了一个包含 `Main` 方法的程序——这是程序开始执行的入口点。要为新创建的程序集添加引用，我们可以在之前的地方继续，使用额外的命令来添加引用：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj package \GeoCoordinates\Debug\netcoreapp2\GeoCoordinates.dll
```

`add` 参数之后是项目所引用的已编译程序集的文件路径。
与其引用程序集，你也可以引用项目文件。正如前面提到的，这会将项目连接起来，因此生成程序时将触发类库的编译（如果尚未编译的话）。这样做的优点是，程序编译时，它会自动定位编译后的类库程序集——无论是在 debug 还是 release 目录下。引用项目文件的命令如下：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj reference \GeoCoordinates\GeoCoordinates.csproj
```

如果你拥有类库的源代码且该源代码频繁更改，请考虑使用类项目文件来引用类库，而不是引用编译后的程序集。
完成项目或已编译程序集的引用后，你的项目就可以使用列表 10.3 中的 `Program` 类源代码进行编译了。

## 使用 Visual Studio 2022 引用项目或库

在第 1 章中，我们还讨论了如何使用 Visual Studio 创建控制台程序。这创建了一个包含 `Main` 方法的程序。要添加对 GeoCoordinates 程序集的引用，点击 Project->Add Reference... 菜单项。

接下来，在 Projects\Solution 选项卡中，选择 GeoCoordinates 项目并点击 OK 确认引用。

同样，若要添加程序集引用，请按照之前的相同过程操作，点击 Project->Add Reference... 菜单项。但是，这次点击 Browse... 按钮并导航到选择 GeoCoordinates.dll 程序集。

与使用 Dotnet CLI 一样，你可以使用列表 10.3 中的 `Program` 类代码编译程序项目。

## NuGet 打包

从 Visual Studio 2010 开始，微软引入了一种名为 NuGet 的库打包系统。该系统旨在提供一种在项目之间以及公司之间轻松共享库的方法。通常，一个库程序集不仅仅是一个单一的编译文件。它可能包含配置文件、其他资源以及相关的元数据。遗憾的是，在 NuGet 出现之前，没有可以标识所有依赖项的清单。此外，也没有标准的提供程序或包库来存放被引用的程序集。

NuGet 解决了这两个问题。NuGet 不仅包含一个可以标识作者、公司、依赖项等信息的清单，它还带有一个默认的包提供程序——NuGet.Org，在该网站上，包被上传、更新、索引，然后由想要利用它们的项目下载。通过 NuGet，你可以引用一个 NuGet 包（`*.nupkg`），它将将从你预配置的其中一个 NuGet URL 自动安装。

NuGet 包附带有一个清单（`*.nuspec` 文件），其中包含了包中包含的所有额外元数据。此外，它还提供了你可能需要的所有资源——本地化文件、配置文件、内容文件等。最终，NuGet 包是将所有单独资源组合成单个 ZIP 文件的归档——尽管扩展名为 `.nupkg`。如果你将文件重命名为 `*.zip` 扩展名，可以使用任何常用工具打开并检查该文件。

## 使用 Dotnet CLI 添加 NuGet 引用

要使用 Dotnet CLI 向项目添加 NuGet 包，需要：

```bash
dotnet add .\HelloWorld\HelloWorld.csproj package Microsoft.Extensions.Logging
```

要创建一个本地包，请使用 dotnet 命令：

```bash
dotnet pack
```

## 使用 Visual Studio 2022 添加 NuGet 引用

如果你按照 Visual Studio 2022 的说明进行操作：

1. 点击 Project->Manage NuGet Packages... 菜单项。
2. 选择 Browse 选项卡并在搜索框中输入 Microsoft.Extensions.Logging。
3. 点击 Install 按钮安装该包。

完成这些步骤后，Microsoft.Extensions.Logging 库将（添加到你的项目中，并包含它可能具有任何依赖项。

## 类型封装
...
)

