

开发者也可以为每个特定的操作系统使用专用软件来完成此操作（我们将在每个平台上审查几种解决方案）。但是，你必须牢记，如果你想为应用程序针对的每个平台提供安装程序，你将需要管理同样数量的安装程序项目，这会给你的开发带来额外的复杂性。

此后，我们将审查一种更适合专业要求的统一多平台安装开发工具。

## 11.1 为每个平台开发安装程序

### 11.1.1 为 Windows 生成安装程序

Windows 上有大量解决方案可用，这些解决方案不仅为你的程序提供安装程序，还可以执行高级任务，例如：依赖项检查、条件系统版本安装等。

以下是我们认为最专业的安装程序简短列表：

- Wix：该程序允许开发者为 Windows 系统生成安装程序，它内置于 Visual Studio 2019 中，需使用免费扩展（请参阅 Visual Studio 市场）。SDK 允许使用用 C# 编写的自定义操作（以及其他功能）。该项目拥有活跃的社区支持。它是微软使用的工具。
- Visual Studio Installer 项目（InstallShield）：这是标志性软件 InstallShield 的“轻量”版本，此扩展不适用于 Visual Studio Community 版本。
- Nsis：（Nullsoft 可脚本安装系统）一个专业的开源程序，用于生成 Windows 安装程序，它小巧灵活，允许使用插件和脚本（在开源社区中非常流行）。

根据我们的经验，在 Windows 上实现安装程序的最佳解决方案是 Wix，该产品提供一种更易于管理且免费的脚本语言（因为它是开源的），此外你可以在互联网上找到大量文档（附带现成的脚本）。其他解决方案，如 Microsoft Visual Studio Installer（InstallShield 轻量版）和 Nullsoft，在各自的应用领域都有其自身优势，可能更适合你特定软件的需求。

| | https://wixtoolset.org |
| | http://www.flexera.com |
| | https://nsis.sourceforge.io |
| | https://advancedinstaller.com |

### 11.1.2 为 macOS 生成安装程序

macOS 通常不使用安装程序，应用程序需要打包为“.app”文件。

“.app”文件可以直接执行。这是 Apple Store 分发的文件格式。

尽管如此，你可以生成“.pkg”、“.mpkg”和“.dmg”文件，以便在此环境中分发你的应用程序。

- 使用“DiskUtility.app”生成.dmg文件：使用“磁盘工具”应用程序手动创建 DMG 文件可能是分发基本应用程序的首选方案。
- iDMG：这是一个拖放工具，用于从文件夹内容创建.dmg文件，它还集成了加密功能（此产品不再开发）。
- Arealium 的 Dmg Canvas：这是一个商业解决方案，允许你为软件分发提供精心设计的安装程序。
- Packages：这是一个由独立开发者开发的免费工具。尽管如此，该产品看起来非常专业，并为在 macOS 上构建应用程序的安装程序提供了非常好的灵活性。“Packages”集成了许多高级功能，如演示文稿编辑器、依赖项编辑器、要求编辑器以及使用证书进行签名的可能性。

| | http://en.wikipedia.org/wiki/Installer_(macOS) |
| | http://arealium.com/dmgcanvas |
| | https://s.sudre.free.fr/Software/Packages |

工具的选择将取决于你想要分发的软件类型。但就我们的观点而言，“Packages”在 macOS 上提供了最简洁、最便宜的解决方案。

### 11.1.3 为 Ubuntu 生成安装包

在 Linux 上分发应用程序与在 Windows（或 macOS）环境中有很大不同，存在许多共存的解决方案用于应用程序的打包和部署。

我们将在 Ubuntu（基于 Debian）发行版上审查其中几种。

- AppImage：AppImage 是 Linux 平台上分发便携式软件的文件格式。与分发应用程序的传统方式相比，AppImage 具有许多优势（因为所有依赖项都包含在一个紧凑的文件中）。
- Debian 包制作器：这是一个用于为你的应用程序创建 Debian 包的 GUI 工具，该工具运行完美，其图形界面易于使用，但已有 10 年未更新（稳定）。
- Nixstaller：这是一个命令行工具，用于帮助开发者在 Linux 上构建图形安装程序。
- izPack（基于 Java）：自 2001 年以来的开源项目，izPack 基于 Java，它为应用程序的打包和分发生成一个单一安装程序。它使用 XML 脚本语言。
- Makeself：这是一个小型 shell 脚本，它从目录生成自解压缩文件（它可以被视为 Linux 平台上分发软件的最小工具）。

鉴于 Linux 平台上为构建应用程序安装工具提供的大量解决方案，我们可以推荐使用 AppImage。

确实，AppImage 提供了一种独特的方式，即开箱即用的应用程序打包解决方案。通过在包中包含应用程序所需的所有元素，它为在 Linux 操作系统上分发你的应用程序提供了一种可靠的方式。此外，它不需要“管理员”权限来安装应用程序（这可能很方便）。

AppImage 在 Linux 开发者社区中获得了广泛认可（并赢得了可靠性的坚实声誉）。该应用程序是开源的，并提供大量文档。

| | https://www.appimage.org |
| | http://debianpackagemaker.blogspot.com |
| | http://directory.fsf.org/wiki/Nixstaller |
| | http://lzipack.org |
| | https://makeself.io |

## 11.2 多平台统一安装程序开发：INSTALLBUILDER

即使先前介绍的解决方案可以满足你的安装程序开发需求，这些解决方案也意味着需要开发多个安装项目（每个操作系统一个）。

在整本书中，我们一直努力为开发者提供尽可能低成本（几乎免费）的链接和解决方案，但开发多平台安装程序的可行方案既不是开源的，甚至也不是免费的，这是 Bitrock 的商业软件 InstallBuilder。

### 11.2.1 什么是 InstallBuilder

Bitrock 的 InstallBuilder 创建多平台安装程序和本机安装包。它允许你在任何环境中部署应用程序。它为每个操作系统提供可靠且专业的安装体验。

这款专业软件为开发应用程序的稳健多平台安装程序提供了原生工具。

InstallBuilder 包含许多有用的功能：

- 使用安装脚本语言
- 安装调试器（带有专用脚本语言）。
- 自动更新集成。
- 多语言。
- 多语言。
- 优化器。
- 多种安装模式（GUI/控制台）。
- 在 Windows、Ubuntu 和 macOS 上为你的安装程序提供原生外观和感觉。

InstallBuilder 为安装程序的开发提供了完整的环境，它允许开发者在不同平台之间保持安装程序同步。由于它是商业产品，你可以找到大量文档（请参阅下方的参考链接），了解如何应对你的特定安装约束。

