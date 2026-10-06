

当直接向 QIODevice 写入文本时，必须向 `open()` 函数显式指定 `QIODevice::Text` 标志，例如：

```cpp
file.open(QIODevice::WriteOnly | QIODevice::Text);
```

在写入时，此标志告诉 QIODevice 在 Windows 上将 '\n' 字符转换为 '\r\n' 序列。在读取时，此标志告诉设备在所有平台上忽略 '\r' 字符。这样我们就可以假设无论操作系统使用什么行结束约定，每行的末尾都是用 '\n' 换行符标记的。

## 遍历目录

QDir 类提供了一种与平台无关遍历目录和检索文件信息的方法。为了了解如何使用 QDir，我们将编写一个小型控制台应用程序，计算特定目录及其任何深度的子目录下所有图像所占用的空间。

应用程序的核心是 `imageSpace()` 函数，它递归地计算给定目录图像的累积大小：

```cpp
qlonglong imageSpace(const QString &path)
{
    QDir dir(path);
    qlonglong size = 0;

    QStringList filters;
    foreach (QByteArray format, QImageReader::supportedImageFormats())
        filters += ".*" + format;

    foreach (QString file, dir.entryList(filters, QDir::Files))
        size += QFileInfo(dir, file).size();

    foreach (QString subDir, dir.entryList(QDir::Dirs | QDir::NoDotAndDotDot))
        size += imageSpace(path + QDir::separator() + subDir);

    return size;
}
```

我们开始使用给路径创建一个 QDir 对象，该路径可以是相对于当前目录的绝对路径。我们向 `entryList()` 函数传递了两个参数。第一个是文件名列表。它们可以包含 '*' 和 '?' 通配符。在这个示例中，我们过滤出只包含 QImage 可以读取的文件格式。第二个参数指定了我们想要什么类型的条目（普通文件、目录、驱动器等）。

我们遍历它们（排除 . 和 ..）并递归调用 `imageSpace()` 来确定它们的累积图像大小。为了创建每个子目录的路径，我们将当前目录的路径与子目录名称结合，并用斜杠分隔。QDir 在所有平台上将 '/' 视为目录分隔符，同时也识别 Windows 上的 '\'，并提供 `nativeSeparators()` 来将斜杠转换为特定平台的分隔符。或者，我们可以调用静态函数 `QDir::nativeSeparators()`。

为我们的的小程序添加一个 `main()` 函数：

```cpp
int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);
    QString args = QCoreApplication::arguments();
    QString path = QDir::currentPath();
    if (args.count() > 1)
        path = args[1];

    std::cout << "Space used by images in " << qPrintable(path)
              << (imageSpace(path) / 1024) << " KB" << std::endl;

    return 0;
}
```

我们使用 `QDir::currentPath()` 初始化路径为当前目录。或者，我们可以使用 `QDir::homePath()` 将其初始化为用户主目录。如果用户在命令行中指定了路径，我们将使用该路径。最后，我们调用 `imageSpace()` 函数来计算图像消耗了多少空间。

QDir 类提供了其他与文件和目录相关的函数，包括 `entryList()`（返回 QFileInfo 对象列表）、`rename()`、`exists()`、`mdir()` 和 `rmdir()`。QFile 类提供了一些便利函数，包括 `remove()` 和 `exists()`。QFileSystemWatcher 类可以通过发射 `directoryChanged()` 和 `fileChanged()` 信号，在目录或文件发生变化时通知我们。

## 嵌入资源

到本章为止，我们已经讨论了如何访问外部设备中的数据，但在 Qt 中，也可以将二进制数据或文本嵌入到应用程序的可执行文件中。这是通过 Qt 的资源系统实现的。在其他章节中，我们使用资源文件将图像嵌入到可执行文件中，但也可以嵌入任何类型的文件。嵌入的文件可以像文件系统的普通文件一样使用 `QFile` 读取。

