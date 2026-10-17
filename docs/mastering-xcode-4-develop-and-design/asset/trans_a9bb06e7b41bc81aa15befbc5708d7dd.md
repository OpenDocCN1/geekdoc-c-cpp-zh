
图 19.2 令人失望的日志搜索结果

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_316_0.png)

不幸的是，这个精巧的特性也带来了巨大的失望。在撰写本文时，这些脚本的标准输出似乎会随意出现在任何地方，具体取决于它所属的构建操作（也许还取决于月相——需要进一步测试）。快速查看图 19.2 可以发现，在构建日志中搜索——这本是容纳“构建操作后脚本”标准输出的好地方——却一无所获。

构建操作脚本的输出被转存到系统控制台日志中，但在其他任何地方似乎都看不到；而运行操作的输出则同时出现在调试器控制台和系统控制台中。测试输出出现在系统控制台日志中，但既不会出现在日志导航器的测试日志中，也不会出现在调试器控制台中。性能分析和归档操作的输出只出现在系统控制台日志中，而分析操作的前置和后置操作的输出则完全不可用（尽管它们会出现在编辑器和问题导航器的界面中）。如果你对此感到困惑，那么你并不孤单。

> 注意：这个功能很可能只是 Xcode 4 中一个尚未成熟的部分，以后会得到改进。就目前而言，如果你需要这些脚本产生一致的标准输出日志，那恐怕要失望了。很可能在本书出版前，Xcode 的一次更新就会让作者收回这番话。他的盐和胡椒已经准备好了。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_316_1.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_317_0.png)

图 19.3 空的 Run Script 构建阶段

## RUN SCRIPT 构建阶段

尽管前面说了那么多悲观的话，但依然存在久经考验的 Run Script 构建阶段，你在第 14 章中已经了解过它。它的输出很容易定位，并且提供了令人印象深刻的一系列环境变量。你可以根据需要，为特定目标的构建阶段添加任意多个此类脚本。图 19.3 显示了一个添加到 TestApp 目标并展开以显示其设置的空 Run Script 构建阶段。Run Script 脚本按照它们在目标构建阶段列表中出现的顺序执行。

“Shell”字段让你可以指定用于执行脚本的 shell。默认是 /bin/sh。其他可选方案包括 bash（Mac OS X 的默认 shell）、perl、python，或任何已安装的脚本环境。

“Show environment variables in build log”（在构建日志中显示环境变量）复选框（图 19.3）是调试脚本时的一个便捷选项，可确保你使用的变量确实具有预期的值。当此复选框选中时，可供 shell 使用的环境变量将包含在构建日志中。但你可以放心地关闭此选项，这不会影响脚本的运行环境，还能减小构建日志的大小。

当选中“Run script only when installing”（仅在安装时运行脚本）复选框时，只有在当前配置下的“Installation Directory”（安装目录）构建设置被设为有效路径，且“Deployment Location”（部署位置）构建设置被设为“Yes”时（触发“安装构建”），脚本才会执行。

## XCODE 的环境变量

Xcode 提供了许多环境变量，其中包含对你的脚本工作有用的信息。例如，了解构建产品的路径，或者了解某些外部资源相对于项目文件夹的路径，可能很重要。了解正在使用哪种构建配置，或者构建设置中指定了哪个安装目录，也可能很有用。

当你使用脚本通过自己的后处理来扩展构建过程时，这些构建环境信息是无价之宝。

### 用“脏”方法获取变量

你可以使用一个小技巧，快速获取项目中使用的环境变量及其在构建时的值。这个技巧相当狡猾，因为它本身就用到了一个构建脚本。如果你熟悉 Unix，你可能知道 printenv 命令，它会打印当前的环境变量及其值。

要使用这个技巧，只需向 TestApp 目标添加一个 Run Script 构建阶段。回想一下，你需要导航到 TestApp 项目，选择 TestApp 目标，然后点击“Build Phases”标签页。使用窗口底部的“Add Build Phase”按钮，选择“Add Run Script”。在 Run Script 阶段控件中的脚本编辑器中添加以下内容：

```
printenv > ~/Desktop/XcodeBuildEnvironmentVariables.txt
```

图 19.5 将环境变量打印到文本文件的脚本

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_320_0.png)

你的 Run Script 阶段应该如图 19.5 所示。构建应用程序（按 Command+B 强制构建）。你要求的文本文件（XcodeBuildEnvironmentVariables.txt）应该出现在桌面上。打开并查看它。

### 用“理智”的方法获取变量

另外请注意图 19.5 中的“Show environment variables in build log”复选框。这在调试脚本时非常有用，因为构建系统会将你刚才放入便捷文本文件的内容直接转储到构建日志中。

## 简单脚本示例

我们当然可以花大量篇幅来详细描述简单和复杂的脚本示例。但既然本书聚焦于 Xcode，只需要一个基本的实际示例来演示使用自定义处理扩展构建系统的部分威力即可。

在第 12 章中，你学习了如何使用 Xcode 4 首选的方法部署应用程序：Archive 操作。此操作会为目标构建发布版本，然后创建一个 Xcode 归档，用于提交到 Apple 的 App Store。正如第 12 章所提到的，Apple 似乎认为开发者所说的“部署”当然就是指“在 App Store 上销售”。但许多拥有 Mac OS X 产品的独立软件供应商可能未必愿意放弃他们现有的分发渠道而改用 Apple 的渠道。因此，对于这些“异类”来说，需要额外做些工作来定制部署过程。

### 场景

考虑以下场景。你想在自己的网站上分发 TestApp，无视 Apple 的善意。你希望用户能够以简单的 zip 文件形式下载应用程序，而 zip 文件中只包含应用程序本身。zip 文件（或某种归档）是必要的，因为应用程序包本质上是一些特殊的文件夹，直接下载会很不方便。归档时，你希望生成这个 zip 文件，并让它出现在 Finder 窗口中，这样你就可以方便地将文件复制到服务器。当然，这是一个非常基础的解决方案，但这个简单的“网关脚本”可以引导你构建更复杂的解决方案（参见“扩展脚本”一节），以满足你的需求。

一种方法是挂接到 Archive 流程中，因为它会自动为发布进行构建，并且确实会生成一个用于分发的归档。Xcode 仍然会创建它自己的归档（目前还无法阻止），但自定义脚本也会创建*你的*归档。

> **注意：** 当然，你可以将自己的归档操作脚本挂接到 Archive 操作的后处理操作中，但下面的示例将作为脚本编写的一般实际示例。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_321_0.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_323_0.png)

图 19.6 完成的自定义归档脚本

```
# Move to the built products directory
cd $BUILT_PRODUCTS_DIR

# Clean up any previous archiving folder and create a new one
rm -Rf Archive
mkdir Archive

# Compress the target into a zip file in the Archive folder
zip -r Archive/$TARGETNAME.zip $FULL_PRODUCT_NAME

# Show the Archive folder in the Finder
open ./Archive
```

要测试它，请从主菜单中选择 Product > Archive 来运行 Archive 操作。Archive 操作会像往常一样运行，但你还应该看到 Finder 窗口出现。

提示：你可能希望阻止 Xcode 打开 Organizer（默认情况下是打开的）。要做到这一点，请编辑 scheme（方案），选择 Archive 操作。取消勾选“Reveal Archive in Organizer”选项，然后点击“确定”。

