
未指定任何要配置的选项，但你可能希望这样做。运行 `configure -help` 可以查看可用选项。

安装后，所有的 Qtopia 文件将位于 `$QPEDIR/image`，而用户通过与 Qtopia 交互产生的文件将位于 `$QPEDIR/home`。在 Qtopspeak 中，“image"（镜像）是一个存储在桌面计算机上的 Qtopia 文件系统，当 Qtopia 环境处于虚拟帧缓冲区时会被其使用。

Qtopia 提供了自己的一套完整的文档集，非常值得熟悉一下，因为 Qtopia 提供了许多 Qt 桌面环境不具备（或与之不相关）的类。它的起点是 `$QPEDIR/doc/html/index.html`。

完成构建和安装后，我们可以通过运行 `$QPEDIR/scripts/runtopia` 进行初始测试。该脚本会启动带有特殊皮肤的虚拟缓冲区和 `qpe`，`qpe` 是包含 Qtopia 应用栈的 Qtopia 环境。我们可以分别启动虚拟缓冲区和 Qtopia 环境，但我们必须按照正确的顺序启动。如果我们不小心先启动了 `qpe`，Qtopia 将写入 X11 帧缓冲区，这将损坏屏幕。执行 `runtopia` 脚本时可以使用 `-help` 参数查看其支持的命令行选项列表。这些包括 `-skin` 以及一个可选的皮肤列表。

虚拟缓冲区有一个右键菜单，在 Qtopia 区域以外的任何地方点击右键即可弹出。菜单允许我们调整显示并终止 Qtopia。

现在 Qtopia 已经在虚拟帧缓冲区中运行，我们可以构建提供的示例应用程序之一，以查看该过程是如何运作的。然后，我们将从头开始创建一个非常简单的应用程序。

切换目录到 `$QPEDIR/examples/application`。此 Qtopia 有它自己的版本 `make qtopiamake`，位于 `$QPEDIR/bin`。运行它进行编译，然后运行 `make install`；这将示例（以及一些其他文件）复制到 Qtopia 的镜像目录中。现在，如果我们终止 Qtopia 并使用 `runtopia` 重新启动，我们新建的“Example”（示例）应用程序就可以用了。要运行该示例，点击 Qtopia 区域底部中间的 'Q' 按钮，然后点击 Packages（“箱子”）图标（位于指向手上方），然后点击“Example”（见图 24.3）。

我们通过创建一个名为 Unit Converter（单位转换器）的小而实用的 Qtopia 应用程序来结束本节，我们必须注意它。该应用程序如图 24.2 所示。它只使用 Qt API，几乎没有惊喜。在下一节中，我们将创建一个使用一些 Qtopia 特定 API 的更复杂的示例。

## 图 24.2. 单位转换器应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_938_0.png)

Unit Converter 应用程序将由三个文件组成：`main.cpp`、`unitconverter.h` 和 `unitconverter.cpp`。创建一个名为 `unitconverter` 的新目录，进入该目录并创建空的 `.cpp` 和 `.h` 文件。现在运行

```
qtopiamake -project
```

以生成一个 `.pro` 文件。该文件看起来如下所示：

```
qtopia_project(qtopia app)
TARGET = unitconverter
CONFIG += qtopia_main no_quicklaunch
HEADERS += unitconverter.h
SOURCES += main.cpp \
    unitconverter.cpp
pkg.domain = none
```

即使我们写了代码、构建了可执行文件并安装了它，它也不会出现在 Qtopia 的应用程序列表中。为了实现这一点，我们必须指定应用程序图片的位置、`.desktop` 文件的位置以及它应该被放置到哪里。提供一些打包信息也是良好的做法。由于这些原因，我们手动编辑了 `.pro` 文件，使其现在看起来像这样：

```
qtopia_project(qtopia app)
TARGET = unitconverter
CONFIG += qtopia_main no_quicklaunch
HEADERS += unitconverter.h
SOURCES += main.cpp \
    unitconverter.cpp
INSTALLS += desktop pics
```