资源由 `rcc`（Qt 的资源编译器）转换为 C++ 代码。我们可以通过在 .pro 文件中添加此行来告诉 qmake 由 rcc 包含特殊规则：

```
RESOURCES = myresourcefile.qrc
```

`myresourcefile.qrc` 是一个 XML 文件，列出了要嵌入可执行文件的文件。

假设我们正在编写一个保存联系人详情的应用程序。为了方便用户，我们希望将国际拨号代码嵌入到可执行文件中。如果文件位于应用程序构建目录下的 datafiles 目录，资源文件可能如下所示：

```xml
<RCC>
  <q>
    <file>datafiles/phone-codes.dat</file>
  </q>
</RCC>
```

在应用程序中，资源通过 `:/` 路径前缀识别。在这个示例中，拨号代码文件的路径为 `:/datafiles/phone-codes.dat`，像任何其他文件一样使用 `QFile` 读取。

在可执行文件中嵌入数据的优点是它不会丢失，并且使得创建真正独立的可执行文件成为（如果使用了静态链接）。两个缺点是：如果嵌入数据需要更改，必须替换整个可执行文件，而且可执行文件的大小更大，因为它必须容纳嵌入的数据。

Qt 的资源系统提供了比我们在示例中演示更多的功能，包括对别名和本地化的支持。这些功能可以在 http://doc.qt.io/4.3/resources.html 查看。

## 进程间通信

QProcess 允许我们运行外部程序并与其进行交互。该类是异步工作的，在后台执行任务，以便用户界面保持响应。QProcess 在外部进程拥有数据或完成时发射信号通知我们。

我们将回顾一个为图像转换提供用户界面的应用程序代码。在这个示例中，我们依赖所有主要平台上提供的 ImageMagick convert。我们的用户界面如图 12.2 所示。

### 图 12.2 图像转换器应用程序

![](img/5a52abdf0b0d58fa99d30abb446361.png)

用户界面是在 Qt Designer 中创建的。ui 文件随本书的示例一起。在这里，我们将关注派生自 uic 生成的 Dialog 类，头文件如下：

```cpp
#ifndef CONVERTDIALOG_H
#define CONVERTDIALOG_H

#include <QDialog>
#include <QProcess>

#include "ui_convertdialog.h"

class ConvertDialog : public QDialog, private Ui::Dialog
{
  Q_OBJECT
public:
    ConvertDialog(QWidget *parent = 0);

private slots:
    void on_browseButton_clicked();
    void convertImage();
    void updateOutputText();
    void processFinished(int exitCode, QProcess::ExitStatus exitStatus);

private:
    void processError(QProcess::ProcessError error);

    QProcess process;
    QString targetFile;
};
#endif
```

头文件遵循 Qt Designer 表单类的类的模式。与我们看到的其他示例的一个微小区别是，这里我们对 `Ui::Dialog` 类使用了私有继承。这防止了从表单外部访问控件。得益于 Qt Designer 的自动连接机制，`on_browseButton_clicked()` 槽会自动连接到浏览按钮的 `clicked()` 信号。

```cpp
ConvertDialog::ConvertDialog(QWidget *parent)
: QDialog(parent)
{
    setupUi(this);

    QPushButton *convertButton = buttonBox->button(QDialog::Ok);
    convertButton->setText(tr("&Convert"));
    convertButton->setEnabled(false);

    connect(convertButton, SIGNAL(clicked()),
           this, SLOT(convertImage()));
    connect(buttonBox, SIGNAL(rejected()), this, SLOT(reject()));
    connect(&process, SIGNAL(readyStandardError()),
           this, SLOT(updateOutputTextEdit()));
    connect(&process, SIGNAL(finished(int, QProcess::ExitStatus)),
           this, SLOT(processFinished(int, QProcess::ExitStatus)));
    connect(&process, SIGNAL(error(QProcess::ProcessError)),
           this, SLOT(processError(QProcess::ProcessError)));
}
```

