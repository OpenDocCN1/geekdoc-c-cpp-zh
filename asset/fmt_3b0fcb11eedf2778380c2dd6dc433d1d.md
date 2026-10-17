
要创建自定义配置，我们手动提供 `qconfig-xxx` 并像使用 C++ 函数一样使用它。Qt/Embedded Linux 提供了以下类：

| 类 | 基础自 |
| :--- | :--- |
| `QScreen` | Screen |
| `QScreenPlugin` | Screen plugins |
| `QMouse` | Mouse |
| `QMousePlugin` | Mouse plugins |
| `QKeyboard` | Keyboard |
| `QKeyboardPlugin` | Keyboard plugins |
| `QInputMethod` | Input methods |
| `QInputMethodPlugin` | Input method plugins |
| `QDecoration` | Window style |
| `QDecorationPlugin` | Window plugins |

Qt/Embedded Linux 支持以下字体格式：TrueType (`TTF`)、PostScript Type 1、位图字体 (`BDF`) 以及 Qt 渲染字体 (`QPF`)。由于 `QPF` 是一种光栅格式，它比 `TTF` 和 Type 1 等矢量格式更快且更紧凑。可以使用 `makeqpf` 工具预渲染 `TTF` 或 Type 1 文件并将其保存为 `QPF`。

## Qt 应用程序集成

由于 Linux 与桌面版本提供相同的 API，任何标准的 Qt 应用程序都可以重新编译运行在 Qt/Embedded Linux 上。但在实践中，最好创建专门的应用程序，以适应运行 Qt/Embedded Linux 的典型小屏幕、有限或无键盘以及资源限制。此外，Qtopia 还提供了针对移动设备的额外库，我们可能在 Qt/Embedded Linux 应用程序中使用它们。

在开始编写使用 Qtopia API 的应用程序之前，我们需要构建并安装 Qtopia SDK，包括其自带的 Qt/Embedded Linux。在这里，我们假设使用的是 Qtopia 开源版 4.2，它包含了 Qtopia 手机版的所有内容。

构建 Qtopia 与标准的 Unix 方法不同，因为 Qtopia 不应该在源码目录内构建。例如，如果我们把包 `qtopia-opensource-src-4.2.4.tar.gz` 下载到 `$HOME/downloads` 目录，我们将如下准备构建 Qtopia：

```
cd $HOME/downloads

gunzip qtopia-opensource-src-4.2.4.tar.gz

tar xvf qtopia-opensource-src-4.2.4.tar
```

现在我们必须创建一个用于构建 Qtopia 的目录，例如：

```
cd $HOME

mkdir qtopia
```

为了方便起见，建议设置 `QPEDIR` 环境变量。例如：

```bash
export QPEDIR=$HOME/qtopia
```

在这里我们假设使用的是 Bash Shell。现在我们准备好构建 Qtopia 了：

```
cd $QPEDIR

$HOME/downloads/qtopia-opensource-src-4.2.4/configure

make

make install
```

未指定任何要配置的选项，但你可能希望这样做。运行 `configure -help` 可以查看可用选项。

安装后，所有的 Qtopia 文件将位于 `$QPEDIR/image`，而用户通过与 Qtopia 交互产生的文件将位于 `$QPEDIR/home`。在 Qtopspeak 中，“image"（镜像）是一个存储在桌面计算机上的 Qtopia 文件系统，当 Qtopia 环境处于虚拟帧缓冲区时会被其使用。

Qtopia 提供了自己的一套完整的文档集，非常值得熟悉一下，因为 Qtopia 提供了许多 Qt 桌面环境不具备（或与之不相关）的类。它的起点是 `$QPEDIR/doc/html/index.html`。

完成构建和安装后，我们可以通过运行 `$QPEDIR/scripts/runtopia` 进行初始测试。该脚本会启动带有特殊皮肤的虚拟缓冲区和 `qpe`，`qpe` 是包含 Qtopia 应用栈的 Qtopia 环境。我们可以分别启动虚拟缓冲区和 Qtopia 环境，但我们必须按照正确的顺序启动。如果我们不小心先启动了 `qpe`，Qtopia 将写入 X11 帧缓冲区，这将损坏屏幕。执行 `runtopia` 脚本时可以使用 `-help` 参数查看其支持的命令行选项列表。这些包括 `-skin` 以及一个可选的皮肤列表。

虚拟缓冲区有一个右键菜单，在 Qtopia 区域以外的任何地方点击右键即可弹出。菜单允许我们调整显示并终止 Qtopia。