```
desktop.files = unitconverter.desktop
desktop.path = appsApplications
desktop.hint = desktop
```

```
pics.files = pics/*
pics.path = pics/unitconverter
pics.hint = pics
```

```
pkg.name = unitconverter
pkg.desc = A program to convert between various units of measure
pkg.version = 1.0.0
pkg.domain = window
```

## 图 24.3. 定位示例应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_939_0.png)

`.pro` 文件现在包含一个 `INSTALLS` 条目，表示执行 `make install` 时，除了可执行文件外，应用程序的 `.desktop` 文件和图片将被安装。

按照惯例，图片存储在 `pics` 子目录下，`.pro` 文件中的 `pics.xxx` 条目指定源图片的位置以及它们安装的位置。`desktop.xxx` 条目指定应用程序 `.desktop` 文件的名称安装位置。将其安装在 `appsApplications` 中可以确保它出现在用户点击 Packages 图标时显示的列表中。当应用程序在桌面机器上运行时，绝对路径 `appsApplications/pics/` 实际上相对于 Qtopia 的镜像，而镜像正在被 `bin` 替换。

`unitconverter.desktop` 提供了关于应用程序的一些基本信息。出于其目的，它用于确保应用程序出现在应用程序列表中。这是完整的文件：

```
[Desktop Entry]
Comment[]=A program to convert between various units of measurement
Icon=unitconverter/Example
Type=Application
Name[]=Unit Converter
```

我们提供的信息仅是可以指定内容的子集。例如，我们可以提供有关翻译的信息。注意图标没有文件扩展名（如 `.png`）；我们让 Qtopia 资源系统去查找并显示合适的图片。

到为止，我们有一个特殊且手动编辑的 `.pro` 和 `.desktop`。我们只需要再做最后一个 Qtopia 特定的操作，就可以使用标准的 Qt 以标准的方式编写 `unitconverter.h` 和 `unitconverter.cpp`。对于 Qtopia，我们必须遵循特定的用法来挂接到环境的其他部分；完整的 `main.cpp` 简化为以下几行：

```
#include <QtopiaApplication>
#include "unitconverter.h"
QTOPIA_ADD_APPLICATION("UnitConverter", UnitConverter)
QTOPIA_MAIN
```

主窗口类的名称包含自 `unitconverter.h` 是 `UnitConverter`。通过 `QTOPIA_MAIN` 宏配合 `qtopiamake`、`unitconverter.h` 和 `unitconverter.cpp`，我们可以产生一个在 Qtopia 环境中运行的 Qtopia 应用程序。由于应用程序除了 `main.cpp` 外使用的是标准 Qt，它也可以作为普通的 Qt 应用程序编译和运行。为了做到这一点，我们需要使用标准的 `qmake` 并将 `main.cpp` 修改为如下：

```
#include <QApplication>
#include "unitconverter.h"

int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    UnitConverter converter;
    converter.show();
    return app.exec();
}
```

此外，我们必须注释掉 `.pro` 文件中的 `qtopia_project()` 行。对于只需要 Qt/嵌入式 Linux 的应用程序，通常作为标准 Qt 应用程序进行开发更方便，可以显式地 `resize()` 主窗口以适应手机或 PDA 的尺寸，然后在准备就绪将其转换为 Qt 应用程序。或者，可以使用两个不同的 `main.cpp` 文件，例如 `main_desktop.cpp` 和 `main_qtopia.cpp`，以及两个 `.pro` 文件。

Unit Converter 应用程序的大部分代码与书中所示其他 Qt 示例相似，因此我们不再重复它。

要测试应用程序，我们必须运行 `make install`，然后运行 `runtopia`。一旦 Qtopia 在虚拟帧缓冲区中运行，我们可以点击 'Q' 按钮，点击 Packages 图标，然后点击“Unit Converter”。之后，我们可以通过更改金额和在组合框中选择不同的单位来操作该应用程序。