现在 Qtopia 已经在虚拟帧缓冲区中运行，我们可以构建提供的示例应用程序之一，以查看该过程是如何运作的。然后，我们将从头开始创建一个非常简单的应用程序。

切换目录到 `$QPEDIR/examples/application`。此 Qtopia 有它自己的版本 `make qtopiamake`，位于 `$QPEDIR/bin`。运行它进行编译，然后运行 `make install`；这将示例（以及一些其他文件）复制到 Qtopia 的镜像目录中。现在，如果我们终止 Qtopia 并使用 `runtopia` 重新启动，我们新建的“Example”（示例）应用程序就可以用了。要运行该示例，点击 Qtopia 区域底部中间的 'Q' 按钮，然后点击 Packages（“箱子”）图标（位于指向手上方），然后点击“Example”（见图 24.3）。

我们通过创建一个名为 Unit Converter（单位转换器）的小而实用的 Qtopia 应用程序来结束本节，我们必须注意它。该应用程序如图 24.2 所示。它只使用 Qt API，几乎没有惊喜。在下一节中，我们将创建一个使用一些 Qtopia 特定 API 的更复杂的示例。

### 图 24.2. 单位转换器应用程序

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

### 图 24.3. 定位示例应用程序

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

## Qtopia APIs

Qtopia Edition 和 Qtopia Phone Edition 提供了一组与移动设备用户相关的应用程序。这些应用程序的大多数功能都被抽象为库，或者使用了特定于版本的库。这些库可以在我们自己的 Qtopia 应用程序中使用，使我们能够访问设备服务，如闹钟、电子邮件、电话拨号、短信、语音录制等。

如果我们想从应用程序中访问设备特定功能，有许多选择：

- 我们可以使用 Qt/Embedded Linux 并编写自己的代码来与设备交互。
- 我们可以获取现有的 Qtopia 应用程序并对其修改以实现我们需要的功能。
- 可以使用额外的 API 进行编写，例如 Qtopia Phone API 或 Qtopia PIM（个人信息管理器）应用程序库。

在本节中，我们将采用最后一种方法。我们将编写一个简单的应用程序，用于记录简单的开支信息。它利用 Qtopia PIM 的数据弹出一个联系人列表，然后将开支报告作为短信消息发送给选定的联系人。它还演示了如何使用 Qtopia 对大多数手机上常见的多功能“软键”的支持。

如图 24.4 所示，该应用程序将出现在应用程序包列表中，就像我们在上一节中构建的示例一样。和之前一样，我们将首先查看 .pro 文件，然后是 .desktop 文件，最后是应用程序的源代码。这里是 expenses.pro：

```
qtopia_project(qtopia app)

depends(libraries/qtopiapim)

CONFIG += qtopia_main no_quicklaunch

HEADERS += expensedialog.h \
expensewindow.h \
SOURCES += expense.cpp \
expensedialog.cpp \
expensewindow.cpp \
main.cpp

INSTALLS += desktop pics

desktop.files = expenses.desktop
```

```
deskt = appsApplications

desktop.hint = desktop

pics.files = pics/*

pics.path = picsexenses

pics.hint = pics

pkg.name = expenses

pkg.desc = A program to record and SMS expenses

pkg.version = 1.0.0

pkg.domain = window
```

### 图 24.4. 定位并运行 Expenses 应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_943_0.png)

`qtopia_project()` 行与之前相同。由于此应用程序依赖于 Qtopia PIM 库，我们使用 `depends()` 指令来指定该库。如果想使用多个库，可以通过逗号将它们分开。.pro 文件的其余部分与我们在单元转换器示例中看到的相似，这次我们有更多源文件，因为该应用程序更加复杂。

`expenses.desktop` 文件与我们之前看到的非常相似：

```
[Desktop Entry]

Comment[]=A program to record and SMS expenses

Exec=expenses/expenses

Icon=expenses/expenses

Type=Application

Name[]=Expenses
```

`main.cpp` 也是如此：

```cpp
#include <QtopiaApplication>
```

```cpp
#include "expensewindow.h"

QTOPIA_ADD_APPLICATION("Expenses", ExpenseWindow)

QTOPIA_MAIN
```

我们现在将查看 Expenses 应用程序的头文件以及源代码中与 Qtopia 特有或特别相关的部分，从 Expense 类开始：

```cpp
class Expense
{
public:
    Expense();
    Expense(const QDate &date, const QString &desc, qreal amount);
    bool isNull(const);
    void setState(const QDate &date);
    QDate date() const;
    void setDescription(const QString &desc);
    QString description() const;
    void setAmount(qreal amount);
    qreal amount() const;
private:
    QDate my;
    QString myDesc;
    qreal myAmount;
};
```
